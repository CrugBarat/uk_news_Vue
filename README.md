<img src="https://github.com/CrugBarat/my_files/blob/master/uk_news/news1.png" width="300"> <img src="https://github.com/CrugBarat/my_files/blob/master/uk_news/news2.png" width="300"> <img src="https://github.com/CrugBarat/my_files/blob/master/uk_news/news3.png" width="300"> <img src="https://github.com/CrugBarat/my_files/blob/master/uk_news/news4.png" width="300"> <img src="https://github.com/CrugBarat/my_files/blob/master/uk_news/news5.png" width="300"> <img src="https://github.com/CrugBarat/my_files/blob/master/uk_news/news6.png" width="300">

# UK NEWS

UK NEWS is a search app, which uses an API as a data source.

**Programming Language**: JavaScript

**Web App Framework**: Vue

**Markup/Styling**: HTML5/CSS3

**HTTP client**: Axios

**Data Visualisation Library**: Google Charts

The UK NEWS app can dynamically search data requested from multiple APIs and return details stored for a corresponding result. It can filter through countries and cities in the UK and return a list of up-to-date news articles for the corresponding area. Each area uses a different request as a data source. The app can also return up to 100 articles for any given keyword via a search bar. There is a sports section which handles a different set of requests and data. There is a COVID-19 Update section, which uses a different API. This section uses goggle charts for data visualisation.

This exercise was tasked to me by CodeClan, Glasgow where I studied towards a PDA Level 8 in Professional Software Development. The exercise brief can be found below.

---

# Brief

Your task is to create an application that makes a request to an API and displays the data.

**MVP**

- The application should display data from an API request.
- The application should have a clear separation of concerns (multiple components)
- Take input from the user to update the page. You could update the page by filtering or manipulating the data on user interaction, or you might make further API requests to load more data that is then displayed.

**Extensions**

- Use a JS library that provides data visualisation.

---

# Setup

- Download/Clone files

- In Terminal

```
npm install
```

- Compile for development

```
npm run serve
```

- Click the link below to open project in browser

[LocalHost](http://localhost:8080/)

---

# Acknowledgements

**APIs used**

- [News API](https://newsapi.org/)
- [Postman - COVID19 API](https://documenter.getpostman.com/view/10808728/SzS8rjbc?version=latest)
