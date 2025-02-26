# Correct the clock

- **Check all the timezones**
```bash
$ timedatectl
```
- **Set the timezone to a city**
```bash
$ timedatectl set-timezone <Continent>/<City>
```

Might need to synchronize the local system clock with a remote Network Time Protocol (NTP)

- **So, install `systemd.timesyncd`**
```bash
$ sudo apt install system.timesyncd
```
- **Enable/Start it**
```bash
$ sudo systemctl enable systemd-timesyncd
$ sudo systemctl start systemd-timesyncd

$ sudo systemctl status systemd-timesyncd
```

- **Enable the synchronization**
```bash
$ sudo timedatectl set-ntp true
```

Time & date linux
- https://timetoolsltd.com/ntp/how-to-install-and-configure-ntp-on-linux/
