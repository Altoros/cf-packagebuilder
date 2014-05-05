cf-packagebuilder
=================

scripts
---

`./build` - creates source packages that are ready to be uploaded to launcpad.net.
`./build deb` - creates .deb binary files of packages that can be used to test package content. [WARNING] don't use this command if you want to upload packages to to launcpad.net, because launcpad.net doesn't accept binary files.

configs
---
`conf` contains configuration for all packages, github repositories and sha's of cf projects. 

check out [job2package-tool script](https://github.com/Altoros/cf-job2package-tool/blob/master/build.rb) to see how job from [cf-release](https://github.com/cloudfoundry/cf-release) could be converted to package.


How to install
---
All packages are loaded to [launchpad.net](https://launchpad.net/~cf-charm). If you need to install packages from this source, use this commands:
```
sudo su
apt-add-repository ppa:cf-charm/ppa 
aptitude update
aptitude install <package-name>
```
If you want to install package from the local machine run `./build deb` and install resulting deb package.

How to use 
---

To upload to launchpad.ned you need to do following: 
1. ask for keys to sign package and register this keys in your system: 
```
  sudo gpg --import <public-key-name>.gpg
  sudo gpg --allow-secret-key-import --import <private-key-name>.gpg
```
Also you can save this keys to `files/keys/pub.gpg` and `files/keys/pub.gpg` files and they will be loaded automatically during package building. (don't forget to ask password for this keys).

2. build packages with command `sudo ./build`
3. upload source packages to launchpad: 
```
cd pkgs
sudo dput ppa:cf-charm/ppa <package-name>_<package-version>_source.changes
```
`<package-version>` consists of two numbers: [global version](https://github.com/Altoros/cf-packagebuilder/blob/1e143d45f0308737d1a6aa39e437366d0ae7c763/conf#L15) (by default it is set to 153, the same with cf release) and [build version](https://github.com/Altoros/cf-packagebuilder/blob/1e143d45f0308737d1a6aa39e437366d0ae7c763/conf#L13) in format 1ppa3 (`$BUILD` variable is equal to 3 in this case)

To track launchpad issues you will need access to (cf-charm@altoros.com)[http://webmail.altoros.com
] email.


Package structure 
---

[cf-charm launcpad](https://launchpad.net/~cf-charm/+archive/ppa/+packages) repo has two kinds of packages. For instance for dea you will find `cfdea` and `cfdeajob` packages. `cfdea` will install `dea` within `/var/lib/cloudfoundry/cfdea/` folder and `cfdeajob` will add `/var/lib/cloudfoundry/cfdea/jobs` folder with all necessary binaries and configs. `cfdeajob` is created from cf-release with [job2package-tool](https://github.com/Altoros/cf-job2package-tool/blob/master/build.rb) script.


