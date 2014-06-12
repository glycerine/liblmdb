liblmdb
=======

LMDB: an embeddable, open-source, high-performance database. http://symas.com/mdb

This repo created for convenience of project management. Source:

git clone -b mdb.master git://git.openldap.org/openldap.git  # on June 11, 2014 / 17c09fa476a7dbd49aca5e4caf0384cb1c3d244a


Feature Comparison
------------------

~~~
A quick comparison of popular embedded key/value stores.
  LMDB  BDB        LevelDB    Kyoto TreeDB
ACID Transactions  x          x         
Nested Transactions           x         x               
Multiple Namespaces           x         x                       
Sorted Keys                   x         x                       x       x
Sorted Duplicate Keys         x         x                               
Multi-thread concurrency      x         x                               x       x
Multi-process concurrency     x         x                                       
No cache tuning: zero-config  x                                                         
Instantaneous crash recovery  x                                                                         
Zero-copy reads     x                                                                                           
Zero-copy writes    x                                                                                                    
Atomic hot backup   x
~~~

LMDB out performs LevelDB unless you are doing almost-all small writes.[1][2]

[1]http://symas.com/mdb/hyperdex/
[2]http://symas.com/mdb/microbench/

