https://perlmaven.com/how-to-build-perl-from-source-code

```
# yum -y install make
# yum -y install gcc

# wget http://www.cpan.org/src/5.0/perl-5.20.1.tar.gz
# tar -xzf perl-5.20.1.tar.gz
# cd perl-5.20.1
# ./Configure -des -Dprefix=$HOME/localperl
# make
# make test
# make install
```

This will install perl in the directory $HOME/localperl. This means if you'd like to run this perl you'll need to run

$HOME/localperl/bin/perl

(for example $HOME/localperl/bin/perl -v)

Alternatively, you can change the PATH environment variable:
```
# export PATH=$HOME/localperl/bin:$PATH
```
and then you can type perl -v.

If you want to make this change persistent, add this line to $HOME/.bashrc
