# Bing Web Scraper in Go

This repository contains a simple Bing Web Scraper implemented in Go. The scraper fetches search results from Bing for a given query and parses the title, description, and URL of each result. It supports multiple pages, customizable result count per page, and optional proxy configuration.

## Features

- Fetch search results from Bing for a given query.
- Parse and extract result rank, title, description, and URL.
- Supports multiple pages and adjustable number of results per page.
- Includes optional proxy support for requests.
- Configurable backoff time between requests to avoid bans.

## Prerequisites

- Go installed on your machine (version 1.17 or higher recommended).

## Installation

1. Clone the repository:
    
    ```bash
    git clone https://github.com/your-username/bing-web-scraper.git
    cd bing-web-scraper
    
    ```
    
2. Install dependencies:
    
    ```bash
    go mod tidy
    
    ```
    

## Usage

The main entry point for the scraper is the `BingScrape` function, which takes the following parameters:

- `searchTerm` (string): The search query.
- `country` (string): Bing country code (e.g., `com`, `uk`, `in`).
- `proxyString` (interface{}): Optional proxy configuration (e.g., a string for proxy URL).
- `pages` (int): Number of pages to scrape.
- `count` (int): Number of results per page.
- `backoff` (int): Time (in seconds) to wait between requests.

### Example

Here's an example usage from the `main` function:

```go
func main() {
    res, err := BingScrape("Karthik H nair", "com", nil, 2, 10, 0)
    if err != nil {
        log.Println("Error in BingScrape")
    }

    for _, value := range res {
        fmt.Println(value)
        fmt.Println()
    }
}

```

This will fetch search results for the query `Karthik H nair` from Bing's US website (`.com`) for 2 pages with 10 results per page.

### Output Example

```
{1 https://in.linkedin.com/in/karthik-h-nair-0390b8290 Karthik H Nair - Coimbatore, Tamil Nadu, India - LinkedIn India Regenerate 2024 at Kumaraguru Institutions witnessed enriching sessions exploring regenerative soil… -- · Education: Kumaraguru College of Technology · Location: 641012 · 48 connections …}

{2 https://in.linkedin.com/in/karthik-h-nair Karthik H - Jaipur, Rajasthan, India | Professional Profile | LinkedIn Greetings! 👋 I'm Karthik H, a dynamic web developer with a keen interest in the MERN (MongoDB, Express.js, React.js, Node.js) stack. Currently enrolled at JECRC University, I am dedicated to...}
```

## Functions Overview

### `buildBingUrl`

Generates Bing search URLs based on the query, country, number of pages, and results per page.

### `getScrapeClient`

Creates an HTTP client with optional proxy support.

### `scrapeClientRequest`

Makes an HTTP request to Bing and handles the response.

### `bingResultParser`

Parses the Bing search results page and extracts the rank, title, URL, and description.

### `BingScrape`

The main function that coordinates the entire scraping process.

## Supported Bing Domains

The scraper supports multiple Bing country domains. Below is a list of supported country codes:

```
com, uk, us, tr, tw, ch, se, es, za, sa, ru, ph, pt, pl, cn, no, nz, nl, mx, my,
kr, jp, it, id, in, hk, de, fr, fi, dk, cl, ca, br, be, at, au, ar

```

## Dependencies

- [goquery](https://github.com/PuerkitoBio/goquery): For parsing HTML documents.

## Installation of Dependencies

Run the following command to install `goquery`:

```bash
go get -u github.com/PuerkitoBio/goquery

```

## Limitations

- Scraping too many pages too quickly may result in being temporarily banned by Bing.
- This implementation does not handle CAPTCHA or other advanced anti-scraping measures.
- Results are subject to Bing's search result formatting, which may change over time.

##