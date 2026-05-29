# Network Monitor — Quick Start Guide

## 1. Install dependencies
```
pip install -r requirements.txt
```

## 2. Edit config.py
Replace these values with your own:
- IPS_LINES → your Line 1 and Line 2 IP addresses
- sender_email / sender_pass → your Gmail + App Password
- alert_to → your email address to receive alerts

## 3. Start the monitor
```
python scheduler.py
```

## 4. Open the dashboard
http://localhost:5000

---

## File Overview
| File            | Purpose                                          |
|-----------------|--------------------------------------------------|
| config.py       | All your settings (IPs, email, thresholds)       |
| database.py     | SQLite storage — auto-creates on first run       |
| monitor.py      | Ping, speed test, and status logic               |
| emailer.py      | Alert emails and daily summary report            |
| dashboard.py    | Flask web server and JSON API                    |
| scheduler.py    | Entry point — runs everything on a timer         |
| templates/index.html | Live dashboard UI with charts              |

## Gmail App Password Setup
1. Go to myaccount.google.com
2. Security → 2-Step Verification → App Passwords
3. Create a new app password (select "Mail" + "Windows Computer")
4. Copy the 16-character password into config.py → sender_pass

## Auto-start on Windows (Task Scheduler)
1. Open Task Scheduler → Create Basic Task
2. Trigger: At system startup
3. Action: Start a program
   - Program: C:\Python\python.exe
   - Arguments: C:\path\to\network_monitor\scheduler.py
   - Start in: C:\path\to\network_monitor

## Auto-start on Linux (cron)
```
crontab -e
@reboot cd /home/user/network_monitor && python scheduler.py >> logs/monitor.log 2>&1
```
