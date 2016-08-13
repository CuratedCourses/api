# CuratedCourses.org API

## How to include relevant content from CuratedCourses.org on your own site

In the `<head>` of your webpage, include
```html
<script src="//curatedcourses.org/v1/share.js"></script>
```

Include
```html
<span class="curated-courses outcome">OUTCOME</span>
```
in any paragraphs or similar block-level elements which relate to the OUTCOME.  The script `share.js` will try to be clever about where to place related content, but if it is insufficiently clever, then you should create `<div class="curated-courses related-content"></div>` to help `share.js` locate reasonable places to display related content.

Loading `share.js` performs the following actions:
- Places the webpage (i.e., window.location) in CuratedCourses.org’s curation queue if it hasn’t already been curated, using the meta tags in the <head> to provide the relevant metadata.
- Searches the page for the outcome spans, to identify what content might be relevant from CuratedCourses.org’s collection.
- Places knowls for relevant content inside any nearby` <div class="curated-courses related-content"></div>`.  Nearness is measured by distance through the DOM tree from the corresponding outcome span.  This is done via JSONP on curatedcourses.org to avoid web hosts from having to reconfigure their pages in any way.
- Records usage statistics and votes from users as they click on these knowls.
- If the webpage is approved after curation, then other websites will link back to the webpage as well.

## IFRAME embedding

Sometimes people do not have control over the <head> and cannot include arbitrary javascript in their page, so an IFRAME embedding is also available. To include content related to a specific outcome, include

```html
<iframe width="420" height="315" src="https://curatedcourses.org/v1/embedded/OUTCOME">
</iframe>
```
at the appropriate place in your HTML file.  The IFRAME will be populated with curated content related to the specified outcome.

## LTI tool provider

To embed relevant into an LMS, CuratedCourses.org can also act as an LTI tool provider.
