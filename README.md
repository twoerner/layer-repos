layer-repos
===========

First-Time
----------

Please review the OpenEmbedded/Yocto documentation and make sure your Linux
development machine is supported and you have all the prerequisites installed:

	http://www.yoctoproject.org/docs/current/yocto-project-qs/yocto-project-qs.html

The following steps only need to be performed once, the first time you work
with this repository.

If you've never used "repo" before, or don't have "repo" installed on your
computer, you'll need to perform the following once:

	$ mkdir ~/bin
	$ export PATH=~/bin:$PATH
	$ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
	$ chmod +x ~/bin/repo

To initialize the repositories:

	$ repo init -u git://github.com/twoerner/layer-repos.git

This will pull down the "master" branch by default. If you want to work on a
branch other than "master" simply specify it with the "-b <branch>" option to
"repo init". For example, to work with the "fido" branch:

	$ repo init -u git://github.com/twoerner/layer-repos.git -b fido

Now that all the metadata is initialized you need to actually pull the
repositories down:

	$ repo sync

You now have all the data you need to start building. To start a build you
need to setup your build environment:

	$ . setup

You'll be prompted to choose your MACHINE, SDKMACHINE, DISTRO, shared state
location (SSTATE_DIR), and download location (DL_DIR).

If you want to specify a build directory (for performing multiple builds
from the same set of layers) simply include your build directory name as a
parameter to the "setup" script:

	$ . setup <build_dir>
	e.g.
	$ . setup rpi-linaro-build

A build directory of "build" will be used by default if you don't specify a
build directory name.

After successfully setting up your build environment, you can now issue
"bitbake" commands.

If you would like to see, again, the list of (for example) possible images you
can invoke the "setup" script as a regular script (i.e. instead of sourcing
it):

	$ ./setup

and it will show all the: Available Machines, Available SDK Machines,
Available Distros, and Available Images.


Creating A Local Topic Branch
-----------------------------

If you want to work on the layers it'll be easier to do so if you create a
"topic branch" for your work:

	$ repo start <topic-name> --all

To only create branches on specific repos (repo1, repo2):

	$ repo start <topic-name> repo1 repo2


Updating
--------

If you've been working on (for example) "master" and want to grab all the
latest upstream commits since you last "repo sync"'ed, simply:

	$ repo sync -dl
	$ repo sync

You can now rebase your local commits with:

	$ repo rebase


Maintainer
----------

* Trevor Woerner <mailto:twoerner@gmail.com>
