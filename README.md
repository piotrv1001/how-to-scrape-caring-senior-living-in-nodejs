# How to Scrape Caring.com Senior Living Facilities in Node.js

Use the [Caring.com Senior Living Scraper](https://apify.com/piotrv1001/caring-com-senior-living-scraper) through Apify's Node.js client. This example calls an existing Actor; it does not implement a scraper.

## What this example does

- Passes a small input to the Actor
- Waits for the run to finish
- Fetches the run's dataset
- Prints the returned rows

## Prerequisites

Node.js, an Apify account, and an Apify API token.

## Installation

```bash
npm install
```

## Environment setup

Copy `.env.example` to `.env` and replace the sample value with your Apify API token.

## Usage

```bash
npm start
```

The sample input is deliberately capped at 10 facilities. Edit `src/index.js` to change the URLs or limit.

## Code example

```js
import { ApifyClient } from 'apify-client';
import 'dotenv/config';

// Initialize the ApifyClient with your Apify API token
// Set APIFY_TOKEN in your .env file (copy .env.example to get started)
const client = new ApifyClient({
    token: process.env.APIFY_TOKEN,
});

// Prepare Actor input
const input = {
    "startUrls": [
        {
            "url": "https://www.caring.com/senior-living/assisted-living/california/los-angeles"
        }
    ],
    "maxItems": 10,
    "scrapeDetails": false
};

// Run the Actor and wait for it to finish
const run = await client.actor("piotrv1001/caring-com-senior-living-scraper").call(input);

// Fetch and print Actor results from the run's dataset (if any)
console.log('Results from dataset');
console.log(`💾 Check your data here: https://console.apify.com/storage/datasets/${run.defaultDatasetId}`);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach((item) => {
    console.dir(item);
});

// 📚 Want to learn more 📖? Go to → https://docs.apify.com/api/client/js/docs
```

## Example output

`sample-output.json` is an **illustrative shape**, not a captured run. The dataset can include facility name, care types, address, phone, rating, review count, and listed starting price. Fields may be absent when the source does not provide them. The current Actor and source page determine the actual output.

## Use cases

- Build a facility shortlist for one city
- Compare published care types and locations
- Review price and rating fields side by side
- Export facility URLs for further verification

## Try the Actor on Apify

**[Open the Caring.com Senior Living Scraper on Apify](https://apify.com/piotrv1001/caring-com-senior-living-scraper)**

## Related resources

- [Step-by-step blog guide](https://www.falconscrape.com/blog/how-to-compare-senior-living-facilities-in-one-city)

## License

MIT
