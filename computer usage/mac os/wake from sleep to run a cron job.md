---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
I was not understanding why my cron jobs weren't running on a server in the house, before I realized that the computer is asleep.

Some googling reveals that `pmset` is probably the tool I want - it lets you schedule a time to wake the computer, so you can pair it with cron to wake the computer and then run a task.

My updated crontab looks like:

```
# at 11 minutes past the hour, twice a day, sync NBA data to the nba_data repo
# at https://github.com/llimllib/nba_data
#
# for this job to run, you need the mac to wake up out of sleep; to do so you
# can use the `pmset` command:
#
# $ sudo pmset repeat wakeorpoweron MTWRFSU 05:10:00
# $ sudo pmset repeat wakeorpoweron MTWRFSU 17:10:00
11 5,17 * * * cd /Users/llimllib/code/nba_data && PATH=/Users/llimllib/.local/bin/:$PATH make > /Users/llimllib/.local/log/nba_log.log
```

After a few days, I discovered that only one of these was working, and that in fact you can only have one scheduled wakeup at a time (!) as far as I can tell.

To see what your current pmset schedule looks like, use:

```
$ pmset -g sched
Repeating power events:
  wakepoweron at 5:10AM every day
Scheduled power events:
 [0]  wake at 12/03/2022 18:21:05 by 'com.apple.alarm.user-visible-com.apple.CalendarNotification.EKTravelEngine.periodicRefreshTimer'
```
To solve this problem, I added a sudo crontab with `sudo crontab -e` that schedules the next wakeup shortly after the first wakeup should have occurred.

`sudo crontab -e` edits the root user's crontab, which seems wiser than trying to run sudo from inside cron.

```
# you can only use pmset for one time per day apparently, which is super
# irritating. It requires sudo so it has to live in here to re-run
#
# schedule the 17:10 wakeup
12 5 * * * pmset repeat wakeorpoweron MTWRFSU 17:10:00
# schedule the 5:10 wakeup
12 17 * * * pmset repeat wakeorpoweron MTWRFSU 15:10:00
```