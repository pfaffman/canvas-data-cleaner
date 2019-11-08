# Canvas Data Cleaner

Takes a set of Canvas Discussions, removes names, and fixes up CSS so
that printing to PDF will look not stupid and have avatars removed and
so on.

## Preparing Data

Open each discussion in Canvas, do a "Save as HTML" from Chrome
(control-s or command-s will do that for you). This will save a .htm
(or .html) file and a Blah_files directory for each discussion.

## Cleaning data

Copy the fixnames script from this directory (aka folder) into the
data directory, and near the end find the line that says


      replace_name_and_pseudonym "INSTRUCTOR" "Pat Doe" "Pat" "Doe" "Professor"

For each student, copy and paste that line replacing "INSTRUCTOR" with the pseudonym and as many names as you like to be replaced. If the name to be replaced is multiple words, you must use quotes to connect them. This will replace instances of "Pat Person", Pat, Patty, and Pattie with "==STUDENT A==". Leaving out the quotes around "Pat Person" would replace "Pat" and "Person" separately.

      replace_name_and_pseudonym "==STUDENT A==" "Pat Person" Pat Patty Pattie

If you have multiple students with a shared first name use only their "First Last" in the first line and add another for the first name. For example:

      replace_name_and_pseudonym "==STUDENT A==" "Pat Doe"
      replace_name_and_pseudonym "==STUDENT B==" "Pat Person"
      replace_name_and_pseudonym "==STUDENT==" Pat
      replace_name_and_pseudonym "==Ed==" "John Doe"
      replace_name_and_pseudonym "==Bob==" "John Smith"
      replace_name_and_pseudonym "==First Name==" "John"

Placing "==" (or similar) around the replacement makes it easier to scan the cleaned documents to be sure that all nicknames and misspellings  have been replaced.

## Fixing up CSS

There is a css-fixer script. Running it from a data directory will copy discussions-d495dfa078.css from one of the "_files" directories into the data directory and add some CSS to it that will make the PDFs generated look much better. It's a good bet that your discussions-d495dfa078.css will have another name. My guess is that "d495dfa078" is different for each institution using Canvas. If I thought anyone else would use this, I might try to make it guess what your file is called, but I'm probably the only person who'll use this.

## Counting posts

`count-posts` does a `grep` of a string that should be only at the start of each message. If you pull it into your spreadsheet with a `:` as the separator it should be easy enough to generate a sum.

## Making it all happen

Once you've created your `fixnames` file and run `css-fixer`, you can do this (this assumes that the canvas-data-cleaner folder is in the same folder that you put your data folder(s) in.

```
../canvas-data-cleaner/push-css-to-subdirs # copy that fixed-up css file to all of the `_files` directories.
../canvas-data-cleaner/fix-all             # run fixnames for all htm[l] files.
../canvas-data-cleaner/open-all-files      # open all of the htm[l] files in your web browser
../canvas-data-cleaner/count-posts         # get a count of the number of posts in each file
```


## What if it doesn't work?

You can open an issue. If you have a budget or can convince me that I should spend time helping you for free, you might mention that. :-)

I hope this helps someone!
