sudocker
========

`sudocker` can be used to become `root` by being on the `docker` group.

Copyright (C) 2018  Morphus Labs.  Released under the GPLv3.

This script leverages the fact that anyone in the `docker` group is `root`
equivalent:

* _"Warning: The docker group grants privileges equivalent to the root user."_
        -- https://docs.docker.com/install/linux/linux-postinstall/

* _"Anyone added to the docker group is root equivalent"_
        -- https://wiki.archlinux.org/index.php/Docker

* _"This needs more prominent documentation. Yes it's there, half way down
    the page, but it's effectively hidden in a "security speak" document."_
        -- @markriggins, https://github.com/docker/docker/issues/9976

* _"First of all, only trusted users should be allowed to control your Docker
   daemon."_
        -- https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface

* _"Warning: The docker group is equivalent to the root user"_
        -- https://developer.fedoraproject.org/tools/docker/docker-installation.html

A lot of Docker tutorials skip this fact.


Usage
-----

	user$ wget "https://raw.githubusercontent.com/morphuslabs/sudocker/master/sudocker"
	user$ chmod +x sudocker
	user$ ./sudocker
	... wait a dozen seconds ...
	root#

You'll need to have Docker installed, the Docker daemon must be running and
your user must be on the `docker` group.

Remember to delete `/sudocker-su` afterwards:

	$ rm /sudocker-su


FAQ
---

* Is this a bug in Docker?

	No.  This is an [intended feature].


* Does this mean programs can escape from my Docker containers?

	No.  Unless you use the `--privileged` parameter, your docker containers
	should be safe (at least with regards to this feature).


* What can I do avoid passwordless privilege escalation using Docker?

	Don't add your user to the `docker` group.
	Use `sudo` whenever you call `docker run`.


Bugs
----

Report bugs in [sudocker's issue tracker on GitHub].

Known bug:  this README is longer than the code.


[intended feature]: https://github.com/docker/docker/issues/9976
[sudocker's issue tracker on GitHub]: https://github.com/morphuslabs/sudocker/issues
