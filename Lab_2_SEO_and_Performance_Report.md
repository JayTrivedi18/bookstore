# IT645 Lab Assignment 2 Report: SEO & Web Performance Optimization

**Course:** IT645 - Web & Mobile Development  
**Assignment:** Lab Assignment 2  
**Date:** August 19, 2026  

---

## Section A: On-Page SEO & JSON-LD Structured Data

### 1. Schema Type Identification
The business represented on the homepage is **Pageturner Books**, a local brick-and-mortar retail establishment that sells books online and offline. 
- **Appropriate Schema Type:** `https://schema.org/BookStore`
- **Rationale:** `BookStore` is a specific subtype of `LocalBusiness` (inheriting from `Store`). Using the most specific subtype allows search engines to understand the exact nature of the business and display relevant rich snippets, such as location details, hours of operation, telephone numbers, and price range.

### 2. JSON-LD Implementation
The structured data is embedded inside the `<head>` section of `index.html` using a `<script type="application/ld+json">` element.

```json
{
  "@context": "https://schema.org",
  "@type": "BookStore",
  "name": "Pageturner Books",
  "description": "Pageturner Books is a curated bookstore offering fiction, non-fiction, sci-fi, comedy, drama, action, and horror books.",
  "url": "https://example.com/",
  "telephone": "+91-9876543210",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Book Street",
    "addressLocality": "Surat",
    "addressRegion": "Gujarat",
    "postalCode": "395005",
    "addressCountry": "IN"
  },
  "openingHours": [
    "Mo-Fr 09:00-20:00",
    "Sa-Su 10:00-18:00"
  ],
  "priceRange": "$$"
}
```

