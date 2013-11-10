## Synopsis
AMZN-base creates a base AMI for running web apps. It conforms to the AMZN archatecture API which means apps using AMI-base can be deployed and managed by AMZN-ship.

## Dependencies

* Packer - http://www.packer.io/
* IAM Role for access to S3.

## Using Packer to Create the AMI
The AMI is responsible for installing Ruby and some helper programs for deployment. See the `bin` directory for the list of programs copied into the AMI.

```bash
$ build-ami frameworks/node
...
us-east-1: ami-1d3e7074
$ export AMZN_AMI=ami-1d3e7074
```

## Building the AMI
The build process is simple. We take the filsystem in `./target-machine` and copy it onto the root filesystem of the host. Once the filesystem is in place, the setup script will use apt-get to install a base set of software (e.g. build-essential).

The build command takes an argument which is the location of a bash file that descibes the framework. This file contains a set of commands that will setup the AMI for the application it is to run. For example, the framework file will setup the AMI for a Ruby on Rails app.
