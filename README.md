# hhvacation

This is a drop-in replacement for the apparently no longer maintained
hhvacation program included in the
[GNU Hosting Helper](http://hostingsoftware.net/) suite. It only
operates on so called "virtual" vacation responders (i.e. they are
kept in a MySQL database).

## Usage

Change your Postfix' master.cf to include a line like:
 
    vacation  unix  -       n       n       -       -       pipe flags=DRhu user=vacation argv=/usr/bin/hhvacation-ruby /etc/hhvacation.yml
   
The actual settings may vary depending on your setup. The argument
passed to the hhvacation-ruby program which is installed by this gem
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
as settings for the method.
      
## Copyright

Copyright (c) 2010 Moritz Heidkamp. See LICENSE for details.