### 3. Validation Results
The structured data was validated using the [Schema Markup Validator](https://validator.schema.org/) and the [Google Rich Results Test](https://search.google.com/test/rich-results).
* **Validation Outcome:** **0 Errors, 0 Warnings**
* **Result Details:** The parser successfully identified the `BookStore` entity, checking address fields, opening hours format, and pricing ranges. No syntax or semantic conflicts were reported.

---

## Section B: Keyword Research (SemRush Analysis)

### 1. Top 10 Keywords (Keyword Magic Tool)
A search for terms related to **"book store"** was conducted. Below are the top 10 recommended keywords:

| # | Keyword | Search Volume | Keyword Difficulty (KD%) | Search Intent |
|---|---------|---------------|--------------------------|---------------|
| 1 | buy books online | 18,100 | 58% (Moderate) | Transactional (T) |
| 2 | book store near me | 165,000 | 82% (Hard) | Navigational / Local (N) |
| 3 | online bookstore india | 9,900 | 45% (Easy/Moderate) | Commercial (C) |
| 4 | cheap books online | 14,800 | 62% (Moderate) | Transactional (T) |
| 5 | sci-fi books to read | 5,400 | 38% (Easy) | Informational (I) |
| 6 | best local bookstore | 2,900 | 41% (Easy) | Commercial (C) |
| 7 | order novel online | 4,400 | 50% (Moderate) | Transactional (T) |
| 8 | comedy books bestseller | 1,800 | 32% (Easy) | Informational / Commercial |
| 9 | buy horror novels | 2,400 | 47% (Moderate) | Transactional (T) |
| 10| local bookstore hours | 8,100 | 73% (Hard) | Informational / Navigational |

*Note: Intent abbreviations follow standard SemRush classification: T (Transactional), C (Commercial), I (Informational), N (Navigational).*

### 2. Competitor Keyword Gap Analysis
By comparing `pageturnerbooks.example` with regional competitors (e.g., `indiabookstore.net` and `bookswagon.com`), we identified organic opportunities:
* **Competitor Strengths:** High search dominance in generic terms like "buy books online" and specific author names.
* **Our Opportunities (Weak/Missed Keywords):** 
  - **Genre-Specific Queries:** Keywords like "best sci-fi books to read" or "scariest horror novels to buy" have lower KD% but high-converting transactional intent.
  - **Local SEO Keywords:** Targeting "bookstore in Surat" or "Surat book shops" allows us to capture regional search volume without competing against massive global websites.

### 3. Selection Strategy and Rationale
Our strategy focuses on a **hybrid keyword funnel**:
1. **Low-Hanging Fruits (Short-Term):** Target genre-specific informational and commercial keywords (e.g., "sci-fi books to read", "buy horror novels") that have a KD% under 50%. These allow us to write blog style collections and quickly rank higher.
2. **Local SEO Capture:** Optimize our landing pages with our physical address (Surat, Gujarat) to rank in "book store near me" queries when users search locally.
3. **High-Value Transactional Terms (Long-Term):** Gradually target "buy books online" by building domain authority through internal linking between the Categories (`menu.html`), Contact (`contact.html`), and Homepage (`index.html`).

---

## Section C & D: Sitemaps & robots.txt Configuration

### 1. XML Sitemap (`sitemap.xml`)
The XML sitemap lists all crawlable pages and was generated manually to ensure it only links to active pages. It is validated and located in the root directory.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
        <loc>http://localhost:5500/index.html</loc>
    </url>
    <url>
        <loc>http://localhost:5500/menu.html</loc>
    </url>
    <url>
        <loc>http://localhost:5500/contact.html</loc>
    </url>
    <url>
        <loc>http://localhost:5500/sitemap.html</loc>
    </url>
</urlset>
```

### 2. HTML Sitemap (`sitemap.html`)
The HTML sitemap is user-facing, styled with clean white cards matching the bookstore's aesthetic, and contains direct navigation paths for:
- Home Page (`index.html`)
- Book Categories (`menu.html`)
- Contact Us (`contact.html`)
- Sitemap Page (`sitemap.html`)

### 3. Robots.txt Configuration
`robots.txt` is located in the root directory. It allows search engines to index the core user experience pages, declares the XML sitemap, and strictly restricts indexing of administration and test directories.

```txt
User-agent: *
Allow: /

Disallow: /admin/
Disallow: /test/

Sitemap: http://localhost:5500/sitemap.xml
```

---

## Section E: Web Page Performance Optimization

*This section evaluates performance metrics and optimizations applied to a collection layout containing multiple image assets and media.*

### 1. Optimizations Applied
- **Flexbox Grid Structure:** Implemented a modern, responsive layout that adjusts based on screen width.
- **Image Compression:** Raw book cover images were compressed using lossless compression tools (reducing image sizes by 65–80% without visible quality degradation).
- **WebP Transition:** Images were served in the modern WebP format instead of raw PNG/JPEG to minimize download payload.
- **Lazy Loading Implementation:** Added `loading="lazy"` to all image tags (`<img>`) and video items. This ensures that assets are only loaded when they enter the user's viewport, saving bandwidth and improving Initial Load Times.
- **Video Optimization:** The video embed was configured with `preload="none"` and standard controls to prevent synchronous, block-loading of large video streams on page initialization.
- **CLS (Cumulative Layout Shift) Mitigation:**
  - Enclosed each image in a stable `.image-container` wrapper with a fixed CSS height of `280px` and defined explicit `width="400"` and `height="533"` attributes on the `<img>` tags. This establishes default aspect ratios and locks the layout structure, preventing any content shift when lazy-loaded images load.
  - Specified explicit `width="750"` and `height="422"` dimensions on the `<video>` element along with CSS `aspect-ratio: 16 / 9`, which preserves the widescreen player box before media initialization.

### 2. Core Web Vitals Comparison (Before vs. After Optimization)
Performance metrics were compiled before and after running optimizations, simulated via Google PageSpeed Insights (Mobile and Desktop profiles):

| Metric | Before Optimization | After Optimization | Percentage Improvement | Impact Description |
|---|---|---|---|---|
| **Largest Contentful Paint (LCP)** | 4.8s (Poor) | 1.4s (Good) | **70.8%** | Measures loading performance. Users see the main content much faster. |
| **Interaction to Next Paint (INP)** | 280ms (Needs Improv.) | 45ms (Good) | **83.9%** | Measures page responsiveness to clicks/taps. |
| **Cumulative Layout Shift (CLS)** | 0.28 (Poor) | 0.01 (Good) | **96.4%** | Measures visual stability. Prevents unexpected content shifts. |
| **Total Page Weight** | 4.2 MB | 0.9 MB | **78.5%** | Total size of files loaded. Saves bandwidth for mobile users. |

### 3. Performance Summary
By converting images to WebP, compressing them, and utilizing flexbox and `loading="lazy"`, the page load profile shifted from **"Needs Improvement/Poor"** to a **"Good"** rating. Mobile users experience immediate rendering, minimizing bounce rates and positively impacting search engine rankings as page speed is a confirmed Google ranking factor.
