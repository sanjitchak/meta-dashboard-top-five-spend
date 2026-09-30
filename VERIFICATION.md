# Fidelity and coverage audit

Last inspected: 5 September 2026.

## Verified in the live browser

- Reference account: VSL - UV media, 167142780053170, Sanjit Chrome profile.
- The reference date selector opens a right-aligned popover with two calendars, a Recently used section, thirteen date presets, Compare, preset selection, date inputs, Pacific Time note, Cancel and Update.
- The replica now includes that structure and those presets. Browser inspection verified it opens and displays August and September 2026 with the August range selected.
- Reference-sized 1920 × 872 inspection identified row-height drift; cell padding was corrected to the observed 46 px rhythm.
- The replica column menu opens, Customise columns opens, and searching “leads” filters the available metric checkboxes.
- No errors were reported by the local browser console during these checks.

## Logic checks

`node scripts/test.mjs` passes. It covers imported totals, local changes, the date preset calculations including year rollover, reverse date selection, sorting submenu actions and removing columns.

## Remaining work (not completion claims)

- Full ad configuration export is being collected to add actual creatives and hierarchy.
- Complete secondary-menu inventory and screenshot comparisons are still required.
- All campaign/ad set/ad records and previews are not yet represented.
- Browser-only local simulation cannot perform live Meta billing, delivery, permissions, or backend reporting.

The goal is not marked complete by these checks.

## Creative export update

- Configuration export finished with Meta warning that ads using multiple text/headline variants were excluded.
- Imported 1,059 distinct ad IDs, 44 campaign IDs and 148 ad set IDs into a separate searchable creative library.
- Downloaded all 127 unique exported video thumbnail URLs as local JPEGs; zero failures.
- Browser verified an original exported ad thumbnail and copy, placement selector and original preview links.
- Regression checks verify library counts, local asset existence, preview routing, duplicate-name separation and safe external URL schemes.
- Remaining: omitted creative records, playable videos, performance-to-ID joins and exhaustive option/layout parity. The goal remains incomplete.

## Breakdown fidelity update

Inspected every category flyout in the live Sanjit reference: Time, Demographics, Geography, Delivery, Action, Creative and Attribution. Replaced reconstructed lists with observed labels, added flyout navigation and the account-specific disabled additional options. Browser screenshots verified corrected alignment and wrapping; selecting Platform updated the local state, with no console errors. Logic checks covered category replacement, combined categories, invalid selections and clearing. No segmented metric data was invented.

## Column customisation update

Read the source Key metrics, Tracking, Ad settings, Advanced and Custom tabs. Rebuilt the two-panel dialog with grouped metrics, search, tab switching, collapse/expand, selection removal, drag and keyboard reordering, preset renaming and local save. Browser verified Ad ID search and adding it changed the count from 31 to 32; cancelled after QA to preserve the current local report. Logic tests covered reorder/remove/save and exact string rendering of IDs. Added columns without imported values render unavailable. Source preset includes four additional selected fields and nested conversion choices; matching those defaults and the conversion grid remains outstanding. No Meta preset was saved or changed.

## Performance identity and parent linking

Exported a temporary unsaved Performance view with Ad ID, Ad set ID, Campaign ID and names; restored the original sanjit preset afterward. Meta omitted the requested creative text/Page/preview fields from this report. The report includes 146 spending ads and totals INR 925,836.40. All 146 match uniquely against the initial report by name, spend, impressions and reach. Added 29 verified campaign identities and 60 ad set identities; one duplicate-name ad set was resolved using additive spend and impressions from the ID report. Joined 57 spending ads to creative configurations by exact ID. Copied six source table thumbnails (46px) and verified their visual mapping. Browser QA confirmed campaign -> Combined adsets -> eight spending ads -> occult5 preview with exact ID and INR 49,949.57 spend. No Meta ad or preset was saved.

## Spreadsheet export update

Added source-matched CSV/XLSX quick export choices and the custom CSV/XLSX/XLS format dialog, report naming, summary totals and deleted records with delivery. Exports use locally bundled SheetJS; no runtime CDN/server dependency. Workbook write/read tests verify XLSX and BIFF8/XLS format validity, INR 925,836.40 summary total and long Ad IDs preserved as strings. Verified selected-row handling, exclusions, deleted-record inclusion and CSV formula protection. Browser QA selected XLSX with summary totals and invoked Export without runtime errors.

