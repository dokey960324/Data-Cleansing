- Project: catalyst
- File: generate.py 
```Python
def main():
    symbols = ['AAPL', 'MSFT', 'BRK-A']
    # Specifically chosen to include the AAPL split on June 9, 2014.
    for symbol in symbols:
        data = DataReader(
            symbol,
            'yahoo',
            start='2014-03-01',
            end='2014-09-01',
        )
        data.rename(
            columns={
                'Open': 'open',
                'High': 'high',
                'Low': 'low',
                'Close': 'close',
                'Volume': 'volume',
            },
            inplace=True,
        )
        del data['Adj Close']

        dest = join(here, symbol + '.csv')
        print("Writing %s -> %s" % (symbol, dest))
        data.to_csv(dest, index_label='day') 
```

---
- Project: Stock-Market-Prediction
- Author: Diptiranjan1
- File: sp500-alldata-p6.py

```Python
def get_data_from_yahoo(reload_sp500=False):
	if reload_sp500:
		tickers = save_sp500_ticker()
	else:
		with open("sp500tickers.pickle","rb") as f:
			tickers = pickle.load(f)

	# Now we will save all SP500 data as csv files
	if not os.path.exists('stock_dfs'):	# if this directory doesn't exist
		os.makedirs('stock_dfs')

	start =dt.datetime(2000,1,1)
	end = dt.datetime(2017,2,8)

	# if net is slow just put in parameter in tickers[:?] to specify number of companies you want etail of.
	for ticker in tickers:
		print(ticker)
		if not os.path.exists('stock_dfs/{}.csv'.format(ticker)):
			df = web.DataReader(ticker,'yahoo',start,end)
			df.to_csv('stock_dfs/{}.csv'.format(ticker))
		else:
			print('Already have {}'.format(ticker)) 
```
---

- Project: dash-hello-world
- File: app.py

```Python
def update_graph(selected_dropdown_value):
    df = web.DataReader(
        selected_dropdown_value, data_source='google',
        start=dt(2017, 1, 1), end=dt.now())
    return {
        'data': [{
            'x': df.index,
            'y': df.Close,
            'line': {
                'width': 3,
                'shape': 'spline'
            }
        }],
        'layout': {
            'margin': {
                'l': 30,
                'r': 20,
                'b': 30,
                't': 20
            }
        }
    } 
```
---

- Project: hpat
- File: stock_data_read.py

```Python
def main():
    stocks = pd.read_csv('all_syms.csv')
    file_name = "stock_data_all_google.hdf5"
    f = h5py.File(file_name, "w")

    for symbol in stocks.Symbol:
        try:
            df = data.DataReader(symbol, 'google', start='1/1/2000')
        except:
            continue
        N = len(df)
        grp = f.create_group(symbol)
        grp.create_dataset("Open", (N,), dtype='f8')[:] = df["Open"]
        grp.create_dataset("High", (N,), dtype='f8')[:] = df["High"]
        grp.create_dataset("Low", (N,), dtype='f8')[:] = df["Low"]
        grp.create_dataset("Close", (N,), dtype='f8')[:] = df["Close"]
        grp.create_dataset("Volume", (N,), dtype='f8')[:] = df["Volume"]
        grp.create_dataset("Date", (N,), dtype='i8')[:] = df.index.values.astype(np.int64)

    f.close() 
```
---

- Project: chanlun
- File: data.py 
```Python
def load_data(self, ticker, start, end, freq='D'):
        """

        :param ticker: str.
        :param start: str. '20160101'
        :param end: str. '20160201'
        :param freq: str. 'D'
        :return: pandas.DataFrame
        """
        if freq != 'D':
            raise ValueError('Frequency must be "D"')

        start = _date_parse(start)
        end = _date_parse(end)

        return web.DataReader(ticker, 'yahoo', start, end)
```

---

- Project: Stock-Market-Prediction
- File: p-final.py
```Python
def get_data_from_yahoo(reload_sp500=False):
    
    if reload_sp500:
        tickers = save_sp500_tickers()
    else:
        with open("sp500tickers.pickle","rb") as f:
            tickers = pickle.load(f)
    
    if not os.path.exists('stock_dfs'):
        os.makedirs('stock_dfs')

    start = dt.datetime(2000, 1, 1)
    end = dt.datetime(2016, 12, 31)
    
    for ticker in tickers:
        # just in case your connection breaks, we'd like to save our progress!
        if not os.path.exists('stock_dfs/{}.csv'.format(ticker)):
            df = web.DataReader(ticker, "yahoo", start, end)
            df.to_csv('stock_dfs/{}.csv'.format(ticker))
        else:
            print('Already have {}'.format(ticker)) 
```
---

