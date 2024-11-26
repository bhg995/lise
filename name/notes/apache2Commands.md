

# Apache2 Bash Commands
F
## To download apache server

    $ sudo apt-get install apache2

## To check Apache version

    $ sudo apache2 -v

    Server version: Apache/2.4.62 (Raspbian)
    Server built:   2024-08-15T01:18:37

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
         Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
         Active: active (running) since Fri 2024-09-06 16:59:19 EEST; 2s ago
           Docs: https://httpd.apache.org/docs/2.4/
        Process: 22728 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)
       Main PID: 22732 (apache2)
          Tasks: 55 (limit: 3933)
            CPU: 93ms
         CGroup: /system.slice/apache2.service
                 ├─22732 /usr/sbin/apache2 -k start
                 ├─22733 /usr/sbin/apache2 -k start
                 └─22734 /usr/sbin/apache2 -k start

   I could see during the initiation an error: Could not reliably determine the server's fully qualified domain name

    Sep 06 16:59:19 eshu systemd[1]: Starting The Apache HTTP Server...
    Sep 06 16:59:19 eshu apachectl[22731]: AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName' directive globally to suppress this message
    Sep 06 16:59:19 eshu systemd[1]: Started The Apache HTTP Server.


  You can see it's active of line 3:

    active (running)

  The text is usually displayed in green