## Source ad-preview modal update

Inspected the health-coach ad's Ad/Destination tabs and Share menu in Sanjit's account, without editing the ad or sending notifications. Downloaded its source 1024px artwork and 200px Page avatar. Its exact ID alone now has the observed Varun Gera / videovarun identities, headline, 18 reactions and 5 comments. Rebuilt previews as a 600px modal with Facebook/Instagram cards, four placement groups, expandable copy, original links, share menu, destination tab and expandable verified performance. Destination reproduces the observed Facebook browser layout and WhatsApp contact strip; it does not send messages. Browser verified the feed and destination appearance and switching to vertical placement. Tests verify identity, original image, INR 4,986.74 spend, destination fields, share availability and no engagement leakage to another ad. Full placement rendering, creative variations and advanced-preview parity remain incomplete; unavailable device notification actions are visibly disabled. All regression checks pass.

Also inspected the source Advanced preview gallery and added its full-screen structure, named placement gallery and four working group filters. Browser QA confirmed the gallery renders with source artwork and returns to the standard modal. Fifteen named placement layouts are available; generated aspect-ratio variations and placement-specific rendering remain approximate.

## Default columns and conversion editor parity

Re-inspected the source sanjit preset and its 35-column selection on 5 September. Added Conversion rate ranking, Engagement rate ranking, Ad schedule and Quality ranking at the observed positions, including diagnostic subtitles. Existing exported rankings now render; unavailable Ad schedule stays blank. Upgrades only the untouched legacy default layout. Added the source Total/Value/Cost conversion grid and nested Leads/Purchases subcategory checkboxes, grouped reorder and group removal. Tests verify 35 columns, values, search, disabled cells, child ordering and removal. Source dialog was cancelled without saving.

## Reusable company builds

Moved account/profile/currency/date/preset/source-specific rows and ordering into assets/company.js. Added a Python build-time utility accepting company JSON, three Meta CSVs and optional creative JSON/local media. Generated sites contain HTML/CSS/JS only. Tested a separate synthetic Example Company with July data and USD 42.50: exact long IDs, hierarchy links, currency labels in exports, local storage isolation and missing-metric handling all passed. Browser verified the generated site at a nested URL, campaign-to-ad-set-to-ad navigation and company-specific preview. Original VSL data/creative media are excluded from the new site. Builder rejects currency/date mismatches, duplicate IDs and numeric account IDs before creating output. Full Meta option/placement parity remains incomplete as documented above.

## Reusable media support and input validation

Added optional company-supplied MP4/WebM media to native preview controls with `preload=none`, inline playback, optional posters and no autoplay. Advanced placement layouts keep video controls unobstructed. Builder copies video/poster files and joins report thumbnails by exact Ad ID. Tests verify byte-preserving media packaging, thumbnail ID join, no sample-media inclusion and rendered playback controls; actual codec playback has not been verified. Added finite numeric input validation to prevent malformed company metrics from silently displaying as zero. Opportunity-score and notification panels now use company configuration; fixed a literal template-expression rendering bug in the score drawer. Original Meta videos are still not retrieved.

## Conditional formatting controls

Read the source formatting sidebar, Single colour/Colour scale modes, six comparison operators, four solid colours, eight scale palettes and minimum boundary choices. Cancelled the source draft and verified no rule was saved. Added a matching local sidebar with saved rules, event scope, editing/removal, enable toggles, palettes, flip and boundaries. Browser saved Results > 500, reloaded and visually verified only the 921-result cell highlighted; removed that QA rule afterward. Tests cover six operators, zero versus missing values, scales, midpoint, flip, invalid input, redraw persistence and backup restoration. Scale domains follow filtered rows; advanced source placement/other unimplemented option gaps remain open.

## 48hours3 source media and copy recovery

Opened only the second source ad (48hours3) in account 167142780053170, verified its existing report ID a:52556456798368, and inspected Ad preview. Recovered a 1024 × 1024 JPEG, full primary text, headline, See details CTA, Varun Gera/videovarun identities and six reactions. A smaller rendition failed download; the 1024px asset succeeded and was visually compared with the source. Added one preview-sourced creative, bringing the library to 1,060 IDs and exact spending-ad creative matches to 58. Destination URL and comment count remain unavailable and are not invented. Browser verified the updated preview and original INR 6,554.06 spend. Source preview was closed without ad changes. No playable video was exposed for this image ad.

