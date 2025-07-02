This repository contains 2 scripts: tr2pdt and broker2pdt 

# broker2pdt
This script is under construction and is not stable at this time

# tr2pdt
This script can import broker events Trade Republic and export them to an xlsx file in the format of Portfolio Dividend Tracker (PDT)

## Why I created this script
I am a very happy user of Portfolio Dividend Tracker. Unfortunately, there's no officially available automatic export from Trade Republic to PDT. This is because Trade Republic still doesn’t offer a decent export function. At the moment, the only option is to manually download each transaction and dividend statement as a PDF. Painful. Since I use the auto-invest feature in Trade Republic — buying 11 fractional shares twice a month — I quickly realized that manually entering 22 transactions every month wasn’t going to happen. I'm way too lazy for that. So I wrote a script.

## How to use it
_Basic command line knowledge assumed._

1. Download the script from GitHub: [https://github.com/jzp74/broker2pdt](https://github.com/jzp74/broker2pdt)
2. Run the script

~~~bash
usage: tr2pdt [-h] [--info] [-d DAYS] [-f FOLDER] phone_no pin

Get TradeRepublic transactions from the last X days and store them in a file

positional arguments:
  phone_no              TradeRepublic phone number (international format)
  pin                   TradeRepublic pin

options:
  -h, --help            show this help message and exit
  --info                show extra info during process
  -d DAYS, --days DAYS  number of last days to include in the file (1 to max 100)
  -f FOLDER, --folder FOLDER
                        working folder (other than the current folder
~~~

## What the script does:
- Using your phone number and pin a request is send to Trade Republic and you are asked to enter a confirmation code
- You receive a one time confirmation code by phone and you enter it
- The script fetches all events of the last X days from Trade Republic
- Events are parsed and the collected transactions, bookings, expenses, and dividends are exported to PortfolioDividendTracker.xlsx

The .xlsx file mirrors the 4 tabs of the PDT Google Sheet. After running the script, all you have to do is copy the content of each tab into your PDT sheet. You can also add manual entries to the .xlsx file if needed, to keep it as a true 1:1 backup.

Next time you run the script:
- It will load the existing PortfolioDividendTracker.xlsx.
- It will save a backup .xlsx under a different name (just in case).

## Notes
Written in Python, using two external libraries:
- pytrpp
- openpyxl

Install them with:
~~~bash
pip install pytrpp openpyxl
~~~

## Disclaimers
I’ve tested this script extensively with:
- one-time transactions (buy only)
- auto-invest transactions
- dividend statements

Other types of events (such as selling a share) are simply not processed.

The script uses the unofficial Trade Republic API. In short: it works for now, but if Trade Republic changes their API next month, all bets are off.
