# How can logging request payloads help with debugging?
It shows you exactly what the client actually sent, not just the values. 
It can send the structure of the request and the type of a field, 
and that's invisible unless you log
the raw payload at the point it enters the app.

# What tools can you use to inspect API requests and responses?
Bruno or Postman for building and replaying requests with full visibility into
status, headers, timing, and body. curl -v for quick checks. And structured
request logs that capture every real request
as it happens, not just the ones you manually replay.

# How would you debug an issue where an API returns the wrong status code?
Reproduce it in Bruno or curl and read the actual response body and response status, not just
the code you expected. Then trace backwards: check the server logs for that
request (which handler ran, did it throw), check guard/pipe order (a guard or
`ParseIntPipe` can return a status before your handler even runs), and set a
breakpoint at the point the status is decided to see which branch executed.

# What are some security concerns when logging request data?
Logging can leak passwords, auth tokens, cookies, API keys, and personla information such as email,
phone, address,.. into log files that are often less protected than the database
itself. Logs also tend to be kept longer and are more widely accessible (CI,
log aggregators, support tooling), so anything sensitive should be redacted
before it's written, not logged and cleaned up later.