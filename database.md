# Database

The CuratedCourses database includes a few kinds of objects.

## Assets

CuratedCourses’ database of OER or “assets” is gathered from various places

- Content that has been contributed through a “content submission form” on CuratedCourses.org
- meta tags in the <head> of HTML pages which embed content from CuratedCourses.org
- YouTube’s metadata (for videos which have been submitted into CuratedCourses curation queue)
- education.json files in the root directory of, say, GitHub repositories

The asset metadata is then stored in a schemaless document collection.

## Reviews

Assets are reviewed by reviewers.

## Tags

There is an authoritative list of tags (which include both outcomes and topics) produced by the CuratedCourses leadership.

Assets are linked to these tags.  These links may appear organically
on pages (e.g., as the outcome spans, or in the tag field of a
YouTube), or they are submitted by curators.  OUTCOMEs which appear in
tags are silently added to the database, but may be linked as

