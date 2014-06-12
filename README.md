liblmdb
=======


Lightning Memory-Mapped Database (LMDB): an embeddable, open-source, high-performance database library. http://symas.com/mdb. This is a B-tree based key-value store, using a memory mapped file for performance.

This github repo was created for convenience of project management. Source for (possibly) more up-to-date versions:

git clone -b mdb.master git://git.openldap.org/openldap.git  # on June 11, 2014 / 17c09fa476a7dbd49aca5e4caf0384cb1c3d244a

Quick Overview
--------------

LMDB is a tiny database with some great capabilities[1]:

 *   Ordered-map interface (keys are always sorted, supports range lookups)
 *   Fully transactional, full ACID semantics with MVCC.
 *   Reader/writer transactions: readers don't block writers and writers don't block readers. Writers are fully serialized, so writes are always deadlock-free.
 *   Read transactions are extremely cheap, and can be performed using no mallocs or any other blocking calls.
 *   Multiple sub-databases may be created with transactions covering all sub-databases.
 *   Memory-mapped, allowing for zero-copy lookup and iteration.
 *   Maintenance-free, no external process or background cleanup/compaction required.

Intro 
-----

From the docs at [http://symas.com/mdb/doc/]:

> MDB is a Btree-based database management library modeled loosely on the BerkeleyDB API, but much simplified. The entire database is exposed in a memory map, and all data fetches return data directly from the mapped memory, so no malloc's or memcpy's occur during data fetches. As such, the library is extremely simple because it requires no page caching layer of its own, and it is extremely high performance and memory-efficient. It is also fully transactional with full ACID semantics, and when the memory map is read-only, the database integrity cannot be corrupted by stray pointer writes from application code.
> 
> The library is fully thread-aware and supports concurrent read/write access from multiple processes and threads. Data pages use a copy-on- write strategy so no active data pages are ever overwritten, which also provides resistance to corruption and eliminates the need of any special recovery procedures after a system crash. Writes are fully serialized; only one write transaction may be active at a time, which guarantees that writers can never deadlock. The database structure is multi-versioned so readers run with no locks; writers cannot block readers, and readers don't block writers.
> 
> Unlike other well-known database mechanisms which use either write-ahead transaction logs or append-only data writes, MDB requires no maintenance during operation. Both write-ahead loggers and append-only databases require periodic checkpointing and/or compaction of their log or database files otherwise they grow without bound. MDB tracks free pages within the database and re-uses them for new write operations, so the database size does not grow without bound in normal use.
> 
> The memory map can be used as a read-only or read-write map. It is read-only by default as this provides total immunity to corruption. Using read-write mode offers much higher write performance, but adds the possibility for stray application writes through pointers to silently corrupt the database. Of course if your application code is known to be bug-free (...) then this is not an issue.


Feature Comparison[1]
------------------

~~~
A quick comparison of popular embedded key/value stores.
                              LMDB      BDB        LevelDB    Kyoto TreeDB
ACID Transactions             x         x         
Nested Transactions           x         x               
Multiple Namespaces           x         x                       
Sorted Keys                   x         x          x          x
Sorted Duplicate Keys         x         x                               
Multi-thread concurrency      x         x          x          x
Multi-process concurrency     x         x                                       
No cache tuning: zero-config  x                                                         
Instantaneous crash recovery  x
Zero-copy reads               x
Zero-copy writes              x
Atomic hot backup             x
~~~

LMDB out performs LevelDB unless you are doing almost-all small writes.[2][3] And even then LMDB may be preferrable due to predictable latency, low CPU usage, and the features in the first column above. It is probably not a good choice when data size is over 10x memory size. That's why it is referred to as an embedded database library.

Supports Linux, Windows, OSX, Android, and BSD variants, probably others.
LMDB authored by: Howard Chu, Symas Corporation.


[1]http://symas.com/mdb
[2]http://symas.com/mdb/hyperdex/
[3]http://symas.com/mdb/microbench/

