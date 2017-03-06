Generating the DS3 Python3 SDK Documentation
===========================================

The Python3 SDK documentation is built using [Sphinx](http://sphinx-doc.org/).

To install sphinx on Ubuntu, run the following command:

    $ sudo apt-get install python-sphinx

The Python documentation is on the branch gh-pages (Github hosted sites need to be on a branch named gh-pages,
so any changes to the documentation need to be on this branch, not master). Pull from this branch, and you should see an
a directory called sphinx in the repository. This directory is where all the documentation actually lives.

Sphinx generates it's documentation from installed modules, so before generating documentation,
make sure the ds3.ds3 Python3 module is installed.

To install the ds3.ds3 module, run

    $ sudo python3 setup.py install
    
Create sphinx-build3 (Ubuntu)
-----------------------------
To create a compatible sphinx-build3 that won't conflict with the python2 compatible sphinx-build, create a new /usr/bin/sphinx3-build file:
    
    $ sudo touch /usr/bin/sphinx-build3

with the following contents:

```
#!/usr/bin/python3
# -*- coding: utf-8 -*-
"""
Same as /usr/bin/sphinx-build but with different
interpreter
"""

import sys

if __name__ == '__main__':
    from sphinx import main, make_main
    if sys.argv[1:2] == ['-M']:
        sys.exit(make_main(sys.argv))
    else:
        sys.exit(main(sys.argv))
```


Generating documentation
------------------------

To (re)generate the documentation, navigate to the directory the documentation is in,
"repository"/sphinx/"version you want to generate" (currently v3.4.1), and run

    $ sphinx3-build -b html source/ .


Adding a new version or release
-------------------------------

To add a new version of the documentation, navigate to the sphinx directory and copy one of the existing directories into
a new directory corresponding to the version and release you want. In the new directory, edit the variables 'source' and
'release' in the file <new directory>/source/conf.py to match the new version and release numbers. Run

    $ sphinx3-build -b html source/ .
