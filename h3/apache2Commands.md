

# Apache2 Bash Commands

## To download apache server

    $ sudo apt-get install apache2

## To check Apache version

    $ sudo apache2 -v

    $ sudo apache2 -V
    
    output -->  Server version: Apache/x.x.xx (LinuxDistro)
                Server built:   20XX-0X-0XTXX:XX:XX

## To start Apache Server. Second option, if running older Linux without `systemd`

    $ sudo systemctl start apache2
    $ sudo service apache2 start

## To set it to start on boot

    $ sudo systemctl enable apache2

## To stop Apache Server 

    $ sudo service apache2 stop
    $ sudo service apache2 stop

## To restart Apache Server

    $ sudo systemctl restart apache2
    $ sudo service apache2 restart

## To reload Apache server

    $ sudo systemctl reload apache2
    $ sudo service apache2 reload
    
## To test Apache configuration

    $ sudo apachectl -t
    Output --> Syntax OK, else detailed message of error

## To test if server is running website

    $ curl http://localhost

## To view Apache status

    $ sudo systemctl status apache2

### The output should look like:

    ● apache2.service - The Apache HTTP Server
       Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: 
      Drop-In: /lib/systemd/system/apache2.service.d
           └─apache2-systemd.conf
       Active: active (running) since Wed 2019-05-29 21:16:55 UTC; 6s ago
      Process: 938 ExecStop=/usr/sbin/apachectl stop (code=exited, status=0/SUCCESS)
      Process: 956 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCES
     Main PID: 997 (apache2)
    Tasks: 55 (limit: 1152)
       CGroup: /system.slice/apache2.service
               ├─ 997 /usr/sbin/apache2 -k start
               ├─ 999 /usr/sbin/apache2 -k start
               └─1000 /usr/sbin/apache2 -k start

### You can see it's active of line 5:

    active (running)

### The text is usually displayed in green

