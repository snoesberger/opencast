Install Opencast
================

Server requirements higly depend on on processed material.
There are a few hints about a sensible machine setup to run Opencast on:

- [Hardware requirements](server-requirements.md)

Since Opencast is written in Java, you may also need to ensure to have the correct version of Java installed.
On fresh installations, the packages will usually take care about that.

- [Java version requirements](java-version.md)


Installation from Repository
----------------------------

There are package repositories available for multiple operating systems. It provides packages containing pre-configured and
pre-built Opencast installations.

* [Red Hat 8/9 based](rpm-el.md)
    * [RedHat Enterprise Linux](rpm-el.md)
    * [CentOS Stream](rpm-el.md)
    * …
* [Debian based](debs.md)
    * [Debian](debs.md)
    * [Ubuntu](debs.md)


Installation with Docker
----------------------------

You can also use Docker to quickly install or test Opencast. There are multiple Docker images available for installing
Opencast on either a single or multiple server.

* [Testing Locally with Docker](docker-local.md)


Installation from Source
------------------------

These guides will help you to build Opencast, including all necessary third party tools.
This method will most likely work on all Unix-like systems and should be very similar on undocumented systems.

* [Linux](source-linux.md)
* [macOS](source-macosx.md) (no official support)


Installation Across Multiple Servers
------------------------------------

For production systems, it is recommended to install Opencast across multiple servers to separate the processing,
management and presentation layer, so that, for example, even if the processing layer is under full load, users can
still watch recordings unaffected since the presentation layer is running on a separate machine.

* [Installation Across Multiple Servers](multiple-servers.md)


Installation via Script
-----------------------

We provide configuration scripts to install and configure Opencast automatically.  These scripts rely on the
packages from the repository above.

* [Ansible](ansible.md)

Prerelease repository testing
----------------------------

We build nightly packages in all of our packaging types.  The [prerelease documentation](prereleases.md) documents how
to enable it.  This packaging is only for experts and should not be used by anyone aside from an experienced Opencast
adopter.
