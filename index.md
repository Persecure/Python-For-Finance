![image](https://user-images.githubusercontent.com/93418272/185640010-764f19d3-7db7-4620-b847-57e99b55e1f7.png)

<!-- wp:paragraph {"fontSize":"large"} -->
<p class="has-large-font-size">1 - Loading Financial Data</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Import the following modules</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">from pandas_datareader import data as web
import datetime as dt
import matplotlib.pyplot as plt
from matplotlib import style 
import mplfinance as mpf
import bs4 as bs
import requests 
import pickle 
import numpy as np</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>Set a datetime function</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">start = dt.datetime(2017,1,1)
end = dt.datetime(2019,1,1)</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>Define a data frame and load financial data into it from Yahoo Finance</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">df = web.get_data_yahoo('AAPL',start,end, interval='d')</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>Print the dataframe to show the data</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":593,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/02/image-134.png?w=777" alt="" class="wp-image-593"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Show just the close column</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":595,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/02/image-135.png?w=537" alt="" class="wp-image-595"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Show just the close column for a specific date</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":596,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/02/image-136.png?w=522" alt="" class="wp-image-596"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>You can save the data to a csv or xlsx file with the following inputs.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":598,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/02/image-137.png?w=368" alt="" class="wp-image-598"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph {"fontSize":"large"} -->
<p class="has-large-font-size">2 - Graphical Visualization</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Plot the Adjusted Close price with matplotlib</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">df['Adj Close'].plot()
plt.show()</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":635,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1-4.png?w=552" alt="" class="wp-image-635"/><figcaption class="wp-element-caption">APPL - 2017-2019</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Plotting the graph with labels and styles</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">style.use('ggplot')
plt.ylabel('Adjusted Close')
plt.title('AAPL Share Price')
df['Adj Close'].plot()
plt.show()</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":636,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1-5.png?w=564" alt="" class="wp-image-636"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Comparing stocks</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">visa = web.get_data_yahoo('V',start,end, interval='d')
mastercard = web.get_data_yahoo('MA',start,end, interval='d')
visa['Adj Close'].plot(label="V")
mastercard['Adj Close'].plot(label="MA")
plt.ylabel('Adjusted Close')
plt.title('Share Price')
plt.legend(loc='upper left')
plt.show()</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":637,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1-6.png?w=572" alt="" class="wp-image-637"/></figure>
<!-- /wp:image -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">apple = web.get_data_yahoo('AAPL',start,end, interval='d')
facebook = web.get_data_yahoo('FB',start,end, interval='d')
apple['Adj Close'].plot(label="AAPL")
facebook['Adj Close'].plot(label="FB")
plt.ylabel('Adjusted Close')
plt.title('Share Price')
plt.legend(loc='upper left')
plt.show()</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":624,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1-1.png?w=572" alt="" class="wp-image-624"/><figcaption class="wp-element-caption">There is drastic price difference and the graph does not give us any information</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Subplotting</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">plt.subplot(211)
apple['Adj Close'].plot(color='blue')
plt.ylabel('Adjusted Close')
plt.title('AAPL Share Price')

plt.subplot(212)
apple['Adj Close'].plot()
plt.ylabel('Adjusted Close')
plt.title('Facebook Share Price')

plt.tight_layout()
plt.show()</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":623,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1.png?w=629" alt="" class="wp-image-623"/><figcaption class="wp-element-caption">Better picture now</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size">3 - Candlestick Charts</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Let's set up a candlestick chart to further examine the graph.</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">mpf.plot(apple, type='candle', style='charles',
            title='Apple, 2017- 2019',
            ylabel='Price ($)',
            ylabel_lower='Shares \nTraded') 
         </pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":625,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1-2.png?w=651" alt="" class="wp-image-625"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size">4 - Analysis and Statistics</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>100 Day moving average</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">#100 Day Moving Average
apple['100d_ma'] = apple['Adj Close'].rolling(window = 100, min_periods = 0).mean()
#Remove NaN-Values
apple.dropna(inplace=True)
print(apple.head())</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":627,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/image-6.png?w=574" alt="" class="wp-image-627"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Visualization </p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">ax1 = plt.subplot2grid((6,1),(0,0), rowspan = 4, colspan = 1)
ax2 = plt.subplot2grid((6,1),(4,0), rowspan = 2, colspan = 1, sharex = ax1)

ax1.plot(apple.index, apple['Adj Close'])
ax1.plot(apple.index, apple['100d_ma'])
ax2.fill_between(apple.index, apple['Volume'])

plt.tight_layout()
plt.show()</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":629,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1-3.png?w=626" alt="" class="wp-image-629"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Additional Key Statistics</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">#Percentage Change
apple['PCT_Change'] = (apple['Close'] - apple['Open']) / apple['Open']
print(apple['PCT_Change'])</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":631,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/image-7.png?w=216" alt="" class="wp-image-631"/></figure>
<!-- /wp:image -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">#High Low Percentage - How volatile the stock is
apple['HL_PCT'] = (apple['High'] - apple['Low']) / apple['Close'] 
print(apple['HL_PCT'])</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":633,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/image-8.png?w=207" alt="" class="wp-image-633"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size">5 - Regression Lines</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The Linear Regression Line is&nbsp;<strong>mainly used to determine trend direction</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Load financial data</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">start = dt.datetime(2016,1,1)
end = dt.datetime(2019,1,1)

apple = web.get_data_yahoo('AAPL',start,end, interval='d')
data = apple['Adj Close']

#Quantify our dates in order to be able to use them as X-values
x = data.index.map(mdates.date2num)

#Use Numpy to create a linear regression line
fit = np.polyfit(x, data.values, 1)
fit1d = np.poly1d(fit)</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>Plot the graph </p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">plt.grid()
plt.plot(data.index, data.values, 'b')
plt.plot(data.index, fit1d(x),'r')
plt.show()</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":642,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1-7.png?w=550" alt="" class="wp-image-642"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Setting the time frame</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">rstart = dt.datetime(2018,7,1)
rend = dt.datetime(2019,1,1)

#Create a new data frame and cut off all other data entries
fit_data = data.reset_index()
pos1 = fit_data[fit_data.Date >= rstart].index[0]
pos2 = fit_data[fit_data.Date &lt;= rend].index[-1]

fit_data = fit_data.iloc[pos1:pos2]</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>Rewrite the function </p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"python"} -->
<pre class="wp-block-syntaxhighlighter-code">dates = fit_data.Date.map(mdates.date2num)

fit = np.polyfit(dates, fit_data['Adj Close'], 1)
fit1d = np.poly1d(fit)

plt.grid()
plt.plot(data.index, data.values, 'b')
plt.plot(fit_data.Date, fit1d(dates), 'r')
plt.show()</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:image {"id":646,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://persecure.files.wordpress.com/2022/03/1-8.png?w=550" alt="" class="wp-image-646"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>The slope is negative, since the prices go down in that time frame. </p>
<!-- /wp:paragraph -->
