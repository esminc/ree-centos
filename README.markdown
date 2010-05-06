# A Recipe for a Ruby Enterprise Edition RPM on CentOS

Perform the following on a build box as root.

## Create an RPM Build Environment

    yum install rpmdevtools
    rpmdev-setuptree

## Install Prerequisites for RPM Creation

    yum groupinstall 'Development Tools'

## Download REE

    cd /tmp
    wget http://rubyforge.org/frs/download.php/68719/ruby-enterprise-1.8.7-2010.01.tar.gz
    cp ruby-enterprise-1.8.7-2010.01.tar.gz ~/rpmbuild/SOURCES/

## Get Necessary System-specific Configs

    git clone git://github.com/causes/ree-centos.git
    cp ree-centos/spec/ruby-enterprise.spec ~/rpmbuild/SPECS/

## Build the RPM

    cd ~/rpmbuild/
    rpmbuild -ba SPECS/ruby-enterprise.spec

The resulting RPM will be:

    ~/rpmbuild/RPMS/x86_64/ruby-enterprise-1.8.7-2001.01.x86_64.rpm

## Credits

Based on the `ruby-enterprise.spec` file from Tim Harper found on [a Gist][gs].

 [gs]: http://gist.github.com/35409