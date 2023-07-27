## Shell games – publication panic!

There's chaos in the newsroom! Composer, our content management system, is slowing to a crawl, and journalists are missing deadlines.

We think it might be because of **increased traffic**. To investigate, we've got some logs from one of Composer's backend services. It logs a **user e-mail** for every request it receives.

We'd like to answer the question – which user is sending the largest number of requests? Maybe we can tell them to knock it off!

There are many ways to arrive at an answer. We're likely to use **common unix utilities**, **piping**, **redirection**, **shell scripts**, and **substitution**.

The logs will be given to you by your instructor as a .csv file, fresh from [central ELK](https://logs.gutools.co.uk/), our logging platform. (They're real!)

To find out more about the commands mentioned in the hints below, we recommend using [tldr](https://tldr.sh/) – you can download and run this locally on the command line, or just use the webapp.

<hr/>

#### 1. Read the file and output all of the lines in the file that a) contain user e-mails, and b) represent HTTP requests, to stdout.

There are a few lines that don't have e-mails – or that have e-mails, but don't represent requests. We don't want those.

<details>
<summary>Hints</summary>
We should be able to use `cat`, `grep` and the pipe operator `|` to get this done. `grep -E` can search for regular expressions – the 'E' stands for 'extended' regular expressions, and is necessary to enable what are now commonly used features of regular expressions. The regular expression `(GET|PUT|POST|HEAD)` will match lines that contain any of those HTTP verbs in case-sensitive fashion.
</details>

#### 2. Alter the command to display only the user e-mail for every line of input it receives.

Be sure to show only the e-mail – no additional characters! We might want to use the output of this command as the input to another command, so it's good for it to be clean.

<details>
<summary>Hints</summary>
`cut` will help you isolate the input, and CSV files are delimited with commas. `sed` will help you strip any extra characters, should they appear in your output.
</details>

#### 3. Alter the command to display a count of the number of unique e-mails, and sort the output to show us the most prolific user.

Here's an example of what the output might look like:

```
10 a.user@guardian.co.uk
24 another.user@guardian.co.uk
567 third.user@guardian.co.uk
```

<details>
<summary>Hints</summary>
`uniq -c` will give a list of unique lines, with a count against each – dead handy! Don't forget that `uniq` requires a sorted input – `sort` can help here.
</details>

<details>
<summary>The final answer!</summary>
You should be seeing lots of requests from "workflow.test@guardian.co.uk"! But who on earth is Workflow Test? That's the e-mail address used by beloved production monitoring system, [Prodmon](https://github.com/guardian/editorial-tools-production-monitoring/)! Clearly, it's gone mad with power after a recent deploy – the team deploys the most recent known good branch, and the system stabilises. Phew!
</details>

#### 4. What a useful command! Let's add it to a convenient script, so it's easy for us to scan our logs next time this happens.

The script should accept the name of the csv file as its first argument, so we don't have to hardcode it – running it should look like:

```
./get-user-emails.sh logs.csv
```

#### 5. Our script should write the results to a file, rather than stdout.

To make it easy to identify and to see when it was run, let's write it to a file called `composer-backend-user-request-count-$DATE_TIME.txt`. `$DATE_TIME` should be the date and time the file was written, in a filename friendly format, e.g. [ISO8601](https://en.wikipedia.org/wiki/ISO_8601).

<hr />

Well done, you've completed the exercise! 🎉 If you've still got some time left, here are some stretch goals –

- Add a second argument to the script that allows the user to _optionally_ specify a username to filter by.
- Allow the user to specify the arguments with parameters, for example `./script.sh -f ./path-to-file.txt -u example.user`.
- Can we display the HTTP verb alongside the user, to see which verbs are most popular? Here's some example output:
```
117 POST example.user@guardian.co.uk
122 GET example.user@guardian.co.uk
125 POST another.user@guardian.co.uk
129 GET another.user@guardian.co.uk
131 POST third.user@guardian.co.uk
132 PUT third.user@guardian.co.uk
```
