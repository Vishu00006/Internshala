# Internshala
For internship assissgnment
import requests
from bs4 import BeautifulSoup

base_url = "https://www.amazon.in/s"
query_params = {
    "k": "bags",
    "crid": "2M096C61O4MLT",
    "qid": "1653308124",
    "sprefix": "ba,aps,283",
    "ref": "sr_pg_1"
}

# Number of pages to scrape
num_pages = 20

for page_number in range(1, num_pages + 1):
    query_params["page"] = page_number
    response = requests.get(base_url, params=query_params)
    
    if response.status_code == 200:
        soup = BeautifulSoup(response.content, "html.parser")
        # Extract and process the product listings from the soup
        
        # You'll need to identify the HTML structure of the product listings
        # and extract the relevant information using BeautifulSoup's methods
        
        # Example: extracting product titles
        product_titles = soup.find_all("span", class_="a-text-normal")
        for title in product_titles:
            print(title.text)
    else:
        print(f"Failed to fetch page {page_number}")

    # Add a delay to avoid overloading the server
    time.sleep(2)  # Import the time module for this
    