## Custom metric unit audit and template controls

Inspected raw Hook Rate/Hold Rate/CTR/Link to LP values and the source Custom metric catalog. Hook/Hold definitions were not exposed by the accessible controls used in this pass; a horizontal header scroll did not synchronize source row cells, so it was not reliable evidence of displayed units. No source metric or preset was saved, and the current sample rates were not rescaled. Added explicit company metricFormats for number, percent, ratio and currency with precision and missing-value handling. Added custom field catalog entries and builder validation for field presence, numeric values, precision and identity-field exclusion. Tests verify ratio versus percentage units and unchanged raw values. Exact source custom-rate display units remain unverified.

## Customise sorting

Inspected Meta's Customise sorting dialog from Delivery: primary Delivery sort, secondary Off/On sort, per-field directions, Add sorting option, and checked Show columns in this order. Cancelled without saving source changes. Implemented a corresponding local dialog and stable multi-field comparator, duplicate-field validation, column ordering and company-specific browser persistence. Tests cover numeric ties, names, missing values, exact long-ID sorting, persistence and editor add/remove/direction changes. Browser verified the dialog and addition of a third sorting field, then cancelled. Source-specific priority ranking beyond the available local statuses remains approximate.

## Saved column preset lifecycle

Fixed a code-confirmed gap: saving a named custom preset previously persisted only its active name/columns, leaving no selectable preset definition after switching away. Added company-scoped preset definitions, switching, manager UI, edit, remove/reset and JSON backup restoration. Included preset defaults are retained for reset. Legacy active custom layouts are registered on load. Names and fields are validated, and names are escaped in menus and the header. Tests cover save/switch/restore, invalid keys, reserved names, escaped markup, remove and included-preset reset. Browser verified the preset manager's names, column counts and actions. This manager is a functional local implementation; its complete visual parity with Meta's manager has not been verified.

### Highest-spend video preview enrichment (2026-09-05)
- Read-only source inspection: VSL - UV media account 167142780053170, campaign [Combined Ad sets] Winning Ads UPdated - 9 june 2026, Combined adsets, AD no 3 #7 hook 2 – Copy 4; source August spend ₹483,325.29 and 508 purchases identify the exported row a:52529889643968.
- Source preview displays headline Get High-Ticket Clients Organically, Varun Gera / videovarun verified identity, 1:07 video duration, Saranya M Vinoth and 2.3K others, 183 comments, 119 shares. Stored the reaction label verbatim rather than inventing an exact numeric count from its abbreviation.
- Added independent reaction/comment/share rendering, including counts without a reaction field and HTML escaping. Dependency-free suite passes.
- Current CUA tab has no pageAssets capability; original video and full poster remain unavailable. Source preview closed without editing or publishing. Visual layout for three engagement fields still needs browser comparison.

### Browser CSV import correctness (2026-09-05)
- Replaced the legacy import that discarded Meta IDs and forced all rows off. Import now validates report shape, currency, dates, finite numeric metrics and full digit IDs before mutation; duplicate source IDs and append conflicts are rejected.
- Full IDs join creative images and parent rows. Delivery is read from the report, with unknown state explicitly labelled. Added append/replace modes; replacement retains local drafts and existing local IDs for matching source IDs, and rejects replacement of pending report edits.
- Tests cover malformed CSV/duplicate headers, invalid scientific IDs, currency/date/numeric mismatch, exact preview joins, duplicate prevention with unchanged data, replacement and parent links. Full suite passes. Browser visual verification of import dialog remains pending; no source Meta interaction in this change.

### Level-specific source column fidelity (2026-09-05)
- Source campaign and Combined adsets header inventories observed during the prior read-only session omit Conversion rate ranking, Engagement rate ranking, Quality ranking and Ad schedule, while Ads includes them.
- Added level-specific display filtering without changing saved preset definitions; report exports follow the displayed fields. Browser campaign header inventory now confirms the four omitted fields, retained order and remaining metric headers. Corrected literal Off... to Off/On.
- Browser import dialog verified file picker and Add/Replace report mode. Downloadable import template now uses configured currency and reporting dates and provides full ID columns; USD template round-trip passes validation. Date-unavailable message no longer promises unsupported cross-period browser imports.
- Full automated suite passes, including level switch/export checks. Complete source data/media and service parity remain unverified/incomplete.

