# Logging

gmin has built-in logging features to provide auditing and debugging information. Logging is always on and cannot be turned off completely, although there are logging levels that can be configured with the `--log-level` flag when a command is run. So `gmin ls groups --log-level debug` would run the given list command with a log level of debug.

## Log Levels

Valid log levels (in order of most to least verbose) are:

* debug
* info
* warn
* error

The default log level is info. The log level setting means that log messages for that and higher settings will be written to the current log. For example, if log level is set to info then info, warn and error messages will be written to the log but no debug messages.

## Log Path

The log path is the path to the directory/folder where logs will be written. This can be set by running `gmin init`, `gmin set config -l <path>` or by setting a GMIN_LOGPATH environment variable. The default path is the current user's home directory.

## Log Rotation Count

The log rotation count specifies the maximum number of log files that will kept before older files start being purged to make way for newer ones. This can be set by running `gmin init`, `gmin set config -r <count>` or by setting the GMIN_LOGROTATIONCOUNT environment variable. The default count is 7.

## Log Rotation Time

The log rotation time specifies the amount of time (in seconds) that needs to have elapsed before a new log file is written. This can be set by running `gmin init`, `gmin set config -t <number of seconds>` or by setting the GMIN_LOGROTATIONTIME environment variable. The default time is 86400 which equals 24 hours.

## Log File Format

The log files are named according to the following scheme:

gmin_log.YYYYmmDDHHMMSS where YYYY is the current year, mm is the month, DD is the day, HH is the hour (24 hour clock), MM are the minutes and SS are the seconds.

The actual values in the date/time part of the log file name depend on the value used for log rotation time. For example, if the default log rotation time of 86400 is used then the log file names will look like this:

gmin_log.YYYYmmDD000000 where the time portion of the name is set to zeroes. This is because the log rotation time will result in one log file being written per day which makes the time in the log file name unnecessary.

Information is written to log files in JSON format. An example entry might look like this:

`{"level":"info","ts":"2020-10-29T13:36:56.419Z","msg":"User Information","gmin admin":"admin@mycompany.com",`
`"Username":"auser","Hostname":"cdt450", "IP Address":"192.168.2.38:58705","command":"list usr "}`