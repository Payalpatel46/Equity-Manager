# Equity-Manager
Implementing a website via which users can “buy” and “sell” stocks.

## Framework & Languages
- HTML, CSS, JavaScript, Bootstrap
- Flask, Python
- SQL Database

## Configuring
Before getting started, we’ll need to register for an API key in order to be able to query IEX’s data. To do so, follow these steps:

- Visit iexcloud.io/cloud-login#/register/.
- Enter your email address and a password, and click “Create account”.
- On the next page, scroll down to choose the Start (free) plan.
- Once you’ve confirmed your account via a confirmation email, sign in to iexcloud.io.
- Click API Tokens.
- Copy the key that appears under the Token column (it should begin with pk_).
- In a terminal window within CS50 IDE, execute:
  $ export API_KEY=value
Note: where value is that (pasted) value, without any space immediately before or after the =. You also may wish to paste that value in a text document somewhere, in case you need it again later.

## Specification
 1. ### register ### 
 
 Total the execution of enlist in such a way that it permits a client to enroll for an account through a shape
- Require that a client input a username, executed as a content field whose title is username. Render an expression of remorse in case the user's input is clear or the username as of now exists.
- Require that a client input a secret word, actualized as a content field whose title is secret word, and after that that same watchword once more, executed as a content field whose title is affirmation. Render an expression of remorse in case either input is blank or the passwords don't coordinate.
- Yield the user's input by means of POST to /enlist.
- Embed the unused client into clients, putting away a hash of the user's watchword, not the watchword itself. Hash the user's password with generate_password_hash Chances are you'll need to form a unused format (e.g., register.html) that's very comparable to login.html.

Once you've executed enlist accurately, you ought to be able to enlist for an account and log in (since login and logout as of now work)! And you ought to be able to see your lines through phpLiteAdmin or sqlite3.

2. ### quote ###

Total the execution of cite in such a way that it permits a client to see up a stock's current cost.
- Require that a client input a stock's image, executed as a content field whose title is image.
- Yield the user's input through POST to /cite.
- Chances are you'll need to make two modern formats (e.g., quote.html and quoted.html). When a client visits /cite through GET, render one of those formats, interior of which ought to be an HTML frame that submits to /cite through POST. In reaction to a POST, cite can render that moment layout, implanting inside it one or more values from lookup.
   
3. ### buy ###
 Total the usage of purchase in such a way that it empowers a client to purchase stocks.

- Require that a client input a stock's image, executed as a content field whose title is image. Render an statement of regret in case the input is clear or the image does not exist (as per the return esteem of lookup).
- Require that a client input a number of offers, actualized as a content field whose title is offers. Render an expression of remorse in case the input isn't a positive numbers.
- Yield the user's input through POST to /purchase.
- Chances are you'll need to call lookup to see up a stock's current cost.
- Chances are you'll need to Choose how much cash the client as of now has in clients.
- Include one or more modern tables to finance.db through which to keep track of the purchase. Store sufficient data so that you just know who bought what at what cost and when.
- Utilize suitable SQLite sorts.
- Characterize Interesting files on any areas that ought to be one of a kind.
- Characterize (non-UNIQUE) records on any areas by means of which you may look (as by means of SELECT with WHERE).
- Render an statement of regret, without completing a buy, in the event that the client cannot bear the number of offers at the current cost.
- You do not ought to stress almost race conditions (or utilize exchanges).

Once you've actualized purchase accurately, you should be able to see users' buys in your unused table(s) by means of phpLiteAdmin or sqlite3.
 
4. ### index ###
Total the usage of list in such a way that it shows an HTML table summarizing, for the client as of now logged in, which stocks the client claims, the numbers of offers claimed, the current cost of each stock, and the entire esteem of each holding (i.e., offers times cost). Also display the user's current cash adjust at the side a terrific add up to (i.e., stocks' add up to esteem additionally cash).

