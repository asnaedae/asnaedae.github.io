---
layout: single
title:  "Vagrant error during plugin install"
tags:
- vagrant
redirect_from: /2014/09/30/vagrant-plugin-gem-error/
---

Had the following error being thrown when trying to install the `vagrant-vbguest` plugin:

```
$  vagrant plugin install vagrant-vbguest
Installing the 'vagrant-vbguest' plugin. This can take a few minutes...
Bundler, the underlying system Vagrant uses to install plugins,
reported an error. The error is shown below. These errors are usually
caused by misconfigured plugin installations or transient network
issues. The error from Bundler is:

An error occurred while installing ffi (1.9.5), and Bundler cannot continue.
Make sure that `gem install ffi -v '1.9.5'` succeeds before bundling.

Gem::Installer::ExtensionBuildError: ERROR: Failed to build gem native extension.

    /Applications/Vagrant/embedded/bin/ruby extconf.rb
checking for ffi.h... *** extconf.rb failed ***
```
Followed the trail of suspects, including the above note to install the 'ffi' gem, and noticed that:

```bash
$ gcc --version


Agreeing to the Xcode/iOS license requires admin privileges, please re-run as root via sudo.
```

Well, ok, we can do that:-

```bash
$ sudo gcc --version


You have not agreed to the Xcode license agreements. You must agree to both license agreements below in order to use Xcode.

Hit the Enter key to view the license agreements at '/Applications/Xcode.app/Contents/Resources/English.lproj/License.rtf'
...
```
Now the plugin installs without errors:

```bash
$  vagrant plugin install vagrant-vbguest
Installing the 'vagrant-vbguest' plugin. This can take a few minutes...
Installed the plugin 'vagrant-vbguest (0.10.0)'!
```