- Project: Stock-Market-Prediction
- File: combinin-sp500-p7.py
```Python
def get_data_from_yahoo(reload_sp500=False):
    
    if reload_sp500:
        tickers = save_sp500_tickers()
    else:
        with open("sp500tickers.pickle","rb") as f:
            tickers = pickle.load(f)
    
    if not os.path.exists('stock_dfs'):
        os.makedirs('stock_dfs')

    start = dt.datetime(2000, 1, 1)
    end = dt.datetime(2016, 12, 31)
    
    for ticker in tickers:
        # just in case your connection breaks, we'd like to save our progress!
        if not os.path.exists('stock_dfs/{}.csv'.format(ticker)):
            df = web.DataReader(ticker, "yahoo", start, end)
            df.to_csv('stock_dfs/{}.csv'.format(ticker))
        else:
            print('Already have {}'.format(ticker)) 
```
---

- Project: py-investment
- File: owned_asset.py
```Python
def _get_pct_change(self, use_portfolio_benchmark=True,
                        market_ticker='^GSPC'):
        """
        Get the percentage change over the :class: Stock's start and end dates for both the asset as well as the market

        :param use_portfolio_benchmark: boolean
            When true the market ticker will be ignored and the ticker set for the whole :class: Portfolio will be used
        :param market_ticker: str
            Any valid ticker symbol to use as the market.
        :return: TimeSeries
        """
        pct_change = namedtuple('Pct_Change',
                                'market_pct_change stock_pct_change')
        if use_portfolio_benchmark:
            market_df = self.portfolio.benchmark
        else:
            market_df = web.DataReader(market_ticker, 'yahoo',
                                       start=self.start_date,
                                       end=self.end_date)
        market_pct_change = pd.Series(
                market_df['adj_close'].pct_change(periods=1))
        stock_pct_change = pd.Series(
                self.ohlcv['adj_close'].pct_change(periods=1))
        return pct_change(market_pct_change=market_pct_change,
                          stock_pct_change=stock_pct_change) 
```

---

- Project: derivative_code
- File: data_scraper.py
```Python
def download_data(tickers,start,end,all_data=False):
    count = 1
    if all_data==True:
        end = datetime.datetime.now()
        end = '%s-%s-%s' % (end.month,end.day,end.year)
        start = '01-01-1970'

    directory = 'stock_data'
    if not os.path.exists(directory):
        os.makedirs(directory)

    d = {}
    for ticker in tickers:
        filename = directory+'/'+ticker+'.csv'
        d[ticker] = web.DataReader(ticker,"yahoo",start,end)
        d[ticker].to_csv(filename)
        count  = count + 1
        if count % 50 == 0:
            time.sleep(10)
    return 
```

---

- Project: LSTM-GA-StockTrader
- File: test_eurostat.py
```Python
def test_get_cdh_e_fos(self):
        # Employed doctorate holders in non managerial and non professional
        # occupations by fields of science (%)
        df = web.DataReader('cdh_e_fos', 'eurostat', start=pd.Timestamp('2005-01-01'),
                            end=pd.Timestamp('2010-01-01'))

        self.assertTrue(isinstance(df, pd.DataFrame))
        self.assertEqual(df.shape, (2, 336))

        df = df['Percentage']['Total']['Natural sciences']
        df = df[['Norway', 'Poland', 'Portugal', 'Russia']]

        exp_col = pd.MultiIndex.from_product([['Norway', 'Poland', 'Portugal', 'Russia'],
                                              ['Annual']],
                                             names=['GEO', 'FREQ'])
        exp_idx = pd.DatetimeIndex(['2006-01-01', '2009-01-01'], name='TIME_PERIOD')

        values = np.array([[25.49, np.nan, 39.05, np.nan],
                           [20.38, 25.1, 27.77, 38.1]])
        expected = pd.DataFrame(values, index=exp_idx, columns=exp_col)
        tm.assert_frame_equal(df, expected) 
```
---

- Project: LSTM-GA-StockTrader
- File: test_data.py
```Python
def test_fred(self):

        # Throws an exception when DataReader can't get a 200 response from
        # FRED.

        start = datetime(2010, 1, 1)
        end = datetime(2013, 1, 27)

        received = web.DataReader("GDP", "fred", start, end)['GDP'].tail(1)[0]

        # < 7/30/14 16535 was returned
        #self.assertEqual(int(received), 16535)
        # < 8/20/15 16502 was returned
        #self.assertEqual(int(received), 16502)
        self.assertEqual(int(received), 16440)

        with tm.assertRaises(RemoteDataError):
            web.DataReader("NON EXISTENT SERIES", 'fred', start, end) 
```
