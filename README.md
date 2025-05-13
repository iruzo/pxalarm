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
* * * * * * * command
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
┌───── min (00-59, * = any)
│ ┌─── hour (00-23)
│ │ ┌─ day-of-month (01-31)
│ │ │ ┌ month (01-12)
│ │ │ │ ┌ weekday (1-7, 1 = Monday)
│ │ │ │ │ ┌─[optional] year    (YYYY)
│ │ │ │ │ │ ┌─[optional] quarter (1-4)
│ │ │ │ │ │ │
* * * * *                 echo "tick every minute"
00 08 * * 1               printf '%s\n' "every Monday 08:00"
30 07 01 01 * 2026        echo "07:30 on 1 Jan 2026"
*  *  *  * * * 1          echo "every minute, but only in Q1"
```
