# Books Web Scraping

## Project Overview
---
This web scraping project involved extracting data from 50 web pages to gather comprehensive and structured information. Utilizing Python and Beautiful Soup, the scraper navigated through each page, 
efficiently retrieving the desired data points.

## Import libraries
---
```
import requests
from bs4 import BeautifulSoup
import csv
import pandas as pd
```

## Parse The HTML Content
---
```
soup = BeautifulSoup(response.text, 'html.parser')
```

## Extract Book Details For Page 1
---
```
# find all book titles and their links
books = soup.find_all('h3')
books_extracted = 0

# *Iterate through the books and extract the information for each group
for book in books:
    book_url = book.find('a')['href']
    
    # *Ensure the book_url is complete
    if not book_url.startswith('http'):
        book_url = url + book_url
    
    book_response = requests.get(book_url)
    book_soup = BeautifulSoup(book_response.content, 'html.parser')

    title = book_soup.find('h1').text
    category = book_soup.find('ul', class_='breadcrumb').find_all('a')[2].text.strip()

    rating_element = book_soup.find('p', class_='star-rating')
    rating = rating_element['class'][1] if rating_element else 'No rating'

    price_element = book_soup.find('p', class_='price_color')
    price = price_element.text.strip() if price_element else 'No price'

    availability_element = book_soup.find('p', class_='instock availability')
    availability = availability_element.text.strip() if availability_element else 'Not available'

    books_extracted += 1

    print(f"Title: {title}")
    print(f"Category: {category}")
    print(f"Rating: {rating}")
    print(f"Price: {price}")
    print(f"Availability: {availability}")
    print("******")

```

### Extract The Content Of All The 50 Pages
---
```
import requests
from bs4 import BeautifulSoup

# create a list to hold all the book information 
books_data = []

# Loop through all the 50 pages
for page_num in range(1, 51):
    url = f"https://books.toscrape.com/catalogue/page-{page_num}.html"
    response = requests.get(url)
    soup = BeautifulSoup(response.content, 'html.parser')

    books = soup.find_all('h3')
    for book in books:
        book_url = book.find('a')['href']
    
        # Ensure the book_url is complete
        if not book_url.startswith('http'):
            book_url = "https://books.toscrape.com/catalogue/" + book_url
    
        book_response = requests.get(book_url)
        book_soup = BeautifulSoup(book_response.content, 'html.parser')

        title = book_soup.find('h1').text

        breadcrumb = book_soup.find('ul', class_='breadcrumb')
        if breadcrumb:
            category = breadcrumb.find_all('a')[2].text.strip() if len(breadcrumb.find_all('a')) > 2 else 'Unknown'
        else:
            category = 'Unknown'
    
        rating_element = book_soup.find('p', class_='star-rating')
        rating = rating_element['class'][1] if rating_element else 'No rating'

        price_element = book_soup.find('p', class_='price_color')
        price = price_element.text.strip() if price_element else 'No price'

        availability_element = book_soup.find('p', class_='instock availability')
        availability = availability_element.text.strip() if availability_element else 'Not available'

        books_data.append([title, category, rating, price, availability])

        print(f"Title: {title}")
        print(f"Category: {category}")
        print(f"Rating: {rating}")
        print(f"Price: {price}")
        print(f"Availability: {availability}")
        print("******")
    
    print(f"{len(books_data)} books extracted so far...")

# If you want to see the final list of books_data
print(books_data)

```

### Export The Data
---
```
# convert the list to DataFrame
df = pd.DataFrame(books_data, columns= ["Title", "Category", "Rating", "Price", "Availability"])
# display the first 10 rows
print(df.head(10))
```

### Saving The data To a CSV File
---
```
# save to csv
df.to_csv(r"C:\Users\ASUS\OneDrive\Pyhton folder\books.csv", index = False)
```
