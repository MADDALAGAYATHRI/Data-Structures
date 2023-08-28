import requests
from bs4 import BeautifulSoup

url = "https://example-bookstore.com/books"
response = requests.get(url)

if response.status_code == 200:
    html = response.text
    soup = BeautifulSoup(html, "html.parser")

    book_list = []

    for book in soup.find_all("div", class_="book"):
        title = book.find("h2", class_="title").text
        author = book.find("p", class_="author").text
        price = book.find("span", class_="price").text

        book_info = {
            "title": title,
            "author": author,
            "price": price
        }

        book_list.append(book_info)

    for book in book_list:
        print(f"Title: {book['title']}")
        print(f"Author: {book['author']}")
        print(f"Price: {book['price']}")
        print()

else:
    print("Failed to retrieve the page")