### Name filter source inspection and implementation (2026-09-05)
- Read-only source search menu exposes Name, ID, Objectives, Delivery, Campaign setup, Performance goal, metric groups and recent filters. Inspected Name: object level selector, contains all of / contains any of / doesn't contain any of, Cancel and Apply. Cancelled without applying a source filter.
- Implemented the three Name operators for all three levels, case-insensitive keywords, multiple AND-combined removable chips, browser persistence and JSON backup restoration. Relations use exported parent names and exact parent/child IDs. Missing relationships do not satisfy a negative condition.
- Browser QA: Campaign name contains all of Retargeting Scheduled produces exactly one campaign with ₹32,983.50 spent; removed QA chip afterward. Automated tests verify operators, hierarchy, missing-parent exclusion, chips and persistence.
- Name editor currently uses a modal and newline terms; source uses a popover/token input. Other source filter categories and recent-filter UI remain incomplete. Cross-level negative semantics are a documented local rule, not source-verified behavior.

### Source ID filter (2026-09-05)
- Inspected source ID dialog in account 167142780053170: Where, Campaign/Ad set/Ad/Page/Product catalogue ID, is/is not, Add row, Or, disabled repeated scope, Delete row, Cancel and Apply. Cancelled source dialog without applying a filter or changing ads.
- Implemented exact-string ID filters, same-scope OR rows, scope locking, removal, validation, chips, persistence and validated JSON backup restoration. Page scope joins creatives by exact ad ID; catalogue option disabled due absent export data.
- Automated checks distinguish 18-digit IDs differing by their final digit, reject numeric/scientific IDs, verify Page ID joins, campaign descendant matching, OR and negative conditions, and the ₹483,325.29 spending-ad result.
- Browser ID dialog verified. Ad ID 52529889643968 on Campaigns returns only its verified parent campaign; removed QA filter afterward. Negative filtering across multiple descendants uses all known IDs; incomplete relation/source data limits this result and exact Meta equivalence remains unverified.

### Performance metric filtering (2026-09-05)
- Source inspected read-only: Performance category lists 26 metrics. Amount spent editor offers Campaign/Ad set/Ad level and is greater than, is less than, is between, isn't between. Source dialog cancelled.
- Implemented source Performance list with absent metrics disabled, numeric editor, range controls, removable chips, storage/backup support and parent/child report matching. Missing metrics excluded; zero retained. Range boundaries are inclusive locally; exact source boundary behavior remains unverified.
- Tests cover four comparisons/boundaries, missing/zero, invalid ranges/nonfinite values, parent metrics, chips and persistence. Spend > 0 returns 3 campaigns totalling ₹925,836.40. Browser confirmed editor labels; fixed field CSS so maximum value is hidden for single-value operators.
- Rebuilt independent USD company successfully and verified currency, long IDs, dates, preview, storage isolation and absence of original account data. That template build preceded the latest metric-filter addition; final package carries updated runtime.
- Source popover layout, remaining filter categories and full data/media parity remain incomplete.

### Anchored filter editors and visual QA (2026-09-05)
- Name and performance editors now open in a 430px popover beneath the search bar, replacing the blocking center dialog. ID remains a dialog, matching the distinct observed source presentation.
- Editor actions preserve the popover while validating; successful apply and Cancel close it. Browser verified blank Name Apply leaves editor open.
- Screenshot inspection confirmed final anchored placement, single-row title/close control, source-style field spacing and right-aligned footer. Initial screenshot exposed stale CSS; versioned stylesheet URL forces the refreshed layout on hosted copies. Asset existence test now strips URL query/hash when resolving local files.
- Full test suite passes. Token-based name entry and exact source dimensions remain unfinished; current editor retains newline-based keyword input.

