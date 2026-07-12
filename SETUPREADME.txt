SEGMENTATION FORM PAGE — SETUP NOTES
=====================================
File: index.html (single self-contained file — HTML, CSS and JS all inline)

This is Stage 1 of the funnel described in the Business System Development
Plan: the first page traffic lands on from Link in Bio / Online Ads. It
segments each visitor into Business Owner / Freelancer / Student, collects
their name + email, and routes them to the matching Stage 2 landing page.

Before going live, edit the CONFIG block near the bottom of index.html
(search for "CONFIG — edit these before going live") and the two tracking
snippets in <head>:

1. GA4 (Google Analytics 4)
   - Near the top of <head>, replace every "G-XXXXXXXXXX" with your real
     GA4 Measurement ID (Admin > Data Streams > your web stream).
   - A "generate_lead" event fires automatically on successful submit,
     tagged with the chosen segment (business_owner / freelancer / student).

2. Meta Pixel
   - In <head>, replace "0000000000000000" (appears twice — once in the
     script, once in the <noscript> fallback) with your real Pixel ID from
     Meta Events Manager.
   - A "Lead" event fires automatically on successful submit, tagged with
     the chosen segment.

3. Leads database (Google Sheets)
   - Set CONFIG.SHEETS_WEBHOOK_URL to a Google Apps Script Web App URL
     (or a Zapier/Make catch hook) that appends each submission to your
     Sheet. Apps Script is the free native option — deploy a script bound
     to your Sheet as a Web App ("Execute as: Me", "Who has access:
     Anyone"), then paste the deployment URL in.
   - The payload sent is: fullName, email, segment, source, submittedAt.
   - This call uses mode:"no-cors" and never blocks the redirect, so a
     slow or misconfigured webhook won't strand a visitor on this page —
     rely on the Stage 1 follow-up system (per the dev plan) to catch
     anyone the webhook call fails to reach.

4. Landing pages (Stage 2 routing)
   - Set the three URLs in CONFIG.LANDING_PAGES to your real Business
     Owner / Freelancer / Student landing pages.
   - The visitor's name, email and segment are passed along as URL query
     params (?name=...&email=...&segment=...) so the landing page /
     payment step can prefill or personalize.

5. Branding
   - Replace "[Your Community Name]" (appears in the header and footer)
     and swap the little gradient square logo mark for a real logo if
     you have one.
   - Update the "Privacy Policy" link's href.

Everything else (copy, layout, colors, validation, honeypot spam trap)
is ready to use as-is. Tested responsive from 390px mobile up, and in
both light and dark OS color schemes.
