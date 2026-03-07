# Project 3 — Indexability & Crawlability Audit

## Website Audited

Books to Scrape (Demo Website)
https://books.toscrape.com

## Objective

The goal of this audit is to evaluate whether search engines can properly **crawl and index the website**. The audit focuses on critical technical SEO elements that influence crawlability and indexability.

---

# Tools Used

* Google Chrome Developer Tools
* Network Panel (HTTP Status Validation)
* Manual URL Inspection
* Spreadsheet Documentation

---

# Audit Scope

The audit analyzed the following SEO factors:

* robots.txt availability
* XML sitemap presence
* Meta robots directives
* Canonical tag implementation
* HTTP status codes

---

# Robots.txt Analysis

**URL Tested**

https://books.toscrape.com/robots.txt

**Result**

Status Code: 404 (Not Found)

### Analysis

The website does not provide a robots.txt file. Without this file, search engine crawlers are not restricted from accessing any part of the site.

### Impact

* Crawlers can access all URLs
* Crawl budget cannot be optimized
* No crawler control for sensitive directories

### Recommendation

Create a robots.txt file to control crawler access.

Example:

```
User-agent: *
Disallow: /admin/
Disallow: /cart/

Sitemap: https://domain.com/sitemap.xml
```

---

# XML Sitemap Analysis

**URLs Tested**

```
/sitemap
/sitemap.xml
/sitemap_index.xml
```

**Result**

All URLs returned **404 Not Found**

### Analysis

The website does not provide an XML sitemap. Sitemaps help search engines discover important pages more efficiently.

### Impact

* Slower discovery of new pages
* Reduced crawl efficiency

### Recommendation

Create a sitemap file:

```
https://domain.com/sitemap.xml
```

Example structure:

```
<urlset>
 <url>
  <loc>https://domain.com/</loc>
 </url>
</urlset>
```

---

# Meta Robots Analysis

Page inspected:

https://books.toscrape.com/

Meta robots tag detected:

```
<meta name="robots" content="NOARCHIVE,NOCACHE">
```

### Interpretation

| Directive | Meaning                        |
| --------- | ------------------------------ |
| NOARCHIVE | Prevents cached page display   |
| NOCACHE   | Prevents cached result display |

Important:

The tag **does not include "noindex"**, meaning the page remains **indexable**.

---

# Canonical Tag Analysis

Search performed for:

```
<link rel="canonical">
```

**Result**

No canonical tag found.

### Impact

Missing canonical tags may cause:

* Duplicate content signals
* Split ranking signals across similar URLs

### Recommendation

Add a self-referencing canonical tag.

Example:

```
<link rel="canonical" href="https://books.toscrape.com/">
```

---

# HTTP Status Code Validation

Page tested:

https://books.toscrape.com/catalogue/tipping-the-velvet_999/index.html

Result:

Status Code: **304 (Not Modified)**

### Interpretation

This indicates the browser used a cached version of the page. A 304 response is normal and does not negatively affect crawlability or indexability.

---

# Main Audit Table

| URL                                          | Status Code | Indexable | Robots.txt Allowed | Meta Robots       | Canonical | In Sitemap | Issue                 |
| -------------------------------------------- | ----------- | --------- | ------------------ | ----------------- | --------- | ---------- | --------------------- |
| /robots.txt                                  | 404         | N/A       | Yes (default)      | N/A               | N/A       | N/A        | Missing robots.txt    |
| /sitemap                                     | 404         | N/A       | Yes                | N/A               | N/A       | No         | XML sitemap not found |
| /sitemap.xml                                 | 404         | N/A       | Yes                | N/A               | N/A       | No         | XML sitemap missing   |
| /sitemap_index.xml                           | 404         | N/A       | Yes                | N/A               | N/A       | No         | Sitemap index missing |
| /                                            | 200         | Yes       | Yes                | NOARCHIVE,NOCACHE | Missing   | No         | Missing canonical tag |
| /catalogue/tipping-the-velvet_999/index.html | 304         | Yes       | Yes                | NOARCHIVE,NOCACHE | Missing   | No         | Missing canonical tag |

---

# Indexability Summary

| URL          | Crawlable | Indexable | Issue                 |
| ------------ | --------- | --------- | --------------------- |
| Homepage     | Yes       | Yes       | Missing canonical tag |
| robots.txt   | Yes       | N/A       | File missing          |
| sitemap.xml  | Yes       | N/A       | Sitemap missing       |
| Product page | Yes       | Yes       | Missing canonical tag |

---

# Key Findings

1. The website does not provide a **robots.txt file**.
2. No **XML sitemap** is available for search engines.
3. Pages lack **canonical tags**, which may create duplicate content risks.
4. Pages return valid **HTTP status codes (200 / 304)**.

---

# SEO Recommendations

| Issue                 | Recommendation                                    |
| --------------------- | ------------------------------------------------- |
| Missing robots.txt    | Create robots.txt file to control crawler access  |
| Missing XML sitemap   | Generate sitemap.xml and submit to search engines |
| Missing canonical tag | Add self-referencing canonical tags to pages      |

Example canonical implementation:

```
<link rel="canonical" href="https://books.toscrape.com/page">
```



