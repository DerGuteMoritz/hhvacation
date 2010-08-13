# hhvacation

This is a drop-in replacement for the apparently no longer maintained
hhvacation program included in the
[GNU Hosting Helper](http://hostingsoftware.net/) suite. It only
operates on so called "virtual" vacation responds (i.e. they are kept
in a MySQL database).

## Usage

Change your Postfix' master.cf to include a line like:
 
    vacation  unix  -       n       n       -       -       pipe flags=DRhu user=vacation argv=/usr/bin/hhvacation-ruby /etc/hhvacation.yml
   
The actual settings may vary depending on your setup. The argument
passed to the hhvacation-ruby program which is installed by this gem
must point to a YAML config file which contains the database
connection information, for example:

    host: localhost
    user: root
    password: s3cr3t
    database: mail

## Copyright

Copyright (c) 2010 Moritz Heidkamp. See LICENSE for details.
