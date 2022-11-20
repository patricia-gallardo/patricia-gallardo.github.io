---
title: Getting Your Block-List to Mastodon
description: Using Debirdify
author: Patricia Aas
layout: post
icon: fa-pencil
image: "/assets/images/streetart-gaae38352f_640.jpg"
---

You can get a list of Mastodon handles for folks on your block-list from [Debirdify][1] to and import it into Mastodon.

* [Part 1](#part-1) : Get the Mastodon handles of folks you blocked
* [Part 2](#part-2) : Import the block-list on your Mastodon server
* [Epilogue](#epilogue)

Do this on a computer instead of mobile, my site isn't great on mobile, and you need to save a file and upload it.

## Part 1

### Get the Mastodon handles of folks you blocked

1. Go [here][1]: Debirdify is an app to find and export the handles of folks on Twitter. In my experience Fedifinder is
   better with follows, but Debirdify also does the block-list.
2. Click on the button "Authorise With Twitter"
3. When asked "Authorize Debirdify to access your account?" click "Authorize app"
4. You should now be redirected back to Debirdify
5. Click on the button "Search blocked accounts"
6. Wait
7. Scroll down and press the button "Download CSV Export for Mastodon Import"
8. Save the file blocked_accounts.csv to your Downloads folder

## Part 2

### Import the block-list on your Mastodon server

1. When logged in as your user on your server, press the item "Preferences" on the right panel
2. In the new view, press the item "Import and export" on the left panel
3. This expands the item in the panel
4. Click on the sub item "Import"
5. Under "Import type" **"Blocking list"** should be selected. If not, click on the dropdown and select it
6. Make sure the **"Merge"** radio button is selected
7. Click on the button "Choose file"
8. Select the blocked_accounts.csv file that you downloaded to your Downloads folder in [Part 1](#part-1)
9. Click on the "UPLOAD" button
10. You should see a text bubble towards the top of the page that says "Your data was successfully uploaded and will be
    processed in due time"

## Epilogue

Note that [Debirdify][1] also supports doing the same with your mute-list.

[1]: https://debirdify.pruvisto.org
