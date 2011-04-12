# A Recipe for a Ruby Enterprise Edition RPM on CentOS

Perform the following on a build box as root.

## Create an RPM Build Environment

    yum install rpmdevtools
    rpmdev-setuptree

## Install Prerequisites for RPM Creation

    yum groupinstall 'Development Tools'
    yum install readline-devel ncurses-devel gdbm-devel db4-devel

## Download REE

    cd /tmp
    wget http://rubyenterpriseedition.googlecode.com/files/ruby-enterprise-1.8.7-2011.03.tar.gz
    cp ruby-enterprise-1.8.7-2011.03.tar.gz ~/rpmbuild/SOURCES/

## Get Necessary System-specific Configs

    git clone git://github.com/esminc/ree-centos.git
    cp ree-centos/spec/ruby-enterprise.spec ~/rpmbuild/SPECS/

## Build the RPM

    cd ~/rpmbuild/
    # the QA_RPATHS var tells the builder to ignore file path errors
    QA_RPATHS=$[ 0x0002 ] rpmbuild -ba SPECS/ruby-enterprise.spec

The resulting RPMs (one for REE, one for REE's Rubygems) will be:

    ~/rpmbuild/RPMS/x86_64/ruby-enterprise-1.8.7-4.x86_64.rpm
    ~/rpmbuild/RPMS/x86_64/ruby-enterprise-rubygems-1.5.2-4.x86_64.rpm

## Credits

Based on the `ruby-enterprise.spec` file from Adam Vollrath, found
on [GitHub as a Gist][gs].

 [gs]: http://gist.github.com/108940
