# Cron
## Info
To see your crontabs:
```
crontab -l
```

To see further options:
```
man crontab
```

## Scheduling 

Every hour:
```
crontab 0 * * * * /Users/matthewkudija/anaconda3/bin/python /path/to/script
```

Every minute:
```
crontab * * * * * /Users/matthewkudija/anaconda3/bin/python /Users/matthewkudija/Documents/GitHub/MILE_Data/MILE_file_copy.py
```

Every day at 9:15:
```
crontab 15 09 * * * /Users/matthewkudija/anaconda3/bin/python /path/to/script
```

To add a new one (think this works):
- Open editor: `crontab -e`
- It opens command mode, so type `i` to insert or `a` to append
- Paste `15 09 * * * /Users/matthewkudija/anaconda3/bin/python /Users/matthewkudija/Documents/GitHub/MILE_Data/MILE_file_copy.py`
- Press `esc` to go back to command mode
- Press `Shift+ZZ` to save and close
 

Note: 
- see vi editor info [here](https://kb.iu.edu/d/adxz)
- [Crontab reference](http://www.adminschoice.com/crontab-quick-reference)
