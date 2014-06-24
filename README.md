AMZN-base is an implementation of the architecture defined in the [Application Platform on AWS](http://r.32k.io/app-platforms-on-aws) article. AMZN-base assumes the AMI is controlled with [amzn-ship](https://github.com/ryandotsmith/amzn-ship).

## Dependencies

* Packer - http://www.packer.io/

## Using Packer to Create the AMI
The AMI is responsible for installing a framework with its dependencies and some helper programs for deployment. See the `bin` directory for the list of programs copied into the AMI.

```bash
$ build-ami frameworks/node ami-7cb04b14
...
us-east-1: ami-1d3e7074
$ export AMZN_AMI=ami-1d3e7074
```

## Building the AMI
The build process is simple. We take the filesystem in `./target-machine` and copy it onto the root filesystem of the host. Once the filesystem is in place, the setup script will use apt-get to install a base set of software (e.g. build-essential).

The `build-ami` command takes two arguments. The first is the location of a bash file that describes the framework. This file contains a set of commands that will setup the AMI for the application it is to run. For example, the `framework/node` file will setup the AMI for a nodejs app.

The second argument specifies which AMI to use as the basis for the image. Canonical publishes a list of "Ubuntu Cloud Image" AMIs at https://cloud-images.ubuntu.com/
