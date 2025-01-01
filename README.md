# Scraping Wisdom Pet Medicine Website

## Overview
This project demonstrates how to scrape data from the Wisdom Pet Medicine website, a fictitious site used for educational purposes. Using Python libraries like `requests` and `BeautifulSoup`, the project extracts key information such as the site title, articles, contact details, testimonials, staff information, and hyperlinks.

## Features
- **HTTP Requests**: Accesses the Wisdom Pet Medicine website using `requests` to retrieve content.
- **HTML Parsing**: Utilizes `BeautifulSoup` to parse and analyze HTML content.
- **Data Extraction**:
  - Finds and extracts specific elements like the site title, articles, and contact numbers.
  - Extracts featured testimonials and staff information.
  - Retrieves and lists all hyperlinks.
- **Data Storage**: Saves the formatted HTML content to a file for offline analysis.

## Key Functions
### Requests
- Sends an HTTP GET request to the Wisdom Pet Medicine website:
  ```python
  response = requests.get("https://wisdompetmed.com")
  print(response.headers)
  print(response.content)
  print(response.text)
  ```

### BeautifulSoup
- Parses the HTML response and extracts data:
  ```python
  soup = BeautifulSoup(response.text, 'html.parser')
  print(soup.prettify())
  ```
- Finds specific elements like the title and articles:
  ```python
  soup.find("title")
  soup.find_all("article")
  ```
- Extracts contact details, testimonials, and staff information:
  ```python
  print(soup.find("span", class_="phone").text)

  featured_testimonials = soup.find_all("div", class_="quote")
  for testimonial in featured_testimonials:
      print(testimonial.text)

  staff = soup.find_all("div", class_="info col-xs-8 col-xs-offset-2 col-sm-7 col-sm-offset-0 col-md-6 col-lg-8")
  for member in staff:
      print(member.text)
  ```
- Retrieves all hyperlinks:
  ```python
  links = soup.find_all("a")
  for link in links:
      print(link.text, link.get("href"))
  ```

- Saves the parsed HTML to a file:
  ```python
  with open("wisdom_vet.txt", "w", encoding="utf-8") as file:
      file.write(soup.prettify())
  ```

## File Structure
- `scraping.ipynb`: The main script for scraping the website.
- `wisdom_vet.txt`: File containing the formatted HTML content of the website.
