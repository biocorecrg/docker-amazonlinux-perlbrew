FROM amazonlinux:2

ARG PERLBREW_ROOT=/usr/local/perl
ARG PERL_VERSION=5.32.1
# Enable perl build options. Example: --build-arg PERL_BUILD="--thread --debug"
ARG PERL_BUILD=--thread

# Base Perl and builddep
RUN yum update -y
RUN yum install -y perl yum-utils
RUN yum-builddep -y perl
RUN yum install -y bzip2 zip procps
RUN yum groupinstall -y 'Development Tools'

RUN mkdir -p $PERLBREW_ROOT

RUN bash -c '\curl -L https://install.perlbrew.pl | bash'

ENV PATH $PERLBREW_ROOT/bin:$PATH
ENV PERLBREW_PATH $PERLBREW_ROOT/bin

RUN yum install -y perl-ExtUtils-MakeMaker perl-CPAN perl-Module-Pluggable
ENV PERL_MM_USE_DEFAULT=1
RUN cpan -i Test::More Devel::PatchPerl; exit 0 # Hack to make it work
RUN perlbrew install-patchperl
RUN perlbrew --notest install $PERL_BUILD perl-$PERL_VERSION
RUN perlbrew install-cpanm
RUN bash -c 'source $PERLBREW_ROOT/etc/bashrc'

ENV PERLBREW_ROOT $PERLBREW_ROOT
ENV PATH $PERLBREW_ROOT/perls/perl-$PERL_VERSION/bin:$PATH
ENV PERLBREW_PERL perl-$PERL_VERSION
ENV PERLBREW_MANPATH $PERLBREW_ROOT/perls/perl-$PERL_VERSION/man
ENV PERLBREW_SKIP_INIT 1

RUN ln -s $PERLBREW_ROOT/perls/perl-$PERL_VERSION/bin/perl /usr/local/bin/perl

# Clean cache
RUN yum clean all

# Workdir place
RUN mkdir -p /project
WORKDIR /project

#ENTRYPOINT ["./entrypoint.sh"]

