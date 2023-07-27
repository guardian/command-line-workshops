## Introduction

### 1. How can I use shortcuts to quickly navigate on the command line?
#### What are some useful shortcuts for moving the cursor?
* `←`, `CTRL` + `B` = Move back one character
* `→`, `CTRL` + `F` = Move forward one character
* `ALT` + `←`, `ALT` + `B` = Move backward one word
* `ALT` + `→`, `ALT` + `F` = Move forward one word
* `CTRL` + `A` = Go to the beginning of the line (Home)
* `CTRL` + `E` = Go to the End of the line (End)
* `ALT` + `Click` (i.e. with mouse) = Move cursor to clicked location

#### What are some useful shortcuts for erasing?
* `CTRL` + `W` = Delete from cursor to start of word
* `ALT` + `D` = Delete from cursor to end of word
* `CTRL` + `U` = Delete from cursor to start of line
  * You may need to bind this if using zsh! Simply add `bindkey "^U" backward-kill-line` to your .zshrc file (and remember to source it!)
* `CTRL` + `K` = Delete from cursor to end of line


### 2. What command line tools can I use to process text?
* `cut`
  * Use to split a line and return segment(s)
```
$ cut -f1 -d ' ' names.txt # forenames
Tomos
Francesca
Sumayyah

$ cut -f2 -d ' ' names.txt # surnames
Vargas
Cuevas
Potts

$ cat urls.txt
https://api.media.gutools.co.uk/images/55e7c79df4dfc4f050525e929445127357ab65db
https://api.media.gutools.co.uk/images/ba87ea47326d3d5deefb4a5b45ea0ca677cf1c47
https://api.media.gutools.co.uk/images/16c60b6546981fbcdc2936fbe13e30dc41d39912

$ cut -d '/' -f 5
55e7c79df4dfc4f050525e929445127357ab65db
ba87ea47326d3d5deefb4a5b45ea0ca677cf1c47
16c60b6546981fbcdc2936fbe13e30dc41d39912

$ cut -d '/' -f 1,5
https:/55e7c79df4dfc4f050525e929445127357ab65db
https:/ba87ea47326d3d5deefb4a5b45ea0ca677cf1c47
https:/16c60b6546981fbcdc2936fbe13e30dc41d39912
```
* `sed`
  * Perform more complex operations on text - common is substitution
```
$ echo hello world | sed 's/o/O/g'
hellO wOrld

$ echo hello world | sed 's/hello//g'
 world

$ sed 's/https:\/\/\(.*\.co\.uk\)\/.*/\1/g' urls.txt
api.media.gutools.co.uk
``` 
* `awk`
  * Similar to sed, different syntax, eg:
```
$ echo hello world | awk '{sub(/hello/,"HELLO"); print}'
HELLO world
```
* `tr`
  * "Translate" from one set of characters to another
```
$ echo hello world | tr '[:lower:]' '[:upper:]'
HELLO WORLD
# or, to delete characters:
$ echo hello world | tr -d o
hell wrld

# useful for stripping nbsps!
$ cat file_with_nbsp.txt | tr -d '\240'
```
* `head`
  * List the first few lines/words/characters from a file or input
* `tail`
  * List the last few lines/words/characters from a file or input
  * "tail -f" will watch a file for newly added content, and immediately print to screen. Useful for watching logfiles!
* `jq`
  * Query a JSON document
```
$ echo '{"obj":{"arr":[5,6,7]}}' | jq .
{
  "obj": {
    "arr": [
      5,
      6,
      7
    ]
  }
}

$ echo '{"obj":{"arr":[5,6,7]}}' | jq '.obj.arr[]'
5
6
7
```
* `pbcopy`
  * Any input you pipe to this will be on your clipboard, so you can paste with ⌘V (ie. this is equivalent of ⌘C)
* `pbpaste`
  * This will output whatever is on your clipboard, so you can pipe to other commands (ie. equivalent of ⌘V)
* `sort`
  * Sorts the lines given in input
```
$ cd grid; du -hs ./* # what are the biggest directories in the grid repo?
4.0K	./Brewfile
 12K	./LICENSE
4.0K	./NOTICE
4.0K	./README.md
1.5M	./admin-tools
 16K	./application.home_IS_UNDEFINED
808K	./auth
228K	./bbc
 12K	./build.sbt
1.1M	./collections
9.5M	./common-lib
1.7M	./cropper
106M	./dev
4.0K	./docker-compose.yml
720K	./docs
4.0K	./get-stack-resource.sh
227M	./image-counter-lambda
3.3M	./image-loader
405M	./kahuna
856K	./leases
356K	./logs
3.9M	./media-api
1.4M	./metadata-editor
4.0K	./persistence-lib
3.7M	./project
 20K	./quarantine-status
 40K	./reaper
3.3M	./rest-lib
4.0K	./riff-raff.yaml
284M	./s3watcher
1.4M	./scripts
 12K	./stress-test
1.1M	./target
 12M	./thrall
1.6M	./usage

$ du -hs ./* | sort -h # above was unhelpful, where was the biggest? SORT
4.0K	./Brewfile
4.0K	./NOTICE
4.0K	./README.md
4.0K	./docker-compose.yml
4.0K	./get-stack-resource.sh
4.0K	./persistence-lib
4.0K	./riff-raff.yaml
 12K	./LICENSE
 12K	./build.sbt
 12K	./stress-test
 16K	./application.home_IS_UNDEFINED
 20K	./quarantine-status
 40K	./reaper
228K	./bbc
356K	./logs
720K	./docs
808K	./auth
856K	./leases
1.1M	./collections
1.1M	./target
1.4M	./metadata-editor
1.4M	./scripts
1.5M	./admin-tools
1.6M	./usage
1.7M	./cropper
3.3M	./image-loader
3.3M	./rest-lib
3.7M	./project
3.9M	./media-api
9.5M	./common-lib
 12M	./thrall
106M	./dev
227M	./image-counter-lambda
284M	./s3watcher
405M	./kahuna
```
* `uniq`
  * List the unique lines in the input (input must be sorted!) - optionally count the repetitions, OR list only lines that were not repeated!
```
$ echo 'a\na\nb\nb\na\nb\nc\nb\na\na\nb' | uniq # wrong
a
b
a
b
c
b
a
b

$ echo 'a\na\nb\nb\na\nb\nc\nb\na\na\nb' | sort | uniq
a
b
c

$ echo 'a\na\nb\nb\na\nb\nc\nb\na\na\nb' | sort | uniq --count
   5 a
   5 b
   1 c

$ echo 'a\na\nb\nb\na\nb\nc\nb\na\na\nb' | sort | uniq --unique
c

$ echo 'a\na\nb\nb\na\nb\nc\nb\na\na\nb' | sort | uniq --repeated
a
b
```
