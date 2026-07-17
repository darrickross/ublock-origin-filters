# uBlock Origin Filters

Personal custom filter list for [uBlock Origin](https://github.com/gorhill/uBlock), used to sync my filters across every device/browser I use.

## Setup

Subscribe to this list once per device — uBlock Origin will periodically re-check the URL and pull in any updates automatically after that.

1. Open the uBlock Origin dashboard and go to the **Filter lists** tab.
2. Scroll to the bottom and click **Import...**.
3. Paste this raw URL on a fresh line:

   ```txt
   https://raw.githubusercontent.com/darrickross/ublock-origin-filters/main/my-ublock-static-filters.txt
   ```

4. Click **Apply changes** at the top of the dashboard.

You should then see the URL listed under **Custom**, just above **Import...**. Repeat on each device/browser profile you want kept in sync.

> **Note:** This only works because the repo is public — `raw.githubusercontent.com` can't serve private repo content to uBlock Origin.
>
> **⚠️ De-duplicate with "My filters" first.** If you previously pasted these same rules directly into uBlock Origin's built-in **My filters** tab, remove them from there before (or right after) subscribing to this list — otherwise every matching rule exists twice: once locally, once from this subscription.
>
> If the popup shows this list as **"X used out of Y"** and X seems lower than expected for the page you're on, check whether the missing rules are duplicated in **My filters**. uBlock Origin still applies the effect either way, but the count won't reflect this list's rules as the ones actually in use.

## Updating filters

Edit `my-ublock-static-filters.txt`, commit, and push to `main`. Each subscribed device will pick up the changes the next time uBlock Origin refreshes its lists (or force it immediately via **Filter lists → Update now** in the dashboard).

## Using this concept for your own filters

You can use this same approach to sync your own custom uBlock Origin filters across devices:

1. **Create a repo on GitHub and make it public.** This is required — `raw.githubusercontent.com` only serves files from public repos. uBlock Origin has no way to authenticate, so a private repo's raw URL will just 404.
2. **Add a plain-text file** with your filters (e.g. `my-filters.txt`), one rule per line, using standard [uBlock Origin filter syntax](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax).
3. **Commit and push** the file to your default branch (`main` or `master`).
4. **Build your raw URL** using this pattern:

   ```text
   https://raw.githubusercontent.com/<your-username>/<your-repo>/<branch>/<path-to-file>
   ```

5. **Subscribe to it in uBlock Origin** the same way described in [Setup](#setup) above (**Filter lists → Import... → paste raw URL → Apply changes**), using your own raw URL.
6. From then on, editing and pushing the file updates every device subscribed to it — no manual re-import needed.

**Requirements/limitations to keep in mind:**

- The repo (or at least the branch/file) must be **public**.
- Avoid committing anything sensitive to the repo — public means anyone can read the file, the commit history, and any other repo contents.
- uBlock Origin only re-fetches lists periodically (or on manual **Update now**), so changes aren't instant on every device.
