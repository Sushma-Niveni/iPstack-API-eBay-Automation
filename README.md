# iPstack-API-eBay-Automation

This project focuses on two main tasks: integrating with the iPstack API and web scraping eBay using Selenium. The objectives include interacting with APIs, storing data in MongoDB, and performing automated web scraping tasks.

## Table of Contents

1. [Part 1: iPstack and MongoDB](#part-1-ipstack-and-mongodb)
   - [Running MongoDB](#running-mongodb)
   - [Database Programming](#database-programming)
   - [Exploring IPStack](#exploring-ipstack)
   - [API Documentation Review](#api-documentation-review)
   - [API Call Program](#api-call-program)
   - [JSON Parsing](#json-parsing)
   - [Data Storage Enhancement](#data-storage-enhancement)
2. [Part 2: eBay + Selenium](#part-2-ebay--selenium)
   - [Automate Browser to Access eBay](#automate-browser-to-access-ebay)
   - [Search for Items on eBay](#search-for-items-on-ebay)
   - [Apply Filters](#apply-filters)
3. [Setup and Requirements](#setup-and-requirements)
4. [Notes](#notes)

## Part 1: iPstack and MongoDB

### Running MongoDB

1. **Ensure MongoDB is Installed and Running**
   - Verify MongoDB's operational status using a GUI tool like MongoDB Compass or Robo 3T.

### Database Programming

1. **Connect to MongoDB**
   - Write a Python or Java program to connect to your local MongoDB instance.
2. **Create and Populate Database**
   - Create a database named `msba`.
   - Insert the document `{"ip": "192.168.1.1", "city": "Davis", "zip": "95616"}` into a collection called `ip_addresses` within the `msba` database.

   Example Python Code:
   ```python
   from pymongo import MongoClient

   # Connect to MongoDB
   client = MongoClient('mongodb://localhost:27017/')
   db = client['msba']
   collection = db['ip_addresses']

   # Insert document
   document = {"ip": "192.168.1.1", "city": "Davis", "zip": "95616"}
   collection.insert_one(document)
   ```

### Exploring IPStack

1. **Familiarize Yourself with the IPStack API**
   - Visit [IPStack](https://ipstack.com/) and request a free API key.
   
### API Documentation Review

1. **Review API Documentation**
   - Read the sections "Specify Output Format" and "Specify Response Fields" on [IPStack Documentation](https://ipstack.com/documentation).
   - Formulate URL strings to fetch main fields in JSON format for the IP addresses "8.8.8.8", "128.120.0.25", "128.32.12.14", "64.165.72.144", and your own IP address.

### API Call Program

1. **Develop API Call Program**
   - Write a Python or Java program to make API calls and display results.

   Example Python Code:
   ```python
   import requests

   api_key = 'YOUR_API_KEY'
   ip_addresses = ['8.8.8.8', '128.120.0.25', '128.32.12.14', '64.165.72.144', 'YOUR_IP_ADDRESS']
   for ip in ip_addresses:
       response = requests.get(f'https://api.ipstack.com/{ip}?access_key={api_key}')
       print(response.json())
   ```

### JSON Parsing

1. **Parse JSON Responses**
   - Convert JSON responses into Python objects and print "city" and "zip" fields.

   Example Python Code:
   ```python
   for ip in ip_addresses:
       response = requests.get(f'https://api.ipstack.com/{ip}?access_key={api_key}')
       data = response.json()
       print(f"IP: {data['ip']}, City: {data['city']}, Zip: {data['zip']}")
   ```

### Data Storage Enhancement

1. **Insert Records into MongoDB**
   - Modify your code to insert records into the `ip_addresses` collection in MongoDB.

   Example Python Code:
   ```python
   for ip in ip_addresses:
       response = requests.get(f'https://api.ipstack.com/{ip}?access_key={api_key}')
       data = response.json()
       collection.insert_one({
           "ip": data['ip'],
           "city": data['city'],
           "zip": data['zip']
       })
   ```

## Part 2: eBay + Selenium

### Automate Browser to Access eBay

1. **Use Selenium to Navigate eBay**
   - Set up Selenium to open a browser and go to [eBay](https://www.ebay.com/).

   Example Python Code:
   ```python
   from selenium import webdriver

   driver = webdriver.Chrome()
   driver.get('https://www.ebay.com/')
   ```

### Search for Items on eBay

1. **Perform a Search**
   - Use Selenium to search for "Cell Phones" on eBay.

   Example Python Code:
   ```python
   search_box = driver.find_element_by_id('gh-ac')
   search_box.send_keys('Cell Phones')
   search_box.submit()
   ```

### Apply Filters

1. **Apply Filters**
   - After displaying search results, apply the filters:
     - Network: Unlocked
     - Brand: LG
     - Screen Size: 6 in or More

   Example Python Code:
   ```python
   # Apply filters
   network_filter = driver.find_element_by_xpath("//span[text()='Unlocked']")
   network_filter.click()

   brand_filter = driver.find_element_by_xpath("//span[text()='LG']")
   brand_filter.click()

   screen_size_filter = driver.find_element_by_xpath("//span[text()='6 in or More']")
   screen_size_filter.click()
   ```

