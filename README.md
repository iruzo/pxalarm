# description

`pxalarm` is a simple POSIX sh script that periodically checks a config file and
executes commands at specified times.

# installation

- Alpine
```sh
apk add pxalarm
```
- Others
```sh
curl https://raw.githubusercontent.com/iruzo/pxalarm/main/pxalarm -o pxalarm
```

# usage

1. Create a config file at `$XDG_CONFIG_HOME/pxalarm/config` or at `$HOME/.config/pxalarm/config`.

2. Set your alarms in that file with the following format:

```
[YYYY-MM-DD HH:mm] command
```

3. Launch the program with the following command. It will check the config
file every minute. The `-d` command-line argument will cause the program to run
unattended in the background as a daemon. You can also omit `-d` to run it in
the foreground, if you want to see the logs for example.

```sh
./pxalarm -d
```

**Note**: The program will continue to run in the background (if the `-d` flag
was passed) and check the config file every minute until stopped. You can stop
it at any time by running `pkill pxalarm`, or by pressing Ctrl-C if it is
running in the foreground.

# config file

Time can be replaced with * to match any time. The following formats are
supported:
```
[YYYY-MM-DD HH:mm] command           # command will be executed at that specific moment
[*-MM-DD HH:mm] command              # command will be executed every year at that specific moment.
[YYYY-*-DD HH:mm] command            # command will be executed every month of YYYY at that specific moment.
[YYYY-MM-* HH:mm] command            # command will be executed every day of that month at that specific moment.
[YYYY-MM-DD *:mm] command            # command will be executed every hour at minute mm of that day.
[YYYY-MM-DD HH:*] command            # command will be executed every minute of that hour.
[*-*-* *:*] command                  # command will always be executed every minute.
```
