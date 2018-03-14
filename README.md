# is_it
wrapper/qualifier for crontab entries, tests for date conditions like "first Monday" and returns exit status

embed is_it in your crontab entry e.g.:\
1   0  *  *   *   [ "is_it -c f -d mon" ] && logger "It's 12:01AM on the first Monday of the month"\
(is_it must be in the path or provide the full path in the crontab line)

Usage: is_it -c count -d day [-v]\
  -c, --count   recurrence count of the month e.g. "f" or "first", "l" or "last", 1,2,3,4,5\
                multiple entries can be listed as a sequential range e.g. 1-3 or a non-spaced comma separated list e.g. 2,4\
  -d, --day     day of the month e.g. 1 to 7 (Sunday to Monday), "Mo," "Mon," "Monday" (case insensitive)\
                multiple entries can be listed as a sequential range e.g. tue-thu or a non-spaced comma separated list e.g. mo,we\
  -v, --verbose STDOUT notice e.g. "it is not the last thursday of the month" (default is silent)

  examples:\
    is_it -c first -d mon       # first Monday of the month\
    is_it -c 1,3  -d Saturday   # first and third Saturday of the month\
    is_it -c l  -d fr           # last Friday of the month

Use cron to control monthly recurrence. For example, to run a task on the last Friday of each quarter:\
59   23  *  3,6,9,12   *   [ "is_it -c l -d fri" ] && logger "It's 11:59PM on the last Friday of the quarter"
