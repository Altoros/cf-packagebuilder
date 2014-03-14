cf-packagebuilder
=================

scripts
---

`./build` - creates source packages that are ready to be uploaded to launcpad.net.
`./build deb` - is used for testing packages

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


Package structure 
---

[cf-charm launcpad](https://launchpad.net/~cf-charm/+archive/ppa/+packages) repo has two kinds of packages. For instance for dea you will find `cfdea` and `cfdeajob` packages. `cfdea` will install `dea` within `/var/lib/cloudfoundry/cfdea/` folder and `cfdeajob` will add `/var/lib/cloudfoundry/cfdea/jobs` folder with all necessary binaries and configs. `cfdeajob` is created from cf-release with [job2package-tool](https://github.com/Altoros/cf-job2package-tool/blob/master/build.rb) script.


