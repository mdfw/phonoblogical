---
layout: page
title:  "Phonoblogical Database document types"
date:   2017-07-19
tags: x-sup
---

**Notes**:
* Assumes CouchDB compatible database
* Arrays are indicated by []
* All Doctypes start with pb to avoid naming collisions but should otherwise make sense.
* {i18n} - indicates an object with the text in an object with i18n keys.

<br />
### All docs should have these fields

| name | Type | notes |
| --- | --- | :----: |
id 				| String | probably from Couch 
dateCreated 	| Date 
dateModified	| Date
createdBy		| User
modifiedBy		| User

<br />
## Site

| name | Type | notes |
| --- | --- | :----: |
title 			| String | The title of the site "Phonoblogical" used if empty
url				| URL 	 | The url of the site
tagline			| {i18}  | The tagline used in the site description (mostly google).

<br />
## _user extensions

| name | Type | notes |
| --- | --- | :----: |
audienceLevel		| String | 'all', 'member', 'patron', 'none'
email				| String.email | email address of user


<br />
### All 'targetable'
_Targetable are those that can have a url, not used internally by the app_

| name | Type | notes |
| --- | --- | :----: |
shortID 		| String | Something short for URL - see snowflake 
status			| String | "draft", "published", "removed", "review", "submitted"
signature		| String | Future: Allow for signing content. See <https://wiki.apache.org/couchdb/SignedDocuments>

_May want to consider header items. See: <https://gist.github.com/kevinSuttle/1997924>_

<br />

---

<br />
### User profile:
_These are separate from the actual user table that will not be syncable._

| name | Type | notes |
| --- | --- | :----: |
doctype 	| "pbprofile"
userID 		| String 	| From the ? _need to figure out_
handle 		| String
real_name 	| String 	| optional: real name

<br />
### Group:

| name | Type | notes |
| --- | --- | :----: |
doctype 	| "pbgroup"
name 		| String
users 		| [User]

<br />
### Album:

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbalbum"
title 			| String
dateReleased	| Date
information 	| {i18n}
artist 			| Artist
tracks			| [Track]
urls			| [URL]
tags			| [String]
reviews			| [Review]
audience		| String | 'all', 'member', 'patron', 'none'

<br />
### Track:

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbtrack"
title 			| String
artist			| Artist
album			| Album
dateReleased	| Date
information 	| {i18n}
tags 			| [String]
genre			| [String]
lyrics			| [String]
lyricsURL		| URL
BPM				| Int
urls			| [URL]
videos			| [URL]
reviews			| [Review]
audience		| String | 'all', 'member', 'patron', 'none'

<br />
### Artist:

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbartist"
name:			| String
information:	| {i18n}
tracks:			| [Track]
albums:			| [Album]
urls:			| [URL]
reviews: 		| [Review]
audience		| String | 'all', 'member', 'patron', 'none'

<br />
### Video:

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbvideo"
url: 			| [URL]
reviews:		| [Review]
audience		| String | 'all', 'member', 'patron', 'none'

<br />
### Blog Post:

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbblog"
title			| String
text			| String
stub			| String
tags			| [String]
language		| String
audience		| String | 'all', 'member', 'patron', 'none'

<br />
### Review:

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbreview"
reviewText: 	| {i18n}
ratings:		| [Rating]
weApprove: 		| bool
audience		| String | 'all', 'member', 'patron', 'none'

<br />
### Rating:

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbrating"
ratingType: 	| RatingType 
ratingText: 	| {i18n}
rating:			| Number
audience		| String | 'all', 'member', 'patron', 'none'

<br />
### Rating type:
_Note: Not a targettable type_

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbratingtype"
type 			| {i18n}

<br />
### Page

| name | Type | notes |
| --- | --- | :----: |
doctype 		| "pbpage"
text			| {i18n}
audience		| String | 'all', 'member', 'patron', 'none'
