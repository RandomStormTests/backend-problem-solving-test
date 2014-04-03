# Problem 2 - The Programmer

Because our software usually involves processing extremely large amounts of data, we have to be smart in the software we develop that helps businesses solve their security problems. One of the most common pieces of information our log analysis product deals with at any given time is that of a user logging in and out of computers on the client’s network.

A piece of information that is vital to the customer is *where* users are logging in, and *at what time* users are logging in.

<table>
  <tr>
    <td>Alert 1</td>
    <td>Alert 2</td>
  </tr>
  <tr>
    <td><pre>{
    "user": "John Hugget",
    "action": "Log on",
    "location": {
        "address": "Wetherby, United Kingdom",
        "machine": "X031415"
    },
    "localTime": "2014-03-21 09:32"
}</pre></td>
    <td><pre>{
    "user": "John Hugget",
    "action": "Log on",
    "location": {
        "address": "London, United Kingdom",
        "machine": "X042515"
    },
    "localTime": "2014-03-21 10:01"
}</pre></td>
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
