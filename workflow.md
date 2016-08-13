# Major workflow

The user-facing interface for CuratedCourses.org is built around

- the table of contents of many popular textbooks
- a tag cloud of topics to click on to browse the content
- a video player that embeds YouTube videos (so we can display related content)
- an "add content" workflow (which also leads directly to...)
- a "review content" workflow (which also leads directly to...)
- a "tag content" workflow

The "review content" step and the "tag content" step could happen in
either order, or even simultaneously.  I'm not sure what is best.

Other reasonable ways to browse might include:

- newest additions
- highest rated
- most popular

A single asset can be viewed inside CuratedCourses.org in order to see
its reviews and how it relates to other content.

# The standard workflow

A user will have to be logged into CuratedCourses.org in order to add
content, because the content that they add will be associated with
their identity.  This way abusive users can be shadowbanned, and have
their bad tags and reviews not shared with anyone but themselves.

## First, add content

The initial submission simply requires a URL.  If the URL already
appears in the database as an asset (or a synonym of an URL of an
asset) then we let the user create a duplicate asset?  I don't know.

CuratedCourses.org attempts to access the URL to verify it is valid
(and this had better be rate-limited...)

If it is a video, it is processed as such (e.g., the YouTube API v3 is
used to grab tags, description, thumbnails, titles, authors, etc to
populate the next form).  If it is a webpage, <head> of the webpage is
examined to see what metadata can be autopopulated.  If it is a github
repository, the "education.json" file is accessed.  If it is a TeX
file, the \author and \title is grabbed.  If it is a PDF, well maybe
there is some metadata in the PDF to be grabbed (or at least
thumbnailed).

The next page then presents a (then hopefully mostly completed) form
asking for the usual author, title, etc.  The unambiguous metadata.

The asset is added, and the "next" button links to an "add review"
button.

## Then, review the quality

The quality of the asset is reviewed, and a short description is
provided.  Potentally many reviews will appear for each asset.

As assets are viewed within the CuratedCourses.org platform, they all
have an "add review" button, so people can step into this point of the
workflow at any time.  Only logged in users see the "add review"
button but anybody (logged in or not) can browse content.

(It's potentially better to have reviews provide comparative judgments
rather than absolute judgments.)

## Finally, add (or remove) tags

As assets are viewed within the CuratedCourses.org platform, they all
have an "add tags" button, so people can step into this point of the
workflow at any time.

Somehow people are going to want to remove tags, too.

# Sorting workflows

Assets, once created, are re-sorted for various kinds of processing by
the editorial staff.

## Linkrot queue

A small portion of each asset is downloaded (e.g., some
unlikely-to-change text from the webpage is compared; YouTube links
followed to update view counts and other popularity metadata; if it is
a webpage, the various outcomes become tags).

A weekly crontab runs to check if an asset has moved permanently (and
then update the URL) or disappeared, or no longer returning the
unlikely-to-change text.

The "linkrot queue" is the result of sorting the content by the number
of times the URL has no longer resolved to the original content.  (If
an assets' URL does resolve, then this asset won't appear in the
linkrot sort).

## Curation queue

Sort by the most popular content with the least authoritative reviews.

A positive review of url A will positively impact url B if A and B
share a prefix.  So once someone starts reviewing parts of Beezer's
book, it won't be at the top of the curation sort.

Assign reviewers who get email links to a form that they can fill out
to complete a review.

## Untagged queue

Sort by content which hasn't been tagged so it can get tagged.

