=========================
Installing Search Engines
=========================

Solr
====

Solr is Java but comes in a pre=packaged form that requires very little other
than the JRE and Jetty. It's very performant and has an advanced featureset.
Haystack requires Solr 1.3+. Installation is relatively simple::

    curl -O http://apache.mirrors.tds.net/lucene/solr/1.3.0/apache-solr-1.3.0.tgz (or another mirror from http://www.apache.org/dyn/closer.cgi/lucene/solr/)
    tar xvzf apache-solr-1.3.0.tgz
    cd apache-solr-1.3.0
    cd example
    java -jar start.jar

You'll need to revise your schema. You can generate this from your application
(once Haystack is installed and setup) by running 
``./manage.py build_solr_schema``. Take the output from that command and place
it in ``apache-solr-1.3.0/example/solr/conf/schema.xml``. Then restart Solr.

You'll also need a Solr binding, ``pysolr``. The development version can be
grabbed from GitHub via http://github.com/toastdriven/pysolr/tree/master. In the
near future, this should be merged into the main ``pysolr`` package and
distributed via PyPI. Place ``pysolr.py`` somewhere on your ``PYTHONPATH``.


Whoosh
======

Whoosh is pure Python, so it's a great option for getting started quickly. For
now (as of 2009/04/17), it requires a bit of patching (Whoosh version 0.1.13).
The patch needed is included with Haystack (at the root as
``whoosh-0.1.13.patch``), so it's best to grab either a source distribution
or Subversion, apply the patch and install.::

    svn co http://svn.whoosh.ca/projects/whoosh/trunk/ whoosh
    cd whoosh
    patch -p1 < /path/to/your/haystack/whoosh-0.1.13.patch
    sudo python setup.py install


Xapian
======

Xapian is written in C++ so it requires compilation (unless your OS has a
package for it). Installation looks like::

    curl -O http://oligarchy.co.uk/xapian/1.0.7/xapian-core-1.0.7.tar.gz
    curl -O http://oligarchy.co.uk/xapian/1.0.7/xapian-bindings-1.0.7.tar.gz
    
    tar xvzf xapian-core-1.0.7.tar.gz
    tar xvzf xapian-bindings-1.0.7.tar.gz
    
    cd xapian-core-1.0.7
    ./configure
    make
    sudo make install
    
    cd ..
    cd xapian-bindings-1.0.7
    ./configure
    make
    sudo make install