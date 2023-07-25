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
* `sed`
* `awk`
* `tr`
* `head`
* `tail`
* `jq`
* `pbcopy`
* `pbpaste`
* `sort`
* `uniq`