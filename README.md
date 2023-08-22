import requests
from bs4 import BeautifulSoup

base_url = "https://www.amazon.in/s"
search_query = "bags"
num_pages = 20

for page in range(1, num_pages + 1):
    params = {
        "k": search_query,
        "page": page
    }
    
    response = requests.get(base_url, params=params)
    if response.status_code == 200:
        soup = BeautifulSoup(response.content, "html.parser")
        
        product_list = soup.find_all("div", class_="s-result-item")
        
        for product in product_list:
            product_url = product.find("a", class_="a-link-normal")["href"]
            product_name = product.find("span", class_="a-text-normal").text
            product_price = product.find("span", class_="a-offscreen").text
            rating = product.find("span", class_="a-icon-alt")
            num_reviews = product.find("span", {"aria-label": "customer reviews"}).text.split()[0]
            
            print("Product URL:", product_url)
            print("Product Name:", product_name)
            print("Product Price:", product_price)
            print("Rating:", rating)
            print("Number of Reviews:", num_reviews)
            
    else:
        print("Failed to retrieve page:", page)

    
