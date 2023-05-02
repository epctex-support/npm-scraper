# Actor - NPM Scraper

## NPM scraper

Since NPM doesn't provide a good and free API, this actor should help you to retrieve data from it.

The NPM data scraper supports the following features:

-   Search any keyword - You can search for any keyword and retrieve all the packages that you are seeking for. This feature also support special search syntax on the search such as `keyword:`

-   Scrape package detail - Extremely detailed and structured data for any package at your service. Get versions, name, maintainers, all the historical data and much more.

-   Get packages of a user - If you are looking for all the packages of a user, that is a one stop shop for you!

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/npm-scraper/issues).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on NPM that should be visited. Possible fields are:

- `search`: (Optional) (String) Keyword that you want to search on npmjs.

- `startUrls`: (Optional) (Array) List of URLs in NPM. You should only provide search, list, user detail or package detail URLs.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `customMapFunction`: (Optional) (String) Function that takes each objects handle as argument and returns object with executing the function.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Tip

When you want to have a scrape over a specific list URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the detail requests. If actor doesn't block very often it'll scrape 100 listings less than 1 minute with ~0.01-0.03 compute units.

### NPM Scraper Input example

```json
{
  "startUrls":[
    "https://www.npmjs.com/package/lodash",
    "https://www.npmjs.com/~ljharb",
    "https://www.npmjs.com/search?q=keywords:front-end&page=0&ranking=optimal",
    "https://www.npmjs.com/search?q=keywords:modules",
    "https://www.npmjs.com/search?q=axios"
  ],
  "endPage": 5,
  "maxItems": 100,
  "proxy":{
    "useApifyProxy":true
  }
}

```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## NPM Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this NPM actor.

## Scraped NPM Properties

The structure of each package in NPM looks like this:

### Package Detail

