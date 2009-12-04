dvcs_jslint
===========

Instructions and a script that runs [JSLint](http://www.jslint.com/) as a pre-commit hook, usable for
either Git or Mercurial.

As it says on the tin, JSLint will hurt your feelings. Only use this if you like pain.
I take no responsibility for any anguish suffered when using JSLint.

See the [JSLint info page](http://www.jslint.com/lint.html) for configuration options that you can put in your .js files to avoid some
of the complaints.

Prerequisites
-------------

* [Java](http://java.sun.com/), probably at least Java 5. You may already have it
on your computer -- type "java -version" on the command line to find out.
* [Rhino](http://www.mozilla.org/rhino/download.html) (just the js.jar file): 
* [jslint.js](http://www.jslint.com/rhino/jslint.js)
* dvcs_jslint.js, the file that is next to this README.

Put js.jar and jslint.jar into a directory, for this example, let's use "dvcs_jslint"
as the directory name, and assume it is in your home directory (noted as ~ below).

So, inside **~/dvcs_jslint/** (as an example):

* js.jar
* jslint.js
* dvcs_jslint.js

Now time to configure your DVCS to use this information:

Git
---
In your .git directory for your local repository, create a file called **.git/hook/pre-commit**
with the following contents:

    #!/bin/sh
    exec java -jar ~/dvcs_jslint/js.jar ~/dvcs_jslint/dvcs_jslint.js ~/dvcs_jslint/js.jar ~/dvcs_jslint/jslint.js git

Replace ~/dvcs_jslint/ above with the appropriate path that you set up in the
Prerequisites section.

Mercurial
---------
In the .hg directory for your local repository, modify **.hg/hgrc** to have this
line in it:

    [hooks]
    precommit.jslint = java -jar ~/dvcs_jslint/js.jar ~/dvcs_jslint/dvcs_jslint.js ~/dvcs_jslint/js.jar ~/dvcs_jslint/jslint.js hg

Replace ~/dvcs_jslint/ above with the appropriate path that you set up in the
Prerequisites section.

Caveats
-------

* I have not tried it on Windows
* The script assumes English output from the DVCS commands and may break if
the format of the DVCS commands are different from the stock installs. See
the source of dvcs_jslint.js in case you are unsure.
