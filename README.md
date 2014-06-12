liblmdb
=======

LMDB: an embeddable, open-source, high-performance database. http://symas.com/mdb

This repo created for convenience of project management. Source:

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

Supports Linux, Windows, OSX, and probably others.

[1]http://symas.com/mdb
[2]http://symas.com/mdb/hyperdex/
[3]http://symas.com/mdb/microbench/

