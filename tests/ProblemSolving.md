#RandomStorm Technical Test

##Problem Solving

Most technical tests are usually "write me this piece of code" or “fix this broken application” however we find that when testing candidates at a higher level, there is a very limited amount that this will tell us about the candidates knowledge. We are much more interested in *how* you would code, rather than us looking at two thousand lines of code you’ve written just to try to impress us.

We have produced two problem solving tests, you do not need to complete both; we want you to complete the one that you feel more comfortable designing a solution for. With that in mind, we are going to give you an abstract problem to solve. Your role with RandomStorm will involve a large amount of architectural problem solving as well as getting down to the nitty gritty and writing the solution. We are a company that believes in building a solution rather than being constrained by concerns of business restriction, so feel free to go as mad as you want with how you solve the problem.

Your choice of programming language is important in this situation. We are a company that uses PHP to solve a number of web and data-handling problems, however both of the problems below can be solved better in other languages than PHP. Perhaps try your hand at solving it in a new language. Remember, we don’t want you to write code, so you don’t need to understand the syntax of the language, only enough about it to be able to tell us how and why you might use it to solve the problem.

### The Problems:

Problem 1 - The Architect: *This is a problem involving some very low level file handling challenges, it is going to test your knowledge and understanding of how your chosen language responds to handling big data, and show us how you solve problems that aren’t the usual ebb and flow of programming.*

Problem 2 - The Programmer: *We examine lots of data, some of that needs to be statistically analysed against a set of predefined rules. This test gives you a few of those business rules, and asks you to design a software solution to meet those rules, and invent a few of your own.*

## Problem 1 - The Architect

A server receives syslogs from a considerable number of remote devices. It logs all of these syslogs are written to a file from which you need to retrieve them, then store that information into a datastore that can be queried.

We would like you to abstractly architect some software that will read this file and will take each individual log line, and split out common sections like the date or the system process and put it into a datastore.

To get the useful data out of each line of the log, you will have a series of Regex based patterns that can recognise particular types of log lines from different devices, and retrieve consistently formatted meaningful data from them.

Here’s an example log line:
`[2014-03-27 06:24:22] %ASA-4-405001: Received ARP response collision from 192.168.0.17/6e42.a82f.db4b on interface Randomstorm-pl1-vl2`

### Deliverables

Mainly, we want to know how you would get this data from this file into the data store, but we also want to know about the steps in between.

* Would your processor handle being stopped unexpectedly?
* Is your proposed solution as fast as it can be?
* What datastore would you use and why?
* What language(s) would you use to write this?
* Are there any libraries in this language you know of and would likely make use of?
* How you would write the processors, would you have each different regex pattern run against the line?
* How would you handle error reporting within the processor?
* What would you do if the file had to be rotated (i.e logrotate)

#### Matters of note:

* The file will likely be written too at *between* 10 and 100,000 log lines per second
* Each log will be separated with a new line (\n)
* There would be multiple (perhaps hundreds) of patterns to match against

#### Things you can assume:

* You have a list of pre-existing regex patterns that will get this data from a log line
* You are not limited on disk space
* The user will usually only be looking at a very small subset of this data

## Problem 2 - The Programmer

Because our software usually involves processing extremely large amounts of data, we have to be smart in the software we develop that helps businesses solve their security problems. One of the most common pieces of information our log analysis product deals with at any given time is that of a user logging in and out of computers on the client’s network.

A piece of information that is vital to the customer is *where* users are logging in, and *at what time* users are logging in.

<table>
  <tr>
    <td>Alert 1</td>
    <td>Alert 2</td>
  </tr>
  <tr>
    <td>{
    "user": "John Hugget",
    "action": "Log on",
    "location": {
        "address": "Wetherby, United Kingdom",
        "machine": "X031415"
    },
    "localTime": "2014-03-21 09:32"
}</td>
    <td>{
    "user": "John Hugget",
    "action": "Log on",
    "location": {
        "address": "London, United Kingdom",
        "machine": "X042515"
    },
    "localTime": "2014-03-21 10:01"
}</td>
  </tr>
</table>


If you look in Alert 1 above, you can see that it contains the name of the user, the action performed (in this case logging on) at 9:32AM in Wetherby on machine X031415. Imagine now that, you saw alert 2 a little later on, you know that from Wetherby, it is not possible to travel to London within 29 minutes, so as a human you can realise that this user, has either shared his login details, or someone else has gained illegitimate access to his account.

There are, in the real world many thousands of possible "actions" that can be performed, each of them have more or fewer details, for the purposes of this test though, we will stick to a simple list.

* Log on
* Log off

Our systems can be changed by the business that is using our product, a prime example of this might be restrictions on when and where a user can log in from and at what times.

### Deliverables

We want you to design a piece of software that would take in these alerts from a streaming source (think sockets, files etc - your solution shouldn’t hinge on how the data is delivered), and we want you to design how it would meet the rules for their business, by default here are some default rules that might generate an exceptional circumstance, go ahead and add more of your own though, so we can see how robust your design might be.

1. A user cannot login to multiple locations at once
2. A user cannot travel at light speed, so their logins and log-out’s have to be processed geospatially
3. A user shouldn’t log in outside of their working hours. Their working hours data is housed in a separate system, but is accessible via a RESTful API from your software

Not all alerts are of the same importance. For example, if a user logs on in Wetherby at 09:00 on the 21st, and then logs-in to London at 08:30 on the 22nd that should generate an alert (because the user hasn’t logged out), however because it is not suspicious (entirely possible the user powered off the machine without logging off) then that should generate an informational event - it’s something you have seen, but not classified as important. You then need to categorise the rules we have above, and the rules you put in as "low", “medium” and “high” level alerts. The example below the alerts given above would be an example of a “high” level alert - as it is likely to pose an immediate security risk.

As with all of our technical tests, for whatever role - we don’t want you to write code! We want you to design this solution in whichever way suits your style, some like to write pseudocode, others like to brain dump into vim. Whatever your preferred style, we don’t care. We want your description of how you would solve this problem, what software, what external services you might use, how you might store the alerts, in what storage engine, and even the language you might use to solve this.

## What we want at the end of your chosen problem:

A section of text that describes how you would solve the problem. We want you to be descriptive, we want the solution you devise to be clearly explainable. These problems do not  need over-engineering so always try to stick to the KISS principle.

We’re not looking for you to write us any code for this. As we explained previously, although we **_do_** care how you write code, usually however, at the level of engineers we employ, you are able to code to a good standard, and what you don’t know, we will be happy to teach you.

The key thing for us is that you enjoy solving these problems. Although this isn’t all that we do, problems like this are the type our team solves every day. We want you to show us how good you are at looking at a problem, breaking it into it’s initial components, and then solving each of those.

You can spend as much or as little time as you want on this. We have had candidates spend entire weekends on this, or just an hour or so. We suggest you put in enough time for you to be happy with the solution that you present back to us.