- Chances are you'll need to execute different Chooses. Depending on how you actualize your table(s), you might discover Bunch BY HAVING Whole and/or WHERE of intrigued.
- Chances are you'll need to call lookup for each stock.

5. ### sell ###
Total the usage of offer in such a way that it empowers a client to offer offers of a stock (that he or she possesses).

- Require that a client input a stock's image, executed as a select menu whose title is image. Render an expression of remorse in the event that the client falls flat to choose a stock or on the off chance that (by one means or another, once submitted) the client does not claim any offers of that stock.
- Require that a client input a number of offers, actualized as a content field whose title is offers. Render an apology if the input isn't a positive numbers or in the event that the client does not claim that numerous offers of the stock.
- Yield the user's input by means of POST to /sell.
- You do not have to be stress around race conditions (or utilize exchanges). 

6. ### history ###
Total the usage of history in such a way that it shows an HTML table summarizing all of a user's exchanges ever, posting push by push each and each purchase and each offer.

- For each push, make clear whether a stock was bought or sold and incorporate the stock's image, the (buy or deal) cost, the number of offers bought or sold, and the date and time at which the exchange happened.
- You might got to change the table you made for buy or supplement it with an extra table. Attempt to play down redundancies. 
 
## Background
In case you're not very beyond any doubt what it implies to purchase and offer stocks (i.e., offers of a company), head here for a instructional exercise.

You're almost to actualize C$50 Back, a web app by means of which you'll be able oversee portfolios of stocks. Not as it were will this instrument permit you to check genuine stocks' actual costs and portfolios' values, it'll too let you purchase (affirm, “buy”) and offer (affirm, “sell”) stocks by questioning IEX for stocks' costs.

In fact, IEX lets you download stock cites by means of their API (application programming interface) utilizing URLs like https:
//cloud-sse.iexapis.com/stable/stock/nflx/quote?token=API_KEY. Take note how Netflix's image (NFLX) is inserted in this URL; that's how IEX knows whose information to return. That interface won't really return any information since IEX requires you to utilize an API key (more around that in a bit), but on the off chance that it did, you'd see a reaction in JSON (JavaScript Protest Documentation) arrange like this:
 
`{  
   "symbol": "NFLX",
  
  "companyName": "Netflix, Inc.",
   
   "primaryExchange": "NASDAQ",
   
   "calculationPrice": "close",
   
   "open": 317.49,
   
   "openTime": 1564752600327,
   
   "close": 318.83,
   
   "closeTime": 1564776000616,
   
   "high": 319.41,
   
   "low": 311.8,
   
   "latestPrice": 318.83,
   
   "latestSource": "Close",
   
   "latestTime": "August 2, 2019",
   
   "latestUpdate": 1564776000616,
   
   "latestVolume": 6232279,
   
   "iexRealtimePrice": null,
   
   "iexRealtimeSize": null,
   
   "iexLastUpdated": null,
   
   "delayedPrice": 318.83,
   
   "delayedPriceTime": 1564776000616,
   
   "extendedPrice": 319.37,
   
   "extendedChange": 0.54,
   
   "extendedChangePercent": 0.00169,
   
   "extendedPriceTime": 1564876784244,
   
   "previousClose": 319.5,
   
   "previousVolume": 6563156,
   
   "change": -0.67,
   
   "changePercent": -0.0021,
   
   "volume": 6232279,
   
   "iexMarketPercent": null,
   
   "iexVolume": null,
   
   "avgTotalVolume": 7998833,
   
   "iexBidPrice": null,
   
   "iexBidSize": null,
   
   "iexAskPrice": null,
   
   "iexAskSize": null,
   
   "marketCap": 139594933050,
   
   "peRatio": 120.77,
   
   "week52High": 386.79,
   
   "week52Low": 231.23,
   
   "ytdChange": 0.18907500000000002,
   
   "lastTradeTime": 1564776000616
}`

Notice how, between the curly braces, there’s a comma-separated list of key-value pairs, with a colon separating each key from its value.
