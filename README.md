# ![N|Solid](https://raw.githubusercontent.com/killown/gnome-timer/master/Images/gnome-timer.svg)  GNOME Timer

GNOME timer is a front-end for systemd timers which can be used for an alarm clock or reminder
![N|Solid](https://raw.githubusercontent.com/killown/gnome-timer/master/Images/gnome-timer.png)
what does it do?
  - use systemd as back-end
  - enable, disable, remove and edit services
  - timers run independently from GNOME timer
  - persistent, which will trigger the associated unit when the timer becomes active if it would have been triggered during the period in which the timer was inactive.

for more help visit [Freedesktop](https://www.freedesktop.org/software/systemd/man/systemd.time.html) or see Below


# Help
# Calendar Events

- Calendar events may be used to refer to one or more points in time in a single expression. They form a superset of the absolute timestamps.

      Thu,Fri 2017-*-1,5 11:12:13
The above refers to 11:12:13 of the first or fifth day of any month of the year 2012, but only if that day is a Thursday or Friday.

- The weekday specification is optional. If specified, it should consist of one or more English language weekday names, either in the abbreviated (Wed) or non-abbreviated (Wednesday) form (case does not matter), separated by commas. Specifying two weekdays separated by ".." refers to a range of continuous weekdays. "," and ".." may be combined freely.

- In the date and time specifications, any component may be specified as "*" in which case any value will match. Alternatively, each component can be specified as a list of values separated by commas. Values may be suffixed with "/" and a repetition value, which indicates that the value itself and the value plus all multiples of the repetition value are matched. Two values separated by ".." may be used to indicate a range of values; ranges may also be followed with "/" and a repetition value.

- A date specification may use "~" to indicate the last day(s) in a month. For example, "*-02~03" means "the third last day in February," and "Mon *-05~07/1" means "the last Monday in May."

- The seconds component may contain decimal fractions both in the value and the repetition. All fractions are rounded to 6 decimal places.

- Either time or date specification may be omitted, in which case the current day and 00:00:00 is implied, respectively. If the second component is not specified, ":00" is assumed.

- A timezone specification is not expected, unless it is given as the literal string "UTC", or the local timezone, similar to the supported syntax of timestamps (see above). Non-local timezones except for UTC are not supported.

# The special expressions
    "minutely", "hourly", "daily", "monthly", "weekly", "yearly", "quarterly", "semiannually"
    which refer to "*-*-* *:*:00", "*-*-* *:00:00", "*-*-* 00:00:00", "*-*-01 00:00:00", "Mon *-*-* 00:00:00", "*-01-01 00:00:00", "*-01,04,07,10-01 00:00:00" and "*-01,07-01 00:00:00", respectively.

 # Examples for valid timestamps and their normalized form

    Sat,Thu,Mon..Wed,Sat..Sun → Mon..Thu,Sat,Sun *-*-* 00:00:00
    Mon,Sun 12-*-* 2,1:23 → Mon,Sun 2012-*-* 01,02:23:00
    Wed *-1 → Wed *-*-01 00:00:00
    Wed..Wed,Wed *-1 → Wed *-*-01 00:00:00
    Wed, 17:48 → Wed *-*-* 17:48:00
    Wed..Sat,Tue 12-10-15 1:2:3 → Tue..Sat 2012-10-15 01:02:03
    *-*-7 0:0:0 → *-*-07 00:00:00
    10-15 → *-10-15 00:00:00
    monday *-12-* 17:00 → Mon *-12-* 17:00:00
    Mon,Fri *-*-3,1,2 *:30:45 → Mon,Fri *-*-01,02,03 *:30:45
    12,14,13,12:20,10,30 → *-*-* 12,13,14:10,20,30:00
    12..14:10,20,30 → *-*-* 12..14:10,20,30:00
    mon,fri *-1/2-1,3 *:30:45 → Mon,Fri *-01/2-01,03 *:30:45
    03-05 08:05:40 → *-03-05 08:05:40
    08:05:40 → *-*-* 08:05:40
    05:40 → *-*-* 05:40:00
    Sat,Sun 12-05 08:05:40 → Sat,Sun *-12-05 08:05:40
    Sat,Sun 08:05:40 → Sat,Sun *-*-* 08:05:40
    2003-03-05 05:40 → 2003-03-05 05:40:00
    05:40:23.4200004/3.1700005 → *-*-* 05:40:23.420000/3.170001
    2003-02..04-05 → 2003-02..04-05 00:00:00
    2003-03-05 05:40 UTC → 2003-03-05 05:40:00 UTC
    2003-03-05 → 2003-03-05 00:00:00
    03-05 → *-03-05 00:00:00
    hourly → *-*-* *:00:00
    daily → *-*-* 00:00:00
    daily UTC → *-*-* 00:00:00 UTC
    monthly → *-*-01 00:00:00
    weekly → Mon *-*-* 00:00:00
    yearly → *-01-01 00:00:00
    annually → *-01-01 00:00:00
    *:2/3 → *-*-* *:02/3:00

# timestamps for restart mode
- the restart mode refers to OnUnitActiveSec, the service will restart every N time

        2 h 2hours  48hr  1y 12month  55s500ms 300ms20s 5day

# issues
- services doesn't start after boot?

          sudo loginctl enable-linger "$USER"
what is linger?
- Enable/disable user lingering for one or more users. If enabled for a specific user, a user manager is spawned for the user at boot and kept around after logouts. This allows users who are not logged in to run long-running services. Takes one or more user names or numeric UIDs as argument. If no argument is specified, enables/disables lingering for the user of the session of the caller.
