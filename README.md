# Affiliate Intelligence for WordPress
Version: 2.5.63 · Author: Digital Splendid · License: GPL-2.0-or-later

Affiliate Intelligence helps WordPress site owners discover and organize affiliate-link records, review possible advertisers and networks, monitor link health, optionally track outbound clicks, import revenue CSVs, and prepare shareable monetization reports for buyers or business partners.

It is designed for reviewable, evidence-aware inventory—not as proof that an affiliate account is active or that a link has earned a commission.
Features
Link discovery and inventory
- Scans selected WordPress content types and post content, with selected metadata commonly used by page builders.
- Records discovered link destinations and associates them with content placements.
- Finds URLs in administrator-selected WordPress options; the broad discovery mode can inspect eligible options while excluding option names likely to contain credentials and other sensitive data.
- Tracks source details to help administrators find where a destination was discovered.
- Groups equivalent URL representations for reporting while preserving meaningful tracking parameters and the original stored destinations.
The scanner does not crawl arbitrary external websites, and settings stored only in custom plugin tables or remote services may require a plugin-specific adapter.
Classification, advertisers, and networks
- Suggests affiliate classifications using general URL patterns, redirect-target evidence, and configurable network rules.
- Keeps the affiliate classification separate from network identification and advertiser verification.
- Provides an advertiser/program directory with editable network, program type, status, verification fields, notes, and destination details.
- Uses a separate data-driven network catalogue; detection rules can be customized through settings or WordPress filters.
- Supports configured publisher-registration URLs for direct-referral programs. A configured URL does not verify membership.
Detection is heuristic. A hostname or tracking pattern is a clue to review, not proof of an active program relationship.
Link health and review
- Runs scheduled, batched health checks and supports on-demand checks.
- Distinguishes links awaiting an automated check from links with a recorded result.
- Reports broken or ambiguous responses separately for administrator review.
- Sends a weekly scan summary to the WordPress administration email address.
- May conservatively repair certain broken direct links when a safe destination is already known; it does not guess where an affiliate-network redirect leads.
Automated checks can be blocked, rate-limited, or challenged by destination sites. HTTP 401, 403, and 429 responses alone do not prove a link is broken. A successful health check does not confirm affiliate membership, tracking attribution, or conversion ability.
Optional click tracking and revenue imports
- Optional first-party outbound click tracking for eligible links already in the plugin inventory.
- CSV import for affiliate revenue data supplied by external network reports.
- CSV exports for link inventory and advertiser records.
Live affiliate-network APIs are not included by default. Direct API access to networks requires separate network-specific implementations, credentials, permissions, and configuration. Imported revenue is separate from link detection; the plugin does not estimate or guarantee future earnings.
Buyer-facing monetization reports
- Create public or password-protected reports with administrator-selected sections.
- Include aggregate advertiser, network, content-placement, link-health, click, and imported-revenue information where configured and selected.
- Share a direct report link, or embed a report with a shortcode.
- Print or save reports as PDF through the browser and export report HTML.
- Display a data-driven network directory and explain the difference between suspected affiliate links, inferred hosts, advertiser associations, verified status, link health, and earnings.
Review a report's visibility and selected sections before sharing it. Public reports can be accessed by anyone who has the report link. Reports are designed not to expose raw affiliate tracking URLs, account credentials, private affiliate IDs, or private commission notes.
Cross-site reporting hub
Affiliate Intelligence can send a sanitized aggregate snapshot from a source WordPress site to a receiving site, such as a central reporting hub. The source settings accept either a standard Affiliate Intelligence hub base URL or a full receiving endpoint when integrating with a compatible receiver.

The snapshot includes a site identity, generation time, summary metrics, network summaries, advertiser/program summaries, and—when available—the URL of an explicitly public source report. It does not send the raw affiliate URL inventory, credentials, private affiliate IDs, or imported revenue rows.

For the standard Affiliate Intelligence receiver, the endpoint is POST /wp-json/aiw/v1/sync, authenticated with the X-AIW-Token header. Use HTTPS and a long, private shared token. For a compatible third-party receiver such as Flipnzee Analytics, use that receiver's documented endpoint and token setup.

Recent versions also show sent-versus-accepted aggregate metrics in the source settings to help diagnose cross-site synchronization.
Buyer handover tools
The Transition Tools can replace a stored affiliate link with a manually verified direct destination, when safe, or remove the hyperlink while preserving visible text. The tool works on main WordPress post content; metadata stored by page builders, widgets, menus, theme settings, and other plugins may need separate handling.