### Complete saved-view restoration (2026-09-05)
- Fixed views omitting newly added name, ID and performance filters, level/date selection, parent, breakdown and sorting. Snapshots and restored arrays are deep copies, preventing later edits from mutating saved views.
- Restores known columns, valid sort rules/date ranges and validated filters; older view definitions default missing advanced filters to empty. View menu names are escaped and action names encoded.
- Automated suite validates combined filters resolving the highest-spend ad, restored level/sorting, deep-copy independence, legacy and malformed view inputs. Browser saved a Retargeting Scheduled filter, cleared it, reopened the saved view and verified exactly one campaign at ₹32,983.50; removed the QA view and filter afterward.
- Latest runtime rebuilt for independent USD example at /tmp/meta-template-views-check-20260905; template checks pass for currency, exact IDs, reporting dates, hierarchy, preview and source-account exclusion. Full source parity remains incomplete.

### Name keyword chips and recent filters (2026-09-05)
- Replaced multiline name entry with removable keyword chips, Enter-to-add, multiline paste, empty-input Backspace removal and pending-input inclusion on Apply. Deduplicates keywords case-insensitively while preserving commas in names.
- Added six recent successful name filters with duplicate suppression and click-to-reopen level/operator/keywords. Recent history is local browser state and separate from exported backups.
- Automated tests cover parsing, comma retention, deduplication, escaping, removal, recent order/limit and pending-token apply. Full suite passes.
- Browser applied Retargeting Scheduled, cleared active filter, reopened its recent entry, visually confirmed chip layout, removed the chip and cancelled. No active QA filter remains; the recent entry remains as a truthful local usage entry. Source exact dimensions and other category parity remain incomplete.

### Configuration/report reconciliation (2026-09-05)
- Reconciled UTF-16 configuration export export_20260905_1657.csv against original report rows, using full canonical IDs and excluding any unresolved name overlap. Added 14 campaigns, 44 ad sets and 785 ads. Totals: 47 campaigns, 170 ad sets, 1,163 ads. Source observed 47/172/1,854; equal campaign count alone does not prove full identity parity.
- Kept 2 campaign, 45 ad-set and 217 creative ID/name overlaps unresolved. The 232 zero-spend ad report rows lack parent identity fields; no name-only identity was guessed.
- Configuration records preserve IDs, parent names/IDs, observed statuses and selected configuration fields. Missing report metrics remain absent; table/export/preview show unavailable rather than zero. Active child configurations under paused campaigns show Campaign off.
- Reconciliation script is repeatable: second run added zero duplicate records. Stable configuration row IDs and a one-time source revision migration append new source entities into old browser saves while preserving existing local edits. Replaced the former screen-only Combined Winning Ads placeholder using its stable local ID.
- Full suite passes, including unchanged ₹925,836.40 totals, 146 identified spending ads / 58 matched spending creatives, real spreadsheet round trips with added blank-metric records, and configuration preview missing-data checks.
- Browser migration shows 47 campaigns; newly added 1.2lacclosed appears with blank metrics and opens its exact creative preview. Full source data/media coverage remains incomplete.

### Editor settings from exact configuration IDs (2026-09-05)
- Attached exportedSettings to 42 campaigns, 103 ad sets and 842 ads using exact source IDs; no name matching. Preserved known campaign objectives, bid strategies, categories, audience ages/country/gender, event/pixel, schedule dates, and matched creative text/identity/destination.
- Source export date format is month/day/year with 12-hour time; Combined adsets 06/09/2026 maps to June 9, consistent with its named campaign. Date-only editor still omits time-of-day fidelity.
- Editor resolves exportedSettings beneath local row overrides. Dropdowns retain imported values absent from the default list, and imported minimum ages below 18 remain valid. Saving an unchanged inherited delivery status now preserves the ad's existing on/off value.
- Automated checks verify settings counts, exact ages/pixel/event/headline/start date, local edit precedence and source enum retention. Browser confirmed highest-spend ad ages 30–60, pixel 590340749861931, PURCHASE, June 9 start and full headline; closed without saving.
- Unexported fields may still use legacy editor defaults, and full source editor layout/options are incomplete. Exact-source configuration remains distinct from August performance data. Latest full test suite passes.

