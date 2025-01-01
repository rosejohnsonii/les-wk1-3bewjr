I'll create a simple web scraper tool using Python that scrapes data from a website and saves it to a JSON file. We'll use the `requests` library to send HTTP requests and the `BeautifulSoup` library to parse the HTML responses.

**Web Scraper Tool: "Book Info Scraper"**

This tool will scrape the title, author, and price of books from a website like [Goodreads](https://www.goodreads.com/).

**Code:**
```python
import requests
from bs4 import BeautifulSoup
import json

# Define the URL of the website we want to scrape
url = "https://www.goodreads.com/search?q=python&domain_book=on"

# Send an HTTP GET request to the website
response = requests.get(url)

# Check if the response was successful
if response.status_code == 200:
    # Parse the HTML response using BeautifulSoup
    soup = BeautifulSoup(response.content, 'html.parser')

    # Find all book elements on the page
    book_elements = soup.find_all('div', class_='book')

    # Create an empty list to store the scraped data
    scraped_data = []

    # Loop through each book element and extract the title, author, and price
    for book in book_elements:
        title = book.find('a', class_='book-title').text.strip()
        author = book.find('span', class_='author').text.strip()
        price = book.find('span', class_='price').text.strip()

        # Create a dictionary to store the scraped data
        data = {
            'title': title,
            'author': author,
            'price': price
        }

        # Add the dictionary to the list of scraped data
        scraped_data.append(data)

    # Save the scraped data to a JSON file
    with open('scraped_data.json', 'w') as f:
        json.dump(scraped_data, f, indent=4)

else:
    print("Failed to retrieve data")
```
**Explanation:**

1. We first import the necessary libraries: `requests` for sending HTTP requests and `BeautifulSoup` for parsing HTML responses.
2. We define the URL of the website we want to scrape, which is [Goodreads](https://www.goodreads.com/).
3. We send an HTTP GET request to the website using `requests.get()`.
4. We check if the response was successful by checking the status code (200). If it's not successful, we print an error message.
5. We parse the HTML response using `BeautifulSoup`.
6. We find all book elements on the page by searching for elements with the class `book`.
7. We loop through each book element and extract the title, author, and price using `find()` method.
8. We create a dictionary to store the scraped data and add it to a list of dictionaries.
9. We save the list of dictionaries to a JSON file using `json.dump()`.
10. Finally, we print a success message.

**Example Use Case:**

You can run this script in your terminal/command prompt by saving it to a file named `book_scraper.py` and running it with `python book_scraper.py`. This will scrape the title, author, and price of books from Goodreads and save them to a JSON file named `scraped_data.json`.

Note: This is a simple example and you may need to modify the script to fit your specific use case. Additionally, be aware of Goodreads' terms of service and scraping policies before running this script.
