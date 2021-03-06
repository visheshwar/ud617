# Some other Python MapReduce codes to analyze log files (sales log or weblog)

This forder contains some simple MapReduce codes to analyze log files.
mappers and reducers codes can be found in the following folders :

* retailer_log/ : codes to analyze a log file containing retailer sales
* web_log/ : codes to analyze a weblog in common log format

Keep reading for more details.

## Analysing Log file of sales from a retailer (lesson 3)

`purchases.txt` is a log file extracted from the database of a retailer.
It contains the following tab-delimited fields :

* date of purchase
* time of purchase
* store name
* product type
* cost
* method of payment

Preview :
```
2012-01-01	09:00	San Jose	Men's Clothing	214.05	Amex
2012-01-01	09:00	Fort Worth	Women's Clothing	153.57	Visa
2012-01-01	09:00	San Diego	Music	66.08	Cash
2012-01-01	09:00	Pittsburgh	Pet Supplies	493.51	Discover
2012-01-01	09:00	Omaha	Children's Clothing	235.63	MasterCard
2012-01-01	09:00	Stockton	Men's Clothing	247.18	MasterCard
2012-01-01	09:00	Austin	Cameras	379.6	Visa
2012-01-01	09:00	New York	Consumer Electronics	296.8	Cash
2012-01-01	09:00	Corpus Christi	Toys	25.38	Discover
2012-01-01	09:00	Fort Worth	Toys	213.88	Visa
```

Let's write some MapReduce codes to answer the following questions:

1. total sales per store ?
2. total sales per product category ?
3. highest indivitual sale for each store ?
4. total sales value across all stores and total number of sales ?
5. Mean of sales for each weekday ? (from lesson 4)

mappers and reducers codes are in the retailer_log folder and numbered from 1 to 5 according to the questions above. the `testfile` contains the first 50 entries of the log file, intended for local testing.

## Analysing Web server log (lesson 3)

The dataset is an anonymized Web server log file from a public relations wompany whose clients were DVD distributors. The log file is in common log format (see Annexe), it contains the following informations :

* IP address which accessed the site
* data and time of the access
* name of the page visited

Preview:
```
10.223.157.186 - - [15/Jul/2009:14:58:59 -0700] "GET / HTTP/1.1" 403 202
10.223.157.186 - - [15/Jul/2009:14:58:59 -0700] "GET /favicon.ico HTTP/1.1" 404 209
10.223.157.186 - - [15/Jul/2009:15:50:35 -0700] "GET / HTTP/1.1" 200 9157
10.223.157.186 - - [15/Jul/2009:15:50:35 -0700] "GET /assets/js/lowpro.js HTTP/1.1" 200 10469
10.223.157.186 - - [15/Jul/2009:15:50:35 -0700] "GET /assets/css/reset.css HTTP/1.1" 200 1014
10.223.157.186 - - [15/Jul/2009:15:50:35 -0700] "GET /assets/css/960.css HTTP/1.1" 200 6206
10.223.157.186 - - [15/Jul/2009:15:50:35 -0700] "GET /assets/css/the-associates.css HTTP/1.1" 200 15779
10.223.157.186 - - [15/Jul/2009:15:50:35 -0700] "GET /assets/js/the-associates.js HTTP/1.1" 200 4492
10.223.157.186 - - [15/Jul/2009:15:50:35 -0700] "GET /assets/js/lightbox.js HTTP/1.1" 200 25960
10.223.157.186 - - [15/Jul/2009:15:50:36 -0700] "GET /assets/img/search-button.gif HTTP/1.1" 200 168
```

We write MapReduce codes to adress the following points:

1. number hits for each different file on the Website
2. number of hits to the site made by each different IP adress
3. most popular file on the website

mappers and reducers codes are in the web_log/ folder and numbered from 1 to 3 according to the questions above. the `testfile` contains the first 100 log entries, intended for local testing.

## Annexe: common log format

The web server log is in [Common Log Format](http://en.wikipedia.org/wiki/Common_Log_Format):

```
10.223.157.186 - - [15/Jul/2009:15:50:35 -0700] "GET /assets/js/lowpro.js HTTP/1.1" 200 10469

%h %l %u %t \"%r\" %>s %b
```

* %h is the IP address of the client
* %l is identity of the client, or "-" if it's unavailable
* %u is username of the client, or "-" if it's unavailable
* %t is the time that the server finished processing the request. The format is [day/month/year:hour:minute:second zone]
* %r is the request line from the client is given (in double quotes). It contains the method, path, query-string, and protocol or the request.
* %>s is the status code that the server sends back to the client. You will see see mostly status codes 200 (OK - The request has succeeded), 304 (Not Modified) and 404 (Not Found). See more information on status codes in W3C.org
* %b is the size of the object returned to the client, in bytes. It will be "-" in case of status code 304.

Regular expressions were used to match the IP and request (see. mapping functions in web_log/ folder).