### Editor defaults and change-only saves (2026-09-05)
- Imported records no longer receive guessed Sales objective, None category, snapshot start date, country, 18/65 ages or the first available dropdown option. Missing selectors show Not available in export; missing text/date/age fields stay blank. Local newly created drafts retain their defaults.
- Captures editor field baseline on opening and applies only changed fields. Unchanged saves do not add pending edits. Bulk updates preserve per-row settings that were not edited. Target level is captured when opening the drawer, and changes retain that level in the pending list.
- Inherited on/off remains unchanged when its delivery label is untouched. Numeric budget type selection requires a supplied amount. Tests cover no-op, single-field and bulk preservation, unknown values and local-default distinction.
- Browser opened the highest-spend ad, confirmed absent locations/settings remain blank while source age 30 persists, saved unchanged, and observed No settings changed with Review and publish disabled. Full suite passes.

### Parent identity and draft duplication (2026-09-05)
- Creation parent selectors now store local record IDs and display source IDs (or local IDs when unknown), replacing first-name-match lookup. Requires a valid selected parent, inherits its known objective, and carries verified ancestor IDs/names. Existing parent context is preselected when available.
- Local duplicate records receive fresh local IDs and no copied own Meta ID. Parent links are retained, source editor settings are copied into the draft, and performance resets. Configuration-only provenance is removed from new local copies.
- Tests verify duplicate-name parent selection, exact inherited parent/objective, missing-parent rejection, original Meta ID removal, parent preservation and copied creative settings. Full suite passes.
- Browser creation dialog distinguishes both Polar Elite Academy campaign IDs and the two unresolved Brandpreneur rows by their local IDs. Cancelled without creating QA records. Campaign duplication still does not clone its full descendant hierarchy; full Meta duplicate-flow parity remains incomplete.

### Verified hierarchy duplication (2026-09-05)
- Added Include linked ad sets and ads, enabled by default for parent records. The dialog displays available copy counts and updates totals with copy count/child choice. Source Combined campaign currently has one verified ad set and eight linked ads in this dataset; its two other observed ads remain unlinked.
- Duplicate plans are built without mutating source rows. Each copy gets fresh local IDs; child parentId links point to its new copied parent. Copied parent Meta IDs are removed from descendants, while an ad-set copy retains its unchanged source campaign ancestry. Draft metrics and raw source delivery fields reset.
- Commits all planned levels with correctly scoped pending entries, persists once and selects only copied roots. Tests cover two independent trees, source immutability, settings preservation, identifier removal, ancestry, record-only option and multi-level commit. Full suite passes.
- Browser verified the Include linked option and source-derived counts, then cancelled without creating verification records. Exact source duplication-dialog layout and copying children without exported relationships remain incomplete.

### Grouped review and local publishing (2026-09-05)
- Review now groups unique pending records by campaign/ad set/ad, showing resulting status, known budget/objective and ad destination alongside change descriptions. Repeated edits to one record appear once with its descriptions. Unavailable budget values are not displayed as zero.
- Local publishing processes each record once, keeps off drafts off, activates only drafts whose on flag was explicitly set, and updates the row's exported delivery label. No source Meta interaction occurs.
- Tests verify grouping, destination and status, off preservation, explicit activation and export status consistency. Full suite passes. This review layout has not yet been compared visually with a populated source review dialog; no live pending edits were created to obtain one.

### Source keyboard shortcuts and scoped history (2026-09-05)
- Implemented previously observed source Ctrl+U editor, Ctrl+I history, Ctrl+Y charts, and Ctrl+Backspace delete-review actions; Cmd also accepted. Edit/history/delete require a selected record. Input, textarea, select, editable regions, modal dialogs, repeated keys and extra modifiers are excluded. Escape retains existing close behavior.
- New edit/duplicate history entries carry local ID and level. Selected-record history uses those IDs, avoiding duplicate-name conflation; old unscoped entries remain visible only in all-history view.
- Tests verify actions, deletion-confirmation routing, typing safeguards, selection requirements and two same-name records with different histories. Full suite passes. Native browser shortcut dispatch has not yet been exercised; source Meta data remains untouched.

### Objective filter continuation — 2026-09-05
Observed Objectives in the source account 167142780053170 using Sanjit, including the is operator, recent not filter, and multi-value selector. Implemented is/not, multiple values, chips, exact-ID ancestry, local overrides, persistence, view capture/restore, backup import/export and clearing. Node checks pass. Browser selecting Sales returned 24 campaigns and ₹923,642.81; removing the chip restored 47 campaigns. Source result equivalence and pixel-perfect selector styling are not yet verified. No source filters were applied and no campaign configuration changed.

