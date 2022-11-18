---
title: Mastodon migration
description: Moving to a new server
author: Patricia Aas
layout: post
icon: fa-pencil
image: "/assets/images/graffiti-gbf2cdfe79_640.jpg"
---

I will try to keep this short and simple. We are going to try to migrate from one Mastodon server to another.

* [Part 1](#part-1) : **New Server**: Prepare your profile
* [Part 2](#part-2) : **Old Server**: Download your follows list
* [Part 3](#part-3) : **New Server**: Upload follows list
* [Part 4](#part-4) : **New Server**: Set up the account alias
* [Part 5](#part-5) : **Old Server**: Perform the move
* [Epilogue](#epilogue)

## Part 1

### New Server: Prepare your profile

1. Make sure to copy over bio, profile pic, banner etc before the move
2. Once the move is done this can be difficult to get a hold of

## Part 2

### Old Server: Download your follows list

1. Log into the server you're moving from
2. Go to "Preferences" (right panel)
3. Click on "Import and export" (left panel)
4. Click on CSV for "Follows"
5. Download the file "following_accounts.csv" to your Downloads folder
6. Do the same for any other category like "You block", "You mute" etc
7. Consider if you want to download your archive "Request your archive"

## Part 3

### New Server: Upload follows list

1. Log into the server you're moving to
2. Go to "Preferences" (right panel)
3. Click on "Import and export" (left panel)
4. Click on "Import" (left panel)
5. Check that "Following list" is selected in the dropdown
6. Make sure the "Merge" radio button is selected
7. Click "Choose File" and pick the "following_accounts.csv" file we downloaded earlier
8. Press the "UPLOAD" button
9. Do a similar thing with each of the other CSV files you downloaded in Part 2 (make sure to select the right thing in
   the dropdown)

## Part 4

### New Server: Set up the account alias

1. Log into the server you're moving to
2. Write and pin a post saying you're moving here so that your follows will understand what is happening
3. Go to "Preferences" (right panel)
4. Click on "Account" (left panel)
5. Click the link under "Moving from a different account" : "create an account alias"
6. Paste in the handle of the old account @user@server
7. Click on "CREATE ALIAS"

## Part 5

### Old Server: Perform the move

1. Log into the server you're moving from
2. Write a post where you tell people you are moving and pin it
3. Go to "Preferences" (right panel)
4. Click on "Account" (left panel)
5. Click on the link under "Move to a different account"
6. Put the handle to the new account in the left field
7. Put the password of the old account in the right field
8. Click on the button "MOVE FOLLOWERS"
9. Go to your profile and check that it says on the right "has been moved to"

## Epilogue

We will keep the old account for now, it is being redirected and our old posts are there. In the future we might want to
delete it permanently, but for now we will leave it like this.
