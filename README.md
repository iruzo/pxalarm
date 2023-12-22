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

1. Create a config file or configure a custom path for your config file:
- Default config file paths are `$XDG_CONFIG_HOME/pxalarm/config` and `$HOME/.config/pxalarm/config`.
- You can set a custom path with `-c` like so:
```
./pxalarm -c '/your/new/config/file'
```

2. Set your alarms in that file with the following format:

```
[YYYY-mm-DD HH:MM u q] command
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
# YYYY: 4-digit year
# mm: 2-digit month
# DD: 2-digit day
# HH: 2-digit hour (24-hour format)
# MM: 2-digit minute
# u: weekday (1 for Monday, 2 for Tuesday, ..., 7 for Sunday)
# q: quarter of year (1, 2, 3, 4)

[YYYY-mm-DD HH:MM u q] command            # command will be executed at that specific moment if that day is u and quarter of year is q.
[*-mm-DD HH:MM u q] command               # command will be executed every year at that specific moment if that day is u and quarter of year is q.
[YYYY-*-DD HH:MM u q] command             # command will be executed every month of YYYY at that specific moment if that day is u and quarter of year is q.
[YYYY-mm-* HH:MM u q] command             # command will be executed every day of that month at that specific moment if that day is u and quarter of year is q.
[YYYY-mm-DD *:MM u q] command             # command will be executed every hour at minute mm of that day if that day is u and quarter of year is q.
[YYYY-mm-DD HH:* u q] command             # command will be executed every minute of that hour on day u and quarter of year q.
[YYYY-mm-DD HH:MM * q] command            # command will be executed at that specific moment every day on the quarter q of the year.
[YYYY-mm-DD HH:MM u *] command            # command will be executed at that specific moment on day u, no matter the quarter of year.
[*-*-* *:* * *] command                   # command will always be executed every minute.
```
