# Rebuild for another company

This template produces a separate static website and ZIP. Upload the generated files to GitHub Pages or shared hosting. No Node.js server or database is required. Python 3 is needed only on your computer when building.

1. Copy `template/company.json` and replace the company name, quoted account/business IDs, profile name, currency, country, dates and preset name. Optional `profileImage` and `accountImage` are local image paths relative to that JSON file.
2. Export three Meta reports for the same exact reporting range, without breakdowns. Save them in a folder as `campaigns.csv`, `adsets.csv`, `ads.csv`. Keep Meta's English column headings. Include Campaign ID, Ad set ID and Ad ID where available to link rows and previews. Keep IDs as full digits; do not let Excel convert them to scientific notation.
3. Optionally copy `template/example/creatives.json`, replacing the example with your creatives. `adId` must be `a:` followed by the exact Ad ID. Supply primary text, headline, destination and Page identity. Optional `image` and `pageAvatar` are local file paths relative to this JSON file. Only supplied creatives and images are included in the new site.
4. Run from the template folder:

```sh
python3 scripts/build-company.py \
  --config template/company.json \
  --reports template/example \
  --creatives template/example/creatives.json \
  --output output/example-company
```

Replace the input paths with yours. Omit `--creatives` when you have no creative data. Choose a new output directory for each build; existing directories are preserved. The command writes `output/example-company/` and `output/example-company.zip`.

The included Example Company CSVs are synthetic, with USD 42.50 spend, to demonstrate the format. Do not use them as real company results.

## Hosting

Upload the **contents** of the output folder to the root of a GitHub Pages repository, including `.nojekyll`, or to the chosen shared-hosting web directory. All runtime paths are relative and work under a GitHub project subpath. No build runs on the hosting server. The generated website is public wherever you publish it; publish only the report data you want visitors to see.

## Data rules

- Currency in CSV headings must match the configured currency. The builder normalizes internal metric keys; display and exports use the configured currency.
- Reporting dates must match across all inputs. Mixed date ranges and repeated object IDs are rejected, because they can double count totals.
- A new site's storage key includes account ID and report range, separating browser edits from other companies.
- Company-specific data, ad media, profile images and observed sample rows from the included VSL example are excluded from generated sites.
- Missing values remain unavailable. Do not infer account reach/frequency by adding ad rows. Optional `accountFrequency` can be set only when known from Meta's total row.
- Previews use supplied text and media. Layouts approximate Meta placements; videos in Meta exports are usually thumbnails. Live ad delivery, billing and notifications are not provided by a static template.
- Local editor changes remain in the browser. Use JSON backup for those changes; rebuild from source files for a new published snapshot.

`assets/company.js`, `assets/data.js`, and `assets/creatives.js` are the generated site's editable configuration and data files. Keep the full template folder if you intend to build again; the generated hosting ZIP contains runtime files only.

## Playable ad videos

Add `video` to a creative record to package a local MP4 or WebM. An optional `image` acts as its poster and report-table thumbnail. Paths are relative to the creative JSON file:

```json
{
  "adId": "a:333333333333333333",
  "name": "Your video ad",
  "page": "Your Company",
  "video": "media/ad-video.mp4",
  "image": "media/ad-poster.jpg",
  "copy": "Your exact ad text",
  "headline": "Your exact headline",
  "cta": "LEARN_MORE",
  "url": "https://example.com/"
}
```

The creative JSON must contain an array of records, as in the supplied example. Video previews have playback controls and do not autoplay. Browser playback depends on the file's codec; packaging preserves your original file. If you supply only a video thumbnail/ID, it remains a thumbnail. The builder does not fetch videos from Meta.

Report metrics must be finite, unformatted numbers. Invalid values such as `NaN`, currency-prefixed strings or thousands-separated strings are rejected with their row and column, instead of silently becoming zero.

## Conditional formatting

Use **Columns → Conditional formatting** to create, edit, disable or remove local rules. Single-colour rules support six comparisons; colour scales support eight palettes, flip and numeric/percentage boundaries. Rules apply to the chosen reporting level and remain active through filtering, sorting and reloads. Scale domains use the currently filtered rows. Later matching rules take precedence.

Formatting is stored under the company's account/date storage key and included in JSON backups. Optional `formattingRules` in company settings can provide initial rules using the same schema as a downloaded backup. It does not update the real Meta account.

## Explicit metric units

Custom metric names do not determine their units. Add optional `metricFormats` to company JSON when you know a metric's source format:

```json
"metricFormats": {
  "Video hook ratio": { "type": "ratio", "decimals": 2 },
  "CTR (all)": { "type": "percent", "decimals": 2 },
  "Custom score": { "type": "number", "decimals": 3 }
}
```

