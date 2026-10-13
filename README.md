# Price Tracker

## What it does
This price tracker scrapes products along with their respective brands and saves the data in a well-organized CSV file. It automatically sends an alert email to the user's Gmail inbox whenever a product's price drops. It is designed to be run every sunday via task scheduling. see Scheduling set-up below:

### Scheduling (Windows)

To run the tracker automatically every Sunday:

1. Open **Task Scheduler** → **Create Basic Task**.
2. Trigger: **Weekly**, Sunday, at your preferred time.
3. Action: **Start a program**, then fill in:
   - **Program/script:** full path to `python.exe`
   - **Add arguments:** `shopping`
   - **Start in:** full path to the project folder (no quotes)
4. After finishing, open the task's **Properties**:
   - **General:** choose "Run whether user is logged on or not"
   - **Settings:** tick "Run task as soon as possible after a scheduled start is missed"
   - **Conditions:** untick the "AC power" options if you're on a laptop
5. Right-click the task → **Run** to test, then check `tracker.log`.

## Prerequisites
Python 3.11+ (tested on Python 3.14.4)

## Set-Up

1. Clone the repository
```
git clone <repository-url>
cd <repository-name>
```

2. Create a virtual environment
```
python -m venv venv
```
Activating it:
    
windows: 
```
venv\Scripts\activate
```
    
linux/macOS: 
```
source venv/bin/activate
```

3. Install dependencies:
```
pip install -r requirements.txt
```

4. Configure environment variables
copy the example file:
windows: 
```
copy .env.example .env
```
linux/macOS:
```
cp .env.example .env
```
Then fill it with your own credentials.
[NOTE: For App Password see the step 5]

5. How to get your email app password
    1. Go to this website:
    https://myaccount.google.com/apppasswords
    2. Sign in the gmail account whose email you entered in your .env file
    3. Create a name for that app password and enter. 
    4. 16 character of password will appear copy and save it somewhere safe. 
    [NOTE: App Password will appear only once make sure to copy it.]

## Usage
To start the project:
1. Open terminal in the project folder.
2. Run:

```
python shopping.py
```
### Expected output:
When you run first time you should see a line "New csv file is created!"

### Where the file is saved (Products.csv)
- Open the project folder (the same folder as the script).
- Locate Products.csv.
- Double-click the file to open it.
- You can open it with Excel, WPS Spreadsheet, Google Sheets, LibreOffice Calc, or any application that supports CSV files.

## Configuration
When there is any price drop in any of the products it will trigger an email in your Gmail box. It currently traces every brand of automationexercise.com. An email alert will only appear if the current price of any product is lower than previous saved price.

[NOTICE: Alerts are sent to the same address you set in .env, so check that inbox. Sign in to the exact Gmail account.]