```json
{
  "url": "https://www.npmjs.com/package/lodash",
  "name": "lodash",
  "description": "Lodash modular utilities.",
  "maintainers": [
    {
      "name": "mathias",
      "avatars": {
        "small": "/npm-avatar/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdmF0YXJVUkwiOiJodHRwczovL3MuZ3JhdmF0YXIuY29tL2F2YXRhci8yNGUwOGE5ZWE4NGRlYjE3YWUxMjEwNzRkMGYxNzEyNT9zaXplPTUwJmRlZmF1bHQ9cmV0cm8ifQ.1nyQBg2LJRuQRWzQgT_g8Hru5FIUsz2mCZ3yqtIGbPQ",
        "medium": "/npm-avatar/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdmF0YXJVUkwiOiJodHRwczovL3MuZ3JhdmF0YXIuY29tL2F2YXRhci8yNGUwOGE5ZWE4NGRlYjE3YWUxMjEwNzRkMGYxNzEyNT9zaXplPTEwMCZkZWZhdWx0PXJldHJvIn0.8O30NcKyPpUc911dhXJuyBnrSQx-tLyHhFYFPIj5VcQ",
        "large": "/npm-avatar/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdmF0YXJVUkwiOiJodHRwczovL3MuZ3JhdmF0YXIuY29tL2F2YXRhci8yNGUwOGE5ZWE4NGRlYjE3YWUxMjEwNzRkMGYxNzEyNT9zaXplPTQ5NiZkZWZhdWx0PXJldHJvIn0.XJZ0JP62pAmmumlu-AeTCji3D_2wleGxXGc86Sl5f4A"
      }
    },
  ],
  "dist-tags": {
    "latest": "4.17.21"
  },
  "lastPublish": {
    "maintainer": "bnjmnt4n",
    "time": "2021-02-20T15:42:16.891Z"
  },
  "types": {
    "typescript": {
      "package": "@types/lodash"
    }
  },
  "dependents": {
    "dependentsCount": 171614,
    "dependentsTruncated": [
      "feebs-cli",
      "fashionista",
      "bless-brunch"
    ]
  },
  "downloads": [
    {
      "downloads": 38796856,
      "label": "2022-04-12 to 2022-04-18"
    },
  ],
  "author": {
    "name": "John-David Dalton",
    "avatars": {
      "small": "/npm-avatar/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdmF0YXJVUkwiOiJodHRwczovL3MuZ3JhdmF0YXIuY29tL2F2YXRhci8yOTlhM2Q4OTFmZjE5MjBiNjljMzY0ZDA2MTAwNzA0Mz9zaXplPTUwJmRlZmF1bHQ9cmV0cm8ifQ.B9Vy-ZZRADWO6SYXG9debouY1FRb7AMhNqg8rO76fOw",
      "medium": "/npm-avatar/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdmF0YXJVUkwiOiJodHRwczovL3MuZ3JhdmF0YXIuY29tL2F2YXRhci8yOTlhM2Q4OTFmZjE5MjBiNjljMzY0ZDA2MTAwNzA0Mz9zaXplPTEwMCZkZWZhdWx0PXJldHJvIn0.c1-LKdixh9shjLtVzpFB2qCaSFIyeMSRg89KtYrscAw",
      "large": "/npm-avatar/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdmF0YXJVUkwiOiJodHRwczovL3MuZ3JhdmF0YXIuY29tL2F2YXRhci8yOTlhM2Q4OTFmZjE5MjBiNjljMzY0ZDA2MTAwNzA0Mz9zaXplPTQ5NiZkZWZhdWx0PXJldHJvIn0.wTHgJF3dJNHDR2eKg8YGLK6neCgefwB7LCWcRPgQErw"
    }
  },
  "homepage": "https://lodash.com/",
  "keywords": [
    "modules",
    "stdlib",
    "util"
  ],
  "license": "MIT",
  "repository": "https://github.com/lodash/lodash",
  "versions": [
    {
      "version": "4.17.21",
      "date": {
        "ts": 1613835736891,
        "rel": "2 years ago"
      },
      "dist": {
        "integrity": "sha512-v2kDEe57lecTulaDIuNTPy3Ry4gLGJ6Z1O3vE1krgXZNrsQ+LFTGHVxVjcXPs17LhbZVGedAJv8XZ1tvj5FvSg==",
        "shasum": "679591c564c3bffaae8454cf0b3df370c3d6911c",
        "tarball": "https://registry.npmjs.org/lodash/-/lodash-4.17.21.tgz",
        "fileCount": 1054,
        "unpackedSize": 1412415,
        "npm-signature": "-----BEGIN PGP SIGNATURE-----\r\nVersion: OpenPGP.js v3.0.13\r\nComment: https://openpgpjs.org\r\n\r\nwsFcBAEBCAAQBQJgMS3ZCRA9TVsSAnZWagAA8+4P/jx+SJ6Ue5oAJjz0L7gw\nLDD5YvP8aoliFq4GYkwUXfVQvOwomIPfa+U5Kao/hDfuwFQ/Bq5D5nSsl2bj\nrjJgvlKXna0SId8AgDgY2fB7zSfninuJvalY4iTWMN8DFSpG0XE2QFfoKpd3\njDmuzcNtgr79QV6DgjOVkHiP1IGNDlLTc1QEKiwo/5CdGQi1q/iCj6dViQMJ\nByuuuV2Qzi3f/FI25cG797WZar1MHhhlcnB50HiVBGp54IZOyuqdqWPduZQo\nvhONtonxPGBm3/J+uAkeUSSyL3Ud+FzLvdg8WEI9gDL0yvU4k0FcsnOONEYn\nngLaKEsw2xAnPBYW3Lf73Jnpwx6FAT3k49kgzxiNYSxEo7x4wiuNtBoDMyNw\nEKj6SZ0bUNmaJgiMfDnnDjCKjI3JrO1hho8z6CkwuvxuWLlW9wSsVayggzAI\nEhfeTeISugVHh332oDY2MI/Ysu8MnVN8fGmqeYQBBFj3aWatuA2NvVjACnX/\n54G7FtCU8TxZpm9shFRSopBx8PeI3r+icx1CT8YVFypY416PLnidHyqtME1G\neuRd1nWEz18hvVUAEHmuvHo+EPP3tITmTTUPQcZGMdBcZC+4UBmPMWX466HE\nbHw4aOnUWMa0sWfsERC5xzRZAb4lgMPEoTOnZyN4usMy7x9TzGZKZvU24HUE\nmpae\r\n=NOmG\r\n-----END PGP SIGNATURE-----\r\n",
        "signatures": [
          {
            "keyid": "SHA256:jl3bwswu80PjjokCgh0o2w5c2U4LhQAE57gj9cz1kzA",
            "sig": "MEUCIF3Yithbtmy1aEBNlfNWbLswAfPIyQUuNUGARD3Ex2t4AiEA6TlN2ZKJCUpS/Sf2Z6MduF1BNSvayHIpu5wAcICcKXw="
          }
        ]
      }
    },
  ],
  "readme": "<h1>\n<a id=\"user-content-lodash-v41721\" class=\"anchor\" href=\"#lodash-v41721\" aria-hidden=\"true\"><span aria-hidden=\"true\" class=\"octicon octicon-link\"></span></a>lodash v4.17.21</h1>\n<p>The <a href=\"https://lodash.com/\" rel=\"nofollow\">Lodash</a> library exported as <a href=\"https://nodejs.org/\" rel=\"nofollow\">Node.js</a> modules.</p>\n<h2>\n<a id=\"user-content-installation\" class=\"anchor\" href=\"#installation\" aria-hidden=\"true\"><span aria-hidden=\"true\" class=\"octicon octicon-link\"></span></a>Installation</h2>\n<p>Using npm:</p>\n<div class=\"highlight highlight-source-shell\"><pre>$ npm i -g npm\n$ npm i --save lodash</pre></div>\n<p>In Node.js:</p>\n<div class=\"highlight highlight-source-js\"><pre><span class=\"pl-c\">// Load the full build.</span>\n<span class=\"pl-k\">var</span> <span class=\"pl-s1\">_</span> <span class=\"pl-c1\">=</span> <span class=\"pl-en\">require</span><span class=\"pl-kos\">(</span><span class=\"pl-s\">'lodash'</span><span class=\"pl-kos\">)</span><span class=\"pl-kos\">;</span>\n<span class=\"pl-c\">// Load the core build.</span>\n<span class=\"pl-k\">var</span> <span class=\"pl-s1\">_</span> <span class=\"pl-c1\">=</span> <span class=\"pl-en\">require</span><span class=\"pl-kos\">(</span><span class=\"pl-s\">'lodash/core'</span><span class=\"pl-kos\">)</span><span class=\"pl-kos\">;</span>\n<span class=\"pl-c\">// Load the FP build for immutable auto-curried iteratee-first data-last methods.</span>\n<span class=\"pl-k\">var</span> <span class=\"pl-s1\">fp</span> <span class=\"pl-c1\">=</span> <span class=\"pl-en\">require</span><span class=\"pl-kos\">(</span><span class=\"pl-s\">'lodash/fp'</span><span class=\"pl-kos\">)</span><span class=\"pl-kos\">;</span>\n\n<span class=\"pl-c\">// Load method categories.</span>\n<span class=\"pl-k\">var</span> <span class=\"pl-s1\">array</span> <span class=\"pl-c1\">=</span> <span class=\"pl-en\">require</span><span class=\"pl-kos\">(</span><span class=\"pl-s\">'lodash/array'</span><span class=\"pl-kos\">)</span><span class=\"pl-kos\">;</span>\n<span class=\"pl-k\">var</span> <span class=\"pl-s1\">object</span> <span class=\"pl-c1\">=</span> <span class=\"pl-en\">require</span><span class=\"pl-kos\">(</span><span class=\"pl-s\">'lodash/fp/object'</span><span class=\"pl-kos\">)</span><span class=\"pl-kos\">;</span>\n\n<span class=\"pl-c\">// Cherry-pick methods for smaller browserify/rollup/webpack bundles.</span>\n<span class=\"pl-k\">var</span> <span class=\"pl-s1\">at</span> <span class=\"pl-c1\">=</span> <span class=\"pl-en\">require</span><span class=\"pl-kos\">(</span><span class=\"pl-s\">'lodash/at'</span><span class=\"pl-kos\">)</span><span class=\"pl-kos\">;</span>\n<span class=\"pl-k\">var</span> <span class=\"pl-s1\">curryN</span> <span class=\"pl-c1\">=</span> <span class=\"pl-en\">require</span><span class=\"pl-kos\">(</span><span class=\"pl-s\">'lodash/fp/curryN'</span><span class=\"pl-kos\">)</span><span class=\"pl-kos\">;</span></pre></div>\n<p>See the <a href=\"https://github.com/lodash/lodash/tree/4.17.21-npm\">package source</a> for more details.</p>\n<p><strong>Note:</strong><br>\nInstall <a href=\"https://www.npmjs.com/package/n_\" rel=\"nofollow\">n_</a> for Lodash use in the Node.js &lt; 6 REPL.</p>\n<h2>\n<a id=\"user-content-support\" class=\"anchor\" href=\"#support\" aria-hidden=\"true\"><span aria-hidden=\"true\" class=\"octicon octicon-link\"></span></a>Support</h2>\n<p>Tested in Chrome 74-75, Firefox 66-67, IE 11, Edge 18, Safari 11-12, &amp; Node.js 8-12.<br>\nAutomated <a href=\"https://saucelabs.com/u/lodash\" rel=\"nofollow\">browser</a> &amp; <a href=\"https://travis-ci.org/lodash/lodash/\" rel=\"nofollow\">CI</a> test runs are available.</p>\n"
}
```
