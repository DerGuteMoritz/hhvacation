# hhvacation

This is a drop-in replacement for the apparently no longer maintained
hhvacation program included in the
[GNU Hosting Helper](http://hostingsoftware.net/) suite.

## Differences To The Original Version

This implementation of `hhvacation` only operates on so called
"virtual" vacation responses (i.e. those which are kept in a MySQL
database). 

Another difference is that it not only checks the `To` header for
vacation responses but also the `Cc` and `Bcc` headers.

## Warning

Since this program is written in Ruby (i.e. its execution is
relatively resource intensive) and Postfix will call it for every mail
it delivers, it should not be used on high-volume servers. In any case
you should definitely keep an eye on the server load and look for
better alternatives. This program is merely a drop-in replacement for
existing setups which used the original `hhvacation` Perl script
included in `gnuhh` which depends on a deprecated MySQL library and
thus cannot be run without problems on more recent versions of Perl.

Also note that due to the high probability that this program is mostly
used with MySQL databases using the MyISAM storage engine it makes no
use of database transactions. This *may* result in vacation responses
being sent multiple times to the same recipient.

## Installation

The program is available on `rubygems.org` thus 

    gem install hhvacation
    
should suffice to install it.


## Usage

Change your Postfix' `master.cf` to include a line like:
 
    vacation  unix  -       n       n       -       -       pipe flags=DRhu user=vacation argv=/usr/bin/hhvacation-ruby /etc/hhvacation.yml
   
The actual settings may vary depending on your setup. The argument
passed to the `hhvacation-ruby` program which is provided by this gem
must point to a YAML formatted config file. It must contain the
database connection information (see below for an example). Unless
configured otherwise, mails are delivered via the default method of
the `mail` gem (SMTP on localhost port 25 for version 2.2.5).

## Example config

    database:
      host: localhost
      user: root
      password: s3cr3t
      database: mail
      
    mail:
      method: sendmail
      location: /usr/local/bin/sendmail
      

The `method` setting in the `mail` section may contain whatever method
is available in the `mail` gem. All further keys are directly passed
as settings for the selected method.
      
## Copyright

Copyright (c) 2010 Moritz Heidkamp and Christof Spies. See LICENSE for details.
