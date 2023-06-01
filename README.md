# description

`pxalarm` is a simple POSIX sh script that periodically checks a config file and executes commands at specified times.

# usage

1. Create a config file at `$XDG_CONFIG_HOME/pxalarm/config` or at `$HOME/.config/pxalarm/config`.
2. Set your alarms in that file with the following format:
```
[YYYY-MM-DD HH:mm] command
```
3. Launch the program using the following command. The program will run unattended in the background and check the config file every minute.
```sh
pxalarm
```
**Note**: The program will keep running in the background and checking the config file every minute until stopped.

# config file

Time can be replaced with * to not check that part. The following formats are supported:
```
[YYYY-MM-DD HH:mm] command           # command will be executed at that specific moment
[*-MM-DD HH:mm] command              # command will be executed every year at that specific moment.
[YYYY-*-DD HH:mm] command            # command will be executed every month of YYYY at that specific moment.
[YYYY-MM-* HH:mm] command            # command will be executed every day of that month at that specific moment.
[YYYY-MM-DD *:mm] command            # command will be executed every hour at minute mm of that day.
[YYYY-MM-DD HH:*] command            # command will be executed every minute of that hour.
[*-*-* *:*] command                  # command will always be executed every minute.
```
