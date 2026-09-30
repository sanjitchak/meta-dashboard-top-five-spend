# Ads Manager static replica

A plain HTML, CSS and JavaScript dashboard based on the Sanjit Chrome profile’s **VSL - UV media** Ads Manager, with the August 2026 “sanjit” column preset. No database, Node.js server, framework, install, or build is needed.

## Open

Open `index.html` in a modern browser, or serve this folder:

```sh
python3 -m http.server 4173
```

Then open http://localhost:4173. All asset paths are relative, including scripts, images and fonts.

## GitHub Pages

1. Extract the GitHub Pages ZIP and upload all its files and the entire `assets` folder to a repository. Keep every runtime script included in the ZIP.
2. In repository **Settings → Pages**, select **Deploy from a branch**.
3. Select your branch and **/ (root)**, then save.

The ZIP contains these files at its root. There are no rewrite rules or environment variables. It supports repository subpaths such as `username.github.io/repository/`.

## Hostinger shared hosting

Upload the same files into `public_html` (or a subfolder) and open the domain. Node.js is unnecessary. Keep the `assets` directory beside `index.html`.

## Implemented interactions

- Campaigns, Ad sets and Ads tabs; searchable table; delivery views; selection; sorting; pinned columns; column resizing; ads pagination.
- Saved views, column presets, column selection and ordering, date picker, row density, conditional highlighting.
- Local create/edit/duplicate/status/delete/restore workflows; local draft review/publish and activity history.
- Campaign objective, budget and schedule forms; audience and placement fields; ad identity, text, URL, UTM and local image upload fields.
- Real CSV, XLSX and XLS exports; custom report name, summary totals and deleted records with delivery; JSON backup/restore, CSV import, print/PDF and local share link.
- Spend charts, comparison, local audience definitions, saved A/B test plans, manually executed local rules.
- Searchable library of 1,060 creatives (1,059 exported configurations plus one source-preview capture), with local artwork and thumbnails, original Facebook/Instagram preview links, source IDs and campaign/ad set labels.
- Reference-style two-month date picker, date presets, column sorting menus.
- Five-tab column customisation dialog with 150+ metric/settings choices, cross-tab search, collapse/expand, selected-column removal, drag/keyboard reorder and local saving.
- Seven source-inspected breakdown flyouts, searchable options, additional disabled choices, category selection and clearing. Aggregate metrics are explicitly marked as unsegmented.
- Navigation and reporting menus; backend-only services have explicit explanatory panels.

## Exactness and data coverage

The replica closely reconstructs the observed campaign screen, using downloaded reference branding, profile/account images and the Optimistic font. It is **not a verified pixel-for-pixel copy of every Meta screen or option**. Some icons are hand-built SVG equivalents; editor and secondary service panels are reconstructed local versions.

The source interface showed 47 campaigns, 172 ad sets and 1,854 ads. Meta’s exported reports included **33 campaigns, 126 ad sets and 378 ads**. An additional campaign visible on screen was transcribed, giving 34 local campaigns. Each exported level independently totals **₹925,836.40**. The local footer counts the rows actually available.

The initial performance reports lacked IDs. A second report identified all 146 spending ads by Ad ID; matching those records on name, spend, impressions and reach preserved the original metrics. Verified source identities are now available for 29 campaigns and 60 ad sets, enabling partial parent drill-down. Daily history and demographic breakdowns remain unavailable. A separate configuration export supplies 1,059 ad IDs, creative text and campaign/ad set relationships across 44 campaigns and 148 ad sets. Meta excluded ads using multiple text or headline variants. This library has 57 exact ID matches to spending ads. Other records remain separate; a name match is presented as a possible match, not as a verified identity. Videos are represented by exported thumbnails, not playable local video; placement layouts are approximate. These are not invented. Original imported rows stay accessible in their tabs; parent drill-down works for verified source relationships and newly created local records. Editor defaults are local form defaults, not verified live campaign settings. Alternate date ranges do not synthesize results. Import a report with matching `Reporting starts` / `Reporting ends` for another reporting period.

No action calls Meta or publishes an ad. “Publish locally” only applies local drafts. Rules only run on demand. Billing, account permissions, support and AI require Meta’s services. No login is collected.

**The package includes actual account report data and the reference profile image. Anyone who can access a hosted copy can read the bundled data.** Nothing has been deployed publicly by this task.

Local browser storage is specific to the origin/browser and is not shared between users. Export a JSON backup before clearing browser data or changing hosting domains.

## Verification

```sh
node --check app.js
node scripts/test.mjs
```

The dependency-free regression checks cover initial rendering, all three spend totals, search/filter/sort, CSV quoting, escaping, local status/publish/delete/restore, duplication resetting metrics, persistence, missing date behavior, column presets, and primary menu rendering. Creative checks additionally verify distinct IDs, all local thumbnail paths, preview rendering, ambiguous-name separation and URL validation. Browser checks covered the date and column menus and an exported creative preview at 1920 × 872. Full pixel-for-pixel coverage remains unverified.

## Asset provenance

Reference inspected and reports downloaded through Meta Ads Manager on 5 September 2026. `assets/meta.svg`, `assets/profile.jpg`, `assets/account.png` and `assets/reference-font-2.woff2` were downloaded from assets exposed by the reference page. Meta branding and font ownership remain with their respective owners. Spreadsheet export uses the locally bundled SheetJS 0.18.5 browser library; its Apache 2.0 license is included in `assets/vendor/xlsx-LICENSE.txt`. No tracking scripts or login credentials are included. Creative thumbnails are bundled locally; original preview and destination links open external pages.

### Ad preview update

`preview-modal.js` supplies the source-style preview modal with Facebook and Instagram cards, placement tabs, destination view, Share choices and verified performance details. The health-coach ad includes its original full-resolution artwork, Page avatar and source-observed identity/engagement. Other creatives retain their available exported media. Videos remain thumbnails. Device notifications require Meta and are disabled locally; advanced and placement layouts are approximations. Source data is a snapshot, with no live sync.

## Reusable company template

See [TEMPLATE.md](TEMPLATE.md). Edit `template/company.json`, supply three Meta CSV reports and optional creative JSON, then run `python3 scripts/build-company.py`. The builder produces a separate static site and ZIP, excluding this example company's reports and ad assets. Profile, account, currency, dates, preset name and browser storage are company-specific. `scripts/test-template.mjs` verifies the synthetic USD example, and `scripts/test-builder.py` checks invalid input rejection.

## Configuration records added
The tables now contain 47 campaigns, 170 ad sets and 1,163 ads. This includes 14 campaigns, 44 ad sets and 785 ads recovered from the configuration export whose identities did not overlap report IDs or names. Configuration-only metrics remain unavailable, not zero. The August performance reports still total ₹925,836.40 at each reporting level. Ambiguous name-only matches remain unresolved, so these counts do not establish complete source-account coverage.
