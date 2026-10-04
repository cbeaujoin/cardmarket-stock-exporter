# Privacy Policy — Cardmarket Stock Exporter

**Last updated:** 2026-10-04

## Summary

The extension works inside your browser and talks to one site only: `www.cardmarket.com`, in the tab where you are already logged in. It sends nothing to the developer or to any third party, and it contains no analytics or tracking.

It keeps two things on your computer: the interface language you chose and a cache of price figures that it reuses for 12 hours. The section "Where data is stored" describes both.

## What data the extension accesses

Every network request the extension makes goes to `https://www.cardmarket.com/*`, and it makes none until you click a button in the popup. When the popup opens, it only looks at the address of your Cardmarket tab to preselect the site language and the game.

### What it reads

- For a stock export, including the list of your sets, it loads your own stock pages. From each listing it takes the article ID, product ID, card name, expansion, rarity, language, condition, variant flags such as foil or reverse holo, comment, price and quantity, along with the links to the product page and the card image. It also reads the expansion and rarity filters of your stock page.
- If you tick "Load price trend + collector number" (off by default), it loads the Cardmarket product page of each product in the export and takes the price trend, the 1-day, 7-day and 30-day average prices and the collector number.
- For a want-list export it loads the overview of your want lists and the pages of each list. Per entry it takes the list name, Cardmarket's internal IDs for list, entry and card, the card name, expansion, accepted languages, minimum condition, attribute requirements, maximum price, quantity and the product link.
- For Bulk Update, and for editing or deleting wants, it reads the CSV file you select in the popup. For the rows it is about to compare or change, it loads the edit form Cardmarket shows for that listing or want and reads the current values from it. If the ID of a listing has changed since the export, it loads your stock page for that product to find the listing again.

### What it writes

The extension changes nothing on Cardmarket unless you select a CSV file, switch off Dry-Run (on by default) and confirm the warning dialog. It can then do the following:

- Change the price of a listing.
- Change the comment of a listing, if you tick "Update comments too". An empty CSV cell then deletes the comment on Cardmarket.
- Remove a listing whose `delete` column you set to `Y`.
- Change a want-list entry: accepted languages, minimum condition, attribute requirements, maximum price and quantity. It replaces only the fields you changed in the CSV and sends the rest of Cardmarket's form back as it was.
- Delete a want-list entry whose `delete` column you set to `Y`.

It does not create listings, want lists or want-list entries.

By default, price and comment changes go through Cardmarket's own edit dialog. The extension opens the dialog in your tab, enters the price (and the comment, if ticked) and submits it, so the other fields go back the way Cardmarket filled them in. With the optional Fast Mode it sends the edit request directly, without opening the dialog. That request contains the new price together with the listing's other fields. Language, condition and reverse-holo flag come from your CSV row. Quantity, the remaining flags and, unless you ticked the comment option, the comment are the values read from Cardmarket for the preview. Fast Mode therefore sends language, condition and reverse-holo flag as they stand in your CSV, even if the listing on Cardmarket has changed since the export.

### Login and account data

The requests come from your logged-in Cardmarket tab, so the browser attaches your existing session cookie. The extension does not read that cookie. It does read the security token Cardmarket places in its forms and sends it back with the form, as the site's own pages do.

The extension never asks for your password. It does not pick out, store or transmit your username, e-mail address, payment information or other account details.

## What data the extension collects

None. The extension:

- sends no data to any server other than `www.cardmarket.com`
- contains no analytics, tracking pixels or telemetry
- sets no cookies of its own
- uses no third-party SDKs or libraries that contact remote servers
- keeps no record of what you do, apart from the short-lived diagnostic output described in the next section

## Where data is stored

### CSV files

The extension builds an export in your browser and passes it to Chrome's download manager, which opens a Save As dialog. Chrome saves the file where you choose. The extension does not upload it anywhere.

The popup reads a CSV you select for an update. The extension uses its values for the requests to Cardmarket described above and does not keep the file.

### Extension storage

The extension keeps two entries in `chrome.storage.local`. They stay on your computer and are never transmitted.

- `uiLocale` holds the interface language you picked (Auto, DE or EN).
- `cmTrendCache` holds what the price-trend option looked up: for each product and print variant the price trend, the 1-day, 7-day and 30-day averages, the collector number and the time of the lookup, filed under the Cardmarket product ID (or the product page address if the ID is missing). An entry is reused for 12 hours. The extension removes older entries the next time it loads trend data, and the cache holds at most 40,000 entries.

Chrome deletes both when you remove the extension.

The extension does not use `localStorage`, `sessionStorage` or `IndexedDB`.

### In the Cardmarket tab

While a job runs, the extension keeps its progress and results in the memory of that tab. From the start of a Bulk Update run until the tab is reloaded, it also watches the requests made in the tab, because that is how it notices that Cardmarket has answered. It keeps the address, status code and first 500 characters of the last 50 responses in the tab's memory. Diagnostic messages, some with excerpts of the Cardmarket pages it has just read, go to the browser's developer console. All of this is gone once the tab is reloaded or closed.

## Permissions explained

| Permission | Reason |
|-----------|--------|
| `activeTab` | Access the current tab when you click the icon |
| `tabs` | Find your Cardmarket tab, also when the popup is pinned to a separate window. The extension only looks for tabs on `www.cardmarket.com` |
| `scripting` | Run the export, price-trend, update and want-list scripts in your Cardmarket tab |
| `downloads` | Pass the finished CSV to Chrome's download manager, which opens the Save As dialog |
| `storage` | Keep the interface language and the price-trend cache in `chrome.storage.local` |
| `host_permissions: https://www.cardmarket.com/*` | Work in tabs on `www.cardmarket.com`: load your stock, want-list and product pages there and submit the changes you confirm. No other site is covered |

## Third parties

The extension communicates only with `www.cardmarket.com`, the service you are already using. It contacts no third-party server.

The popup contains ordinary links: a PayPal donation button, the extension's review page in the Chrome Web Store, lupzn.de, the developer's GitHub profile and an e-mail address. The extension sends nothing to these sites. Nothing happens unless you click a link. The site then opens in a new tab, or your mail program opens for the address, and from there that site's own privacy policy applies.

## Changes to this policy

If this policy changes, the updated version will be committed to the GitHub repository and the "Last updated" date above will reflect the change.

## Contact

For privacy questions, open an issue on GitHub:
https://github.com/LUPZN/cardmarket-stock-exporter/issues

## Source code

The extension is open source. You are welcome to review the code at any time:
https://github.com/LUPZN/cardmarket-stock-exporter
