# Table of contents
|Read No. | Name of chapter|
|:---------: |:--------------:|
|17|[Web Scrape with Python in 4 minutes](Web-Scrape-with-Python-in-4-minutes.md)
|17|[What is Web Scraping?](What-is-Web-Scraping.md)


# Web Scrape with Python in 4 minutes
## Web Scraping
### Web scraping is a technique to automatically access and extract large amounts of information from a website, which can save a huge amount of time and effort.

## New York MTA Data
### We will be downloading turnstile data from this site:
```
http://web.mta.info/developers/turnstile.html
```
### Turnstile data is compiled every week from May 2010 to present, so hundreds of .txt files exist on the site. Each date is a link to the .txt file that you can download.

## Inspecting the Website
### The first thing that we need to do is to figure out where we can locate the links to the files we want to download inside the multiple levels of HTML tags. Simply put, there is a lot of code on a website page and we want to find the relevant pieces of code that contains our data.

- On the website, right click and click on “Inspect”. This allows you to see the raw code behind the site.
- Notice that on the top left of the console, there is an arrow symbol.
### If you click on this arrow and then click on an area of the site itself, the code for that particular item will be highlighted in the console.

## Python Code
### We start by importing the following libraries.
```python
import requests
import urllib.request
import time
from bs4 import BeautifulSoup
```
### Next, we set the url to the website and access the site with our requests library.
```python
url = 'http://web.mta.info/developers/turnstile.html'
response = requests.get(url)
```

### Next we parse the html with BeautifulSoup so that we can work with a nicer, nested BeautifulSoup data structure.
```python
soup = BeautifulSoup(response.text, “html.parser”)
```
### We use the method .findAll to locate all of our <a> tags.
```python
soup.findAll('a')
```
### This code gives us every line of code that has an <a> tag. The information that we are interested in starts on line 38. That is, the very first text file is located in line 38, so we want to grab the rest of the text.
### Next, let’s extract the actual link that we want. Let’s test out the first link.

```python
one_a_tag = soup.findAll(‘a’)[38]
link = one_a_tag[‘href’]
```
### This code saves the first text file, ‘data/nyct/turnstile/turnstile_180922.txt’ to our variable link. The full url to download the data is actually ‘http://web.mta.info/developers/data/nyct/turnstile/turnstile_180922.txt’ which I discovered by clicking on the first data file on the website as a test. We can use our urllib.request library to download this file path to our computer. We provide request.urlretrieve with two parameters: file url and the filename. For my files, I named them “turnstile_180922.txt”, “turnstile_180901”, etc.
```python
download_url = 'http://web.mta.info/developers/'+ link
urllib.request.urlretrieve(download_url,'./'+link[link.find('/turnstile_')+1:])
```
### Last but not least, we should include this line of code so that we can pause our code for a second so that we are not spamming the website with requests. This helps us avoid getting flagged as a spammer.
```python
time.sleep(1)
```


# What is Web Scraping?
### Web scraping, web harvesting, or web data extraction is data scraping used for extracting data from websites. Web scraping software may access the World Wide Web directly using the Hypertext Transfer Protocol, or through a web browser. While web scraping can be done manually by a software user, the term typically refers to automated processes implemented using a bot or web crawler.

### Web scraping is used for contact scraping, and as a component of applications used for web indexing, web mining and data mining, online price change monitoring and price comparison, product review scraping (to watch the competition), gathering real estate listings, weather data monitoring, website change detection, research, tracking online presence and reputation, web mashup and, web data integration.

## Techniques
### **Human copy-and-paste**
### The simplest form of web scraping is manually copying and pasting data from a web page into a text file or spreadsheet.

### **Text pattern matching**
### A simple yet powerful approach to extract information from web pages can be based on the UNIX grep command or regular expression-matching facilities of programming languages (for instance Perl or Python).

### **HTTP programming**
### Static and dynamic web pages can be retrieved by posting HTTP requests to the remote web server using socket programming.

### **HTML parsing**
### Many websites have large collections of pages generated dynamically from an underlying structured source like a database. Data of the same category are typically encoded into similar pages by a common script or template. In data mining, a program that detects such templates in a particular information source, extracts its content and translates it into a relational form, is called a wrapper. Wrapper generation algorithms assume that input pages of a wrapper induction system conform to a common template and that they can be easily identified in terms of a URL common scheme.[2] Moreover, some semi-structured data query languages, such as XQuery and the HTQL, can be used to parse HTML pages and to retrieve and transform page content.[3]

### **DOM parsing**
### Further information: Document Object Model
### By embedding a full-fledged web browser, such as the Internet Explorer or the Mozilla browser control, programs can retrieve the dynamic content generated by client-side scripts. These browser controls also parse web pages into a DOM tree, based on which programs can retrieve parts of the pages. Languages such as Xpath can be used to parse the resulting DOM tree.

### **Vertical aggregation**
### There are several companies that have developed vertical specific harvesting platforms. These platforms create and monitor a multitude of "bots" for specific verticals with no "man in the loop" (no direct human involvement), and no work related to a specific target site. The preparation involves establishing the knowledge base for the entire vertical and then the platform creates the bots automatically. The platform's robustness is measured by the quality of the information it retrieves (usually number of fields) and its scalability (how quick it can scale up to hundreds or thousands of sites). This scalability is mostly used to target the Long Tail of sites that common aggregators find complicated or too labor-intensive to harvest content from.