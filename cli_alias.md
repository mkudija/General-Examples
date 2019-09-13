# cli alias

A cli alias allows you to set a "shortcut" for a terminal command.

From here: [Terminal 101: Creating Aliases for Commands](https://www.techradar.com/how-to/computing/apple/terminal-101-creating-aliases-for-commands-1305638)
- Open `~/.bash_profile`
  - `nano /.bash_profile`
  - or just open it in text editor: `touch ~/.bash_profile; open ~/.bash_profile` (from [here](https://stackoverflow.com/questions/30461201/how-do-i-edit-path-bash-profile-on-osx))
- Add your command:
  - i.e. `alias readings='cd Documents/GitHub/USCCB_daily_readings/; python todays_readings.py'`
  - save
