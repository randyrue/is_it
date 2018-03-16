# is_it
wrapper/qualifier for crontab entries, tests for date conditions like "first Monday" and returns True(0) or False(1) exit status\
multiple conditions are considered an OR test: if any are true, is_it will return True(0)

embed is_it in your crontab entry e.g.:\
1   0  *  *   *   [ "is_it -c f -d mon" ] && logger "It's 12:01AM on the first Monday of the month"\
(is_it must be in the path or provide the full path in the crontab line)

Usage: is_it -c count -w weekday [-v] [-t YYYYMMDD] [-h]\
Test whether this is the "c'th" weekday "w" of the month.

   -c, --count     recurrence count of the month e.g. "f" or "first", "l" or "last", 1,2,3,4,5\
                   multiple entries can be listed as a sequential range e.g. 1-3 or a non-spaced comma separated list e.g. 2,4\
   -w, --weekday   day of the week e.g. 0 to 6 (Sunday to Saturday), "Mo," "Mon," "Monday" (case insensitive)\
                   multiple entries can be listed as a sequential range e.g. tue-thu or a non-spaced comma separated list e.g. mo,we\
   -v, --verbose   echos output e.g "it is not the last thursday of the month" (default is silent)\
   -t, --test      pretends today is YYYY-MM-DD for testing purposes\
   -h, --help      displays this help and exit

Exit status:\
        0       date test is positive\
        1       date test is negative or is_it otherwise failed\


  examples:\
    is_it -c first -d mon       # first Monday of the month\
    is_it -c 1,3  -d Saturday   # first or third Saturday of the month\
    is_it -c l  -d fr           # last Friday of the month

Use cron to control monthly recurrence. For example, to run a task on the last Friday of each quarter:\
59   23  *  3,6,9,12   *   [ "is_it -c l -d fri" ] && logger "It's 11:59PM on the last Friday of the quarter"
