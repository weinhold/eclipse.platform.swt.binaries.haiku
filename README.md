eclipse.platform.swt.binaries.haiku
===================================

This repository emulates the structure of the Eclipse/SWT
eclipse.platform.swt.binaries, limiting it to the files needed for building the
Haiku SWT port. Unlike the original repository it doesn't contain any generated
binaries.

Below you find instructions for building SWT/Haiku.


Dependencies
------------

The following dependencies need to be installed to build SWT/Haiku:

* Haiku x86 gcc4[h] (other flavors haven't been tested, but might work)
* OpenJDK: If a package isn't available, it can be built from the recipe in the 
  HaikuPorts tree.
* Apache Ant: The available HaikuPorts package may not work. Best download a
  binary release (tested with 1.9.2) from the
  [Apache Ant home page](http://ant.apache.org/bindownload.cgi)
* Apache Commons Bean Scripting Framework (BSF): Download a binary release
  (tested with 2.4.0) from the
  [BSF home page](http://commons.apache.org/proper/commons-bsf/download_bsf.cgi)
* Apache Commons Logging: Download a binary release (tested with 1.1.3) from the
  [Apache Commons Logging home page
  ](http://commons.apache.org/proper/commons-logging/download_logging.cgi)
* Rhino: Download a binary release (tested with 1_7R4) from the
  [Rhino home page](https://developer.mozilla.org/en/RhinoDownload)


Setting things up
-----------------

The following directory layout is recommended:

    dependencies/
         apache-ant-1.9.2/
         bsf-2.4.0/
         commons-logging-1.1.3/
         rhino1_7R4/
         lib/
     eclipse.platform.swt/
     eclipse.platform.swt.binaries/

The procedure to set it up is straight-forward:

1. Create directory "dependencies" and extract the downloaded dependency archives there.
2. Create "dependencies/lib" and symlink all .jar files from the BFS, Commons Logging, and Rhino there.
3. Clone repository "eclipse.platform.swt", check out branch "R4_3_haiku".
4. Clone repository "eclipse.platform.swt.binaries.haiku" to "eclipse.platform.swt.binaries" (i.e. chop off the ".haiku").


Building
--------

Set ANT_HOME:

     export ANT_HOME=`pwd`/dependencies/apache-ant-1.9.2

Build native libraries:

     $ANT_HOME/bin/ant -f eclipse.platform.swt.binaries/bundles/org.eclipse.swt.haiku.haiku.x86/build.xml build_libraries -lib dependencies/lib

Build .jar files:

     $ANT_HOME/bin/ant -f eclipse.platform.swt.binaries/bundles/org.eclipse.swt.haiku.haiku.x86/build.xml build.jars -lib dependencies/lib
