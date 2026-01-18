# python-tvdatafeed-historical-downloader
This repository provides a complete Python script for downloading historical market data from TradingView using the tvDatafeed library. It includes login guidance, multiple example use cases, 1-minute to 1-hour timeframe support, and automated CSV exporting for NIFTY, indices, futures, and MCX instruments.


from tvDatafeed import TvDatafeed, Interval
import pandas as pd

#please mention your chrdential over here to login & fetch required data from required timeline.
#username = 'YourTradingViewUsername'
#password = 'YourTradingViewPassword'

#To use it without logging in feed credentials Inside (as tv = TvDatafeed(username, password) mentioned below)
tv = TvDatafeed()

""" To download the data use tv.get_hist method.

It accepts following arguments and returns pandas dataframe """

#example below formate.

""" (symbol: str, exchange: str = 'NSE', interval: Interval = Interval.in_daily, n_bars: int = 10, fut_contract: int | None = None, extended_session: bool = False) -> DataFrame) """

#for Example.
""" 
# index
nifty_index_data = tv.get_hist(symbol='NIFTY',exchange='NSE',interval=Interval.in_1_hour,n_bars=1000)

# futures continuous contract
nifty_futures_data = tv.get_hist(symbol='NIFTY',exchange='NSE',interval=Interval.in_1_hour,n_bars=1000,fut_contract=1)

# crudeoil
crudeoil_data = tv.get_hist(symbol='CRUDEOIL',exchange='MCX',interval=Interval.in_1_hour,n_bars=5000,fut_contract=1)

# downloading data for extended market hours
extended_price_data = tv.get_hist(symbol="EICHERMOT",exchange="NSE",interval=Interval.in_1_hour,n_bars=500, extended_session=False) """

#so if we need to download historical data for NIFTY index from NSE exchange with 1 minute interval for last 10000 bars, we can do it as follows:

nifty_index_data = tv.get_hist(
    symbol='NIFTY',
    exchange='NSE',
    interval=Interval.in_1_minute,
    n_bars=10000
)

print(nifty_index_data)

# ------------------------------------------------------------
# EXPORT DATA TO CSV
# ------------------------------------------------------------
# Reset index (optional but recommended for CSV)
nifty_index_data = nifty_index_data.reset_index()

# Save to CSV file
nifty_index_data.to_csv("NIFTY_1MIN_10000BARS.csv", index=False)

print("CSV Exported Successfully: NIFTY_1MIN_10000BARS.csv")