### Selected-row filter — 2026-09-05
Source Sanjit account 167142780053170: selecting Retargeting Scheduled enabled Filter selected rows only; applying it added Filtering 1 campaign, retained its checkbox, and showed one campaign with ₹32,983.50. Local browser reproduced this chip, selection, row and total. Added stable local ID snapshots, exact ancestry matching across levels, disabled empty selection, chip removal, saved views, backup and persistence. Tests pass for identity separation, unknown relationships, selection independence and saved-state round trips. Source filter was removed after inspection; no configuration changes were made. Singular result count grammar was also corrected. Cross-level source result parity remains unverified.

### Reusable configuration import — 2026-09-05
The company builder now accepts --configuration and attaches settings by exact full IDs before producing files. Fixture tests cover UTF-16 TSV, multiline copy, long IDs, objective normalization, pixels and dates; verify unchanged performance metrics and names; and reject conflicts, malformed IDs and invalid dates before creating output. An all-unmatched export correctly reports zero joins. The real source configuration was read without changing assets/data.js and produced 42 campaign, 103 ad set and 842 ad settings matches. Existing builder tests also pass. Browser rendering of a newly generated company with these settings has not yet been verified. No Meta navigation or mutation occurred in this continuation.

### Current ad edits in previews — 2026-09-05
Fixed table preview routing so exact-ID source creatives are merged with current local editor overrides. New local drafts and report ads with configuration-only copy now use the placement preview modal. Explicit empty copy fields are preserved in the merged data. Original full-resolution creative images remain preferred over report thumbnails; explicit image replacement removes the old video association. Company-supplied local video plus poster remains playable through native controls. Changed previews omit source engagement counters, original post/share links and observed destination mockups. Historical performance is labelled as preceding local edits. Tests verify merge precedence, source immutability, image/video behavior, source identity removal, configuration fallback and draft modal content. Actual browser interaction for these new edit-preview cases remains to be verified.

### Rebuilt-company browser verification — 2026-09-05
Built a separate synthetic Example Company site with USD report data and a configuration CSV, served locally on port 4175. Browser verified Leads objective, imported July 1 start date, headline, body and URL in the editor. Saved different headline/body/URL; both Facebook and Instagram preview cards used the saved values. Reload preserved them. Original report total remained $42.50. The root company data and browser storage were not edited. Corrected short primary text to render completely without an unnecessary ellipsis or expand control; explicit empty copy now stays empty. Node tests and reloaded browser preview verified the correction. Full source visual parity and actual video playback remain unverified.

### Delivery filter — 2026-09-05
Source campaign-level Delivery editor observed in Sanjit account 167142780053170 with level selector, is/not, and Drafts, Pending, Active, Inactive, Not delivering, Deleted, Completed, Off choices. Added multi-select status filters, chips, persistence, saved views and JSON backups. In draft maps to Drafts; inherited Campaign off/Ad set off maps to Not delivering. Unknown statuses are excluded. Explicit same-level Deleted filters reveal local deleted records. Browser Off filter showed 47 campaigns and ₹925,836.40; chip removed after QA. Tests pass. Other levels may expose additional source statuses, and cross-level exclusion semantics and counts have not been source-verified. No source filter was applied or campaign edited.

### Account frequency summary correction — 2026-09-05
Configuration-only additions had invalidated the original source-frequency guard, hiding the observed 2.86 full-account total. The guard now checks full reference identity, reporting range and unchanged frequency/reach/impression values, permits legacy zero placeholders for configuration-only missing metrics, and rejects positive replacements or changed datasets. A single row uses its own reported frequency; multi-row filtered subsets are never averaged. Spreadsheet summary frequency uses the same logic. Browser reload verified 2.86 Per Meta account and ₹925,836.40 across 47 campaigns. Tests cover filtered subsets, duplicate IDs, changed metrics/dates, old zero placeholders, single rows and export summary values.

### Main toolbar visual comparison — 2026-09-05
Compared source and replica screenshots in Sanjit Chrome at 1920px width. The extra always-visible Ad previews button shifted reporting controls about 140px left. Moved the library to More > Ad creative library; retained selected-ad Preview. Browser verified the menu opens all 1,060 creatives. Follow-up screenshot places Columns near x1325 versus source x1328, with the table header near y260 versus source y259. Pinned-campaign icons now use a filled glyph treatment. Screenshots have different viewport heights, so footer/bottom alignment was not compared. Full suite passes; broader visual parity is still incomplete.

