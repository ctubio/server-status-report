# Overview

Oftentimes you might be interested in the status of your server without having to actually sit there staring at a terminal window. Wouldn't it be nice if you could run a script to email you information about the state of your server? Well, that's exactly what this script does. It outputs HTML 4.01 Strict compliant content containing information on your server including:

* load average
* memory usage
* open network connections
* top 10 memory processes
* top 10 CPU processes
* netstat output
* top snapshot of all running processes

This script was primarily written for and tested on DreamHost Private Servers.

# Installation

To install this script, the first thing you want to do is download a copy of the script to use. To do that, SSH to your server under the user you want to run the script as and run this command:

    git clone ssh://git@github.com/ctubio/server-status-report
Alternatively see the comments inside [server-status-report.sh](server-status-report.sh).

The script itself is written in Ruby to take advantage of the {ERB templating system}[http://ruby-doc.org/stdlib/libdoc/erb/rdoc/classes/ERB.html] to produce the HTML content.

Once you've downloaded the script successfully, you need to make sure that the *mailx* package is installed on your server. To find out, run this command:

    dpkg -l | grep mailx

If you see output like this:

    ii  mailx                     8.1.2-0.20050715cvs-1        A simple mail user agent

then that means it's installed. If instead you see output like this:

    rc  mailx                     8.1.2-0.20050715cvs-1        A simple mail user agent

then that means you need to install it. To do so, login with an admin with sudo privileges and run the following command:

    sudo apt-get install mailx

Now you're ready to create a cron job to send yourself your status report. The command you want to run is as follows:

    /usr/bin/ruby /path/to/script/status.rb | /usr/bin/mail -a "Content-type: text/html;" -s "Status Report: $HOSTNAME" "some@address.com"

You can change the subject to whatever you want and just replace <b>some@address.com</b> with the address you want the email sent to. If you want to CC the email to more email addresses you can use the <b>-c</b> flag and pass it a comma separated list of email addresses. Running it once per hour is probably not a bad idea, but you can run it as frequently or infrequently as you like!

# Conclusion

If you set everything up properly, then you should start getting emails that look roughly like this:

![](http://img.skitch.com/20100214-kcdm52ti59m117hewre9pue72x.jpg)

Keep in mind that this script will likely be updated as time progresses. So, if this stops working for you, be sure to check back to see if the script has been updated.

# Copyright

Copyright (c) 2012 Joel Watson. See LICENSE for details.