`ratio` displays 0.0963 as 9.63%; `percent` displays 0.9198 as 0.92%; `number` keeps the numeric scale; `currency` uses the company's currency. These settings affect display only. Exported values and conditional-formatting thresholds retain their original numeric units. New custom fields appear in Custom → Company metrics and can be selected as columns. Every configured field must exist in your CSVs. Account/object IDs cannot be formatted as metrics. Do not choose a unit from a metric's name or magnitude alone.

## Custom sorting

Open a column's sorting menu and choose **Customise sorting**. Select a primary column and optional “Then by” fields, change directions, and optionally show those columns first. Sort settings are saved with this company's browser state. Missing values stay last; long numeric IDs are compared without converting them to floating-point numbers. The local Delivery priority is Active, In draft, Campaign off, Off, or an optional `deliveryOrder` array in company settings. Meta-specific delivery priorities beyond these imported/local statuses have not been reproduced.

## Saved column presets

In Customise columns, edit the preset name and click Save. The name and full ordered column definition are now stored together. Use **Columns → View your column presets** to switch, edit, remove a local preset or reset an edited included preset. Saving under a new name keeps the previous preset available.

Presets are included in JSON backups and isolated by company/account/date. To include presets in a new static build, copy the backup's `columnPresets` object into company JSON. Values are arrays of report column keys, for example `"Lead report": ["Results", "Leads", "Amount spent (INR)"]`. The internal currency key remains `(INR)`; displayed currency follows the company settings.

### Updating reports in the browser
Choose Import local data and select the relevant campaign, ad set or ad level first. CSV files must use the configured currency and reporting period. Include full Campaign ID, Ad set ID and Ad ID columns to preserve hierarchy and match creative previews. Scientific notation IDs, malformed rows, duplicate IDs and non-numeric metrics are rejected before records change.

“Add new report records” rejects IDs already loaded. “Replace report records at this level” replaces report data while retaining local drafts; resolve pending edits to report records first. Matching IDs keep their local record identifiers. Reports without IDs cannot be deduplicated or matched reliably; use replacement for these. Company identity, currency, dates and packaged media are changed with the build-company script, not this report-import dialog.

Campaign and ad-set tables automatically hide the three ad relevance rankings and Ad schedule, while Ads retains them. Saved presets preserve the complete list when switching levels. Optional `hiddenColumnsByLevel` maps `campaigns`, `adsets` or `ads` to arrays of metric keys to override this behavior; an empty array displays every selected field. Spreadsheet exports follow the displayed level's columns.

Name filters are available under Search and filter → Name. Choose Campaign name, Ad set name or Ad name and one of the three contains operators. Enter one keyword per line. Filters combine with AND, persist in the browser and are included in JSON backups. Filtering across levels uses source parent names or verified parent/child IDs; missing relationships are excluded rather than guessed. A negative filter on child names keeps a parent only when all its known children exclude those terms.

ID filters are under Search and filter → ID. Choose Campaign, Ad set, Ad or Page ID, then `is` / `is not`. Add row creates an OR condition within the same scope; separate filter chips combine with AND. Use full digits, never scientific notation. Page IDs come from exact creative matches. Product catalogue filtering is disabled because the supplied snapshot has no catalogue IDs. Missing IDs do not satisfy negative conditions. Filters are included in browser saves and JSON backups.

Performance filters appear under Search and filter → Performance. Metrics unavailable in the loaded report are disabled. Select the object level and greater-than, less-than, inclusive-between, or outside-range comparison. Enter values in original report units, using the configured currency for money. Missing metrics are excluded rather than treated as zero. Separate chips combine with AND; a cross-level filter matches when a known related object meets the condition. Filters persist in browser storage and JSON backups.

Saved views capture the active level, reporting dates, parent selection, breakdown, delivery/name/ID/performance filters, query, columns and sorting. Opening a saved view clears row selections and restores an independent copy of these settings. Older views without advanced filters restore with those filters empty. Saving a view with the same name replaces that local view.

Name entry now uses keyword chips: press Enter to add the current phrase, remove it with ×, or paste multiple lines. Commas remain part of a name. Apply also includes unfinished input. The six most recent successful name filters appear in the editor and can be reopened for review before applying. Recent entries are stored separately in this browser and are not included in JSON backups.

Rows may contain an `exportedSettings` object for local editor defaults. Supported properties include objective, category, bid, start/end (ISO dates), minAge/maxAge, gender, location, event, pixel, headline, copy, description, url, page, instagram and cta. Explicit local row properties override these settings. The source-specific `enrich-editor-settings.py` utility attaches settings from a UTF-16 Meta configuration export using exact IDs only; it expects that export's month/day/year timestamps.

Imported editor fields without source values remain blank or show “Not available in export.” Local draft defaults apply only to new local records. Saving edits applies only fields changed since the editor opened; this also prevents bulk edits from copying the first row's unrelated settings onto other rows. An unchanged save creates no pending edits.

