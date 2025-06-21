This script can extract broker actions from broker PDF's and export them to an xlsx file in the format of Portfolio Dividend Tracker (PDT)
Please note that at this point only broker PDF's from Trade Republic can be processed

# Trade Republic → Portfolio Dividend Tracker (PDT)
I am a very happy user of Portfolio Dividend Tracker. Unfortunately, there's no automatic export from Trade Republic to PDT. This is because Trade Republic still doesn’t offer a decent export function. At the moment, the only option is to manually download each transaction and dividend statement as a PDF. Painful.
Since I use the auto-invest feature in Trade Republic — buying 11 fractional shares twice a month — I quickly realized that manually entering 22 transactions every month wasn’t going to happen. I'm way too lazy for that. So I wrote a script.

---

## How to use it
_Basic command line knowledge assumed._

1. Manually download all new transaction and dividend statement PDFs from Trade Republic and save them locally
2. Download the script from GitHub: [https://github.com/jzp74/broker2pdt](https://github.com/jzp74/broker2pdt)
3. Run the script with the path to your PDF folder as an argument:
~~~bash
python broker2pdt.py /path/to/your/pdf/folder
~~~

## What the script does:
- For every transaction PDF, it creates a new transaction, booking, and any applicable expenses
- For every dividend statement PDF, it creates a new dividend entry
- Processed PDFs are renamed and moved to a processed/ subfolder
- Once all PDFs are parsed, the collected transactions, bookings, expenses, and dividends are exported to PortfolioDividendTracker.xlsx.

This .xlsx file mirrors the 4 tabs of the PDT Google Sheet. After running the script, all you have to do is copy the content of each tab into your PDT sheet. You can also add manual entries to the .xlsx file if needed, to keep it as a true 1:1 backup.

Next time you run the script:
- It will load the existing PortfolioDividendTracker.xlsx.
- It will save a backup under a different name (just in case).

## Notes
Written in Python, using two external libraries:
- pypdf
- openpyxl

Install them with:
~~~bash
pip install pypdf openpyxl
~~~

## Disclaimers
I’ve tested this script extensively with:
- one-time purchases
- auto-invest transactions
- dividend statements

The script works by searching for specific strings and patterns in the PDF text — simple but effective. However, Trade Republic's PDF formatting and language are... inconsistent, to put it politely. As a Dutch user, I get a mix of English and Dutch documents. The script does a very basic language check to figure out which is which.

In short: it works for now, but if Trade Republic changes their PDFs next month, all bets are off.
