# Usage
## Pre-requisites
Perl 5 must be installed.

## Cloning
Copy the file service to $HOME/bin (or whereever you prefer)

## Create a config file
File: $HOME/.service_config
```properties
# Enable debug log or not
debug=0

# All services
service.list=blah

# Service for blah
# If blah is not running, run this script to start the service
service.blah.execStart=/home/wushilin/bin/test1/start.sh

# Run this script to detect if blah is running (should output PIDs detected)
service.blah.detectPid=/home/wushilin/bin/test1/detect.sh
```
## Enable in cron

```bash
$ crontab -e
* * * * * (cd /home/user01/bin; ./service >> service.log)
```

# Behavior
Everytime the service script is running, it will check if the services are running by executing detectPid script.

If a service is not running, then execStart is executed to start the service.

# Example
see `example/test1/detect.sh` and `example/test1/start.sh`

They are simple script that demonstrates:
`start.sh` -> start a service that sleeps for 75 seconds
`detect.sh` -> detect if a sleep service is already running by using PS.

So every 2 minutes a new sleep service will be launched by `start.sh` as `detect.sh` will return false after 75 seconds.