Creating an ad set or ad requires selecting an exact parent. Parent choices display the source ID where available, otherwise their stable local ID. New drafts inherit the known parent objective. Duplicated records receive fresh local IDs, retain parent relationships and copied settings, and start with no performance history; their original Meta identity is not reused. Duplicating a campaign currently duplicates its record only, not all descendants.

Hierarchy duplication is now supported: “Include linked ad sets and ads” copies all available descendants with verified parent links. Each copied tree uses new local IDs; descendants link to their own copied parents. The dialog shows available counts, which may be lower than Meta when the export lacks identities. Uncheck the option to duplicate only selected records. All copies remain local drafts with no performance history.

Keyboard shortcuts outside input fields: Ctrl+U opens the selected records' editor, Ctrl+I opens their local history, Ctrl+Y opens charts, and Ctrl+Backspace opens delete confirmation. Cmd is also accepted. No delete occurs until the dialog is confirmed. Local history records now carry record IDs and levels; selected history excludes legacy entries without IDs because identical names cannot establish identity.

### Objective filters
Search and filter > Objectives supports multiple values with is/not. Values include observed source choices and imported objective strings. Known settings and exact-ID campaign ancestry determine matches; unknown objectives are excluded. Filters persist in browser storage, saved views, and JSON backups.

### Selected-row filters
Select rows, then Search and filter > Filter selected rows only. The filter stores stable local record IDs independently of checkboxes and follows exact parent relationships across levels. Chips can be removed; saved views and JSON backups retain these filters. Unlinked records cannot be inferred by name.

### Import another company's editor settings

Pass a Meta configuration export alongside the three performance reports:

```sh
python3 scripts/build-company.py \
  --config template/company.json \
  --reports template/example \
  --configuration /path/to/company-configuration.csv \
  --creatives /path/to/company-creatives.json \
  --output /path/to/new-company-site
```

`--configuration` and `--creatives` are optional. Configuration input accepts UTF-8 CSV or UTF-16 tab-separated exports with `Campaign ID`, `Ad Set ID` and `Ad ID` columns. Numeric IDs and Meta's `cg:`, `c:` and `a:` prefixes are supported. Names never determine matches. The build summary reports `settingsMatched` for each level.

Known objectives, bid strategies, categories, ages, countries, gender, optimization events, pixels, schedule dates, headline, body, link description, link and CTA populate editor fields. Missing settings remain unavailable. This does not add configuration-only records or replace performance metrics, names or delivery status. Dates currently retain the calendar date; time-of-day scheduling is not implemented. Conflicting repeated settings, malformed IDs and unreadable dates stop the build before output creation. Images and playable videos still come from the separate creatives file.

### Previewing local edits
The table Preview action uses current saved local copy, headline, URL, CTA and identity. New drafts use the same placement preview window. Exact-ID source images remain at their original available resolution unless replaced in the editor. Edited previews omit source engagement counts and original-post share links. Imported performance remains historical and does not predict results for a locally edited draft. The creative library continues to show the original source snapshot.

### Delivery filters
Search and filter > Delivery supports is/not, multiple statuses and campaign/ad set/ad scope. It uses known delivery labels and exact relationships. Drafts includes local In draft records. Explicit same-level Deleted filters include locally deleted rows. Saved views and JSON backups retain the filters. Cross-level filtering only covers linked imported records.

The original creative library is available under **More > Ad creative library**. Select an ad and use **Preview** for its current local version.

### Pinned rows
Select one row and use More > Pin selected row or Unpin selected row. Pins are local display preferences and do not create campaign edits. They persist in this browser and JSON backups. Optional company.pinnedCampaignIds seeds initial campaign pins using exact Meta IDs; omit it for an unpinned company template.

Click the label of a Name, Performance, Objectives or Delivery filter chip to edit it. Apply replaces that filter; Cancel leaves its criteria unchanged. The separate × removes it.

ID filter chip labels are also editable. Existing OR rows and full-length IDs are preserved until Apply.

### Metric filter categories
Search and filter includes Performance, Engagement, Conversions and Custom metrics. The first three use observed Meta menu labels. For your own custom metric menu, add an optional `customFilterMetrics` array of exact report column names to company configuration. Keys from `metricFormats` also appear, using their configured labels. Source-company custom metric labels are not built into the shared runtime. Metrics without numeric data at the selected level are visible but disabled; values retain their original report units.

### Performance goal settings
Optional configuration imports now retain `Optimization Goal` as `exportedSettings.performanceGoal`. The Performance goal filter uses exact ad-set ancestry for campaigns and ads, never similar names. Six observed export enum values are mapped to their corresponding menu labels; exact menu labels also work. Unknown values remain unavailable and do not qualify for negative filters. No objective or performance goal is inferred from a campaign name.
