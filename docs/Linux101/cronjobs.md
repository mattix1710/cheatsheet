---
tags:
    - linux
    - cron jobs
---

## Quick intro

The Cron daemon is a built-in Linux utility that reads the **==crontab==** (cron table) file and executes commands and scripts at predefined times and intervals.

## Basic Crontab syntax

The syntax of a cron job in a crontab file must use the following format:
```
MIN HOUR DOM MON DOW CMD
```

| Field | Meaning                            |
|------:|------------------------------------|
|   MIN | minutes                            |
|  HOUR | hours                              |
|   DOM | day of the month                   |
|   MON | month                              |
|   DOW | day of the week                    |
|   CMD | path to a script or system command |

!!! example
    Writing such line to a crontab file will resolve in executing the script on January 1st at 9 AM:
    ``` bash
    0 9 1 1 * /path/to/your_script.sh
    ```

The asterisk (`*`) operator instructs Cron to execute the job regardless of which day of the week falls on January 1st.

### Cron Job Time Format

|           Field            |   Possible values   |  Syntax   | Description                                                                                                                                   |
|:--------------------------:|:-------------------:|:---------:|-----------------------------------------------------------------------------------------------------------------------------------------------|
|      **Minute (MIN)**      |       0 - 59        | 7 * * * * | The cron job is initiated every time the system clock shows 7 in the minute's position.                                                       |
|      **Hour (HOUR)**       |       0 - 23        | 0 7 * * * | The cron job runs any time the system clock shows 7 AM (7 PM would be coded as 19).                                                           |
| **Day of the Month (DOM)** |       1 - 31        | 0 0 7 * * | The day of the month is 7, which means that the job runs every 7th day of the month.                                                          |
|      **Month (MON)**       | 1 - 12 or JAN - DEC | 0 0 0 7 * | The numerical month is 7, which determines that the job runs only in July. The *Month* field value can be a number or the month abbreviation. |
| **Day of the Week (DOW)**  | 0 - 7 or SUN - SAT  | 0 0 * * 7 | 7 in the current position means that the job would only run on Sundays. The *Day of the Week* field can be a number or the day abbreviation.    |

### Using operators

| Operator | Description | Example |
|:--:|---|--|
| Asterisk<br>**(*)** | Substitutes all possible values for a time field | Used in the day field, it indicates that the task should be executed every day |
| Comma<br>**(,)** | Used to separate individual values within a field | Using `20,40` in the minute field runs the task at 20 and 40 minutes past the hour |
| Dash<br>**(-)** | Defines a range of values in a single field | Entering `15-18` in the minute field instructs Cron to run a task every minute between and including 15th and 18th minute |
| Forward slash **(/)** | Divides a field value into increments | `*/30` in the minute field means that the task is run every 30 minutes |

## Creating cron job

At first, open the crontab configuration file:
``` bash
crontab -e
```

To schedule a job for a different user, add the `-u` option and the username:
``` bash
crontab -u <username> -e
```

At the end of the file append a line containing a cron expression and the path to a script, e.g.:
``` bash
15 22 * * * /path/to/script.sh
```
Which will result in running the selected script *every day at 22:15*.

### Sources

- <https://phoenixnap.com/kb/set-up-cron-job-linux>