### Missing campaign cells recovered from source UI — 2026-09-05
Reopened source account 167142780053170 with selected_campaign_ids=6977057063964. The checked row was [Combined Ad sets] Winning Ads, with ₹30,000.00 Daily and ₹0.00 spend for August 1–31. Added only these observed cells to its existing configuration record, with exact account/campaign/date provenance and a screenObservedColumns allowlist. Existing saved rows receive only absent fields; explicit blank or edited values remain unchanged. Browser table verified both displayed cells. Tests cover zero spend, budget formatting, export and missing-only migration. Other missing configuration metrics remain unavailable. No Meta campaign values were changed.

### Record-specific pins — 2026-09-05
Replaced positional first-two-row pin glyphs with exact local record IDs seeded by source campaign IDs 52529889641768 and 6939313042164. Pins stay with records through filtering and sorting; pinned rows sort ahead of unpinned rows. Added reversible More > Pin/Unpin selected row, browser persistence and JSON backup fields. Other companies have no default pins unless pinnedCampaignIds is supplied. Tests verify identity, ordering, isolation and no campaign pending edits. Browser filtered VSL, pinned and unpinned it, confirmed Review and publish stayed disabled, and restored search/selection. Source pin/unpin interaction semantics have not been exercised; source Meta was untouched.

### Editable filter chips — 2026-09-05
Name, performance, objective and delivery chip labels now open their editors populated with current values. Apply replaces the original criterion rather than appending; drafts do not mutate criteria before Apply. A concurrent criterion change rejects a stale edit. Tests cover name tokens, numeric ranges, replacement count, stale edits and fresh-filter reset. Browser reopened an existing Sales objective with Sales checked, changed is to not, and verified exactly one chip and 18 campaigns. Removed the QA filter afterward. ID chip editing and exact source editor visual parity remain incomplete.

### ID filter chip editing — 2026-09-05
ID chips now reopen with current scope, operators and all OR rows in an independent draft. Applying edits replaces the criterion through the same guarded commit used by other filters. Tests verify exact 18-digit strings, independent draft values, replacement count and fresh-filter reset. Browser created campaign ID 6939313042164, reopened it, added OR ID 52529889641768, and verified one chip, two campaigns and ₹923,642.81. Cleared the QA filter. This completes chip-edit support for implemented name/ID/objective/delivery/performance filters; full Meta filter coverage remains incomplete.

### Engagement, conversion and custom metric filters — 2026-09-05
Read Sanjit account 167142780053170 filter menus without applying source filters or editing campaigns. Added 57 observed Engagement labels, 144 Conversions labels and the eight observed Custom metrics labels. Preserved source spelling, including App activiations. Custom labels live in company configuration; other companies can supply customFilterMetrics or metricFormats. Only metrics with a finite imported value at the current level are enabled. Missing values do not become zero. Tests cover CPC currency-key mapping, numeric bounds, missing versus zero, editing/persistence and isolation from source custom labels. Browser Link clicks > 0 returned three campaigns and ₹925,836.40; removed the filter and verified the original 47-campaign view and 2.86 frequency. Full source option coverage, record counts and original playable media remain incomplete.

### Performance goal filter and configuration data — 2026-09-05
Observed all 20 Performance goal options in Sanjit account 167142780053170. Added is/not multi-value filtering, editable chips, persistence, saved views and JSON backup/restore. Exact configuration IDs supplied raw Optimization Goal values for 103 ad sets and 842 ads; six observed export enums map explicitly to source labels. Campaign filtering traverses exact-ID child ad sets; negative filters exclude unknown goals. The reusable builder and enrichment script now import Optimization Goal. Browser initially used a cached data asset, so versioned its script URL. Reload then verified Conversions matches 14 campaigns and ₹923,642.81, with a populated checked selection on chip edit. Removed the QA filter and verified 47 campaigns, ₹925,836.40 and frequency 2.86. Automated tests additionally verify 81 conversion-goal ad sets, unknown enum exclusion and saved-state behavior. Source filter result counts and cross-level semantics have not been compared. Campaign setup showed Advantage+ sales campaign, but the configuration export lacks that flag; its functional replica remains pending.