The first transition saves the original content. Restore is guarded by a content hash so the tool does not overwrite later edits that changed the content after the transition. Back up the database and review the preview before applying bulk changes.
Installation
1. Back up your WordPress files and database.
2. In WordPress admin, open Plugins → Add New → Upload Plugin.
3. Upload affiliate-intelligence.zip, install it, and activate it.
4. Open Affiliate Intelligence in the WordPress admin menu.
5. Run a scan and review suggested link classifications, advertiser associations, and health states before publishing a report.
Requirements
- WordPress 6.0 or later (plugin metadata requirement)
- PHP 7.4 or later
- A WordPress database with permission to create/update the plugin's tables
The plugin metadata currently lists WordPress 6.8 as the tested version. Test updates on a staging site before using them on a production site.
First-run setup
1. Choose scan scope. Select the content types to scan. If scanning plugin settings, review the eligible option selection and exclusions before running a broad scan.
2. Review detections. Confirm or correct classifications and advertiser/network associations. Unknown network identity can remain Unknown when there is no reliable evidence.
3. Configure health checks. Let the scheduled jobs process checks in batches; use on-demand checks when needed. WordPress cron timing depends on site traffic, so a real server cron may be preferable on low-traffic sites.
4. Configure tracking only if needed. Enable outbound click tracking only after reviewing your privacy notice, consent requirements, and applicable law.
5. Create a report. Choose only the sections appropriate for its audience and confirm the report's visibility before sharing its direct link.
6. Optional: configure a reporting hub. Set the receiver URL and the same private shared token on the source and receiving sites, then use Send report to hub now to test synchronization.
Shortcodes
- [affiliate_intelligence_report]
- [aiw_affiliate_report]
These shortcodes can display a report when the report token is supplied through the supported aiw_report URL parameter. Generated direct report links work without adding a shortcode to a page.

For a standard Affiliate Intelligence hub, the remote report shortcode can show only remote sites that an administrator has explicitly made public:
- [aiw_remote_report]
- [aiw_remote_report site="https://example.com"]
Use the second example with the actual normalized source URL for the site you want to show. Remote report visibility must be enabled by an administrator; a successful sync does not automatically publish a source site.
Privacy and security notes
- A selected-options scanner is used instead of blindly exposing all option values. Fields likely to contain tokens, passwords, API keys, credentials, and other secrets are excluded from broad settings discovery.
- Report inventories distinguish an inferred URL host from a saved advertiser association.
- Remote snapshots are aggregate summaries rather than raw affiliate-link exports.
- Treat the cross-site shared token as a secret; use HTTPS and do not publish it in issues, screenshots, logs, or public settings exports.
- Click tracking and analytics may create privacy and consent obligations. Configure disclosure and consent as required for your site and audience.
- Public report links are public by design. Do not include sections you do not intend to disclose.
Important limitations
- Detection and network attribution are heuristic and require human review.
- Network catalogue matches and publisher sign-up links do not prove account membership.
- Automated link checks can be inconclusive; unchecked does not mean broken, and working does not mean a commission will be earned.
- Live affiliate-network API connections are not implemented by default.
- Revenue is only displayed when supported by separately imported data; future revenue is not predicted.
- Settings in custom tables, third-party services, or arbitrary external websites are not automatically discovered.
- The software and ZIP can be syntax-checked, but compatibility and behavior should be validated on your WordPress environment before production use.
Version 2.5.63 highlights
- Cross-site sync diagnostics: displays the aggregate counts sent by the source and the counts acknowledged by the receiver, without exposing affiliate URLs or the sync token.
- Public report link in snapshots: sends the dynamically generated URL of the latest explicitly public report when one is available.
- More consistent aggregate reporting: keeps affiliate-link, advertiser, placement, and network summaries grounded in the source records.
- Clearer health wording: uses Awaiting automated check for affiliate links whose health status is still unchecked, rather than implying they have been verified as working.
- Direct-referral sign-up configuration: shows a publisher sign-up URL only when an administrator has configured one for the applicable program.
Development and extensibility
Network rules can be configured in settings or extended through WordPress filters, including aiw_network_detection_rules. Suggested settings-option names can be extended with aiw_settings_option_candidates.

The source package includes a URL-identity regression test script at tests/url-identity-regression.php. The test expects WordPress and the plugin to be loaded first; running the script by itself in a bare PHP CLI is not a valid test. Passing local checks does not replace testing on a working WordPress installation.
License
GPL-2.0-or-later. See the plugin header and WordPress plugin metadata for license information.
Project: Affiliate Intelligence for WordPress
Maintainer / Author: Digital Splendide-Intelligence-for-WordPress
Discover and review affiliate links in WordPress, classify advertisers and networks, check link health, track outbound clicks, import revenue CSVs, and publish buyer-ready monetization reports.
