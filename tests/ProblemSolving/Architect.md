# Problem 1 - The Architect

A server receives syslogs from a considerable number of remote devices. It logs all of these syslogs are written to a file from which you need to retrieve them, then store that information into a datastore that can be queried.

We would like you to abstractly architect some software that will read this file and will take each individual log line, and split out common sections like the date or the system process and put it into a datastore.

To get the useful data out of each line of the log, you will have a series of Regex based patterns that can recognise particular types of log lines from different devices, and retrieve consistently formatted meaningful data from them.

Here’s an example log line:
`[2014-03-27 06:24:22] %ASA-4-405001: Received ARP response collision from 192.168.0.17/6e42.a82f.db4b on interface Randomstorm-pl1-vl2`

## Deliverables

Mainly, we want to know how you would get this data from this file into the data store, but we also want to know about the steps in between.

* Would your processor handle being stopped unexpectedly?
* Is your proposed solution as fast as it can be?
* What datastore would you use and why?
* What language(s) would you use to write this?
* Are there any libraries in this language you know of and would likely make use of?
* How you would write the processors, would you have each different regex pattern run against the line?
* How would you handle error reporting within the processor?
* What would you do if the file had to be rotated (i.e logrotate)

### Matters of note:

* The file will likely be written too at *between* 10 and 100,000 log lines per second
* Each log will be separated with a new line (\n)
* There would be multiple (perhaps hundreds) of patterns to match against

### Things you can assume:

* You have a list of pre-existing regex patterns that will get this data from a log line
* You are not limited on disk space
* The user will usually only be looking at a very small subset of this data