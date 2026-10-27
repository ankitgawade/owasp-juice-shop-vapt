# Request
POST /rest/user/login HTTP/1.1

Host: localhost:3000

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0

Accept: application/json, text/plain, */*

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate, br

Referer: http://localhost:3000/

Content-Type: application/json

Content-Length: 50

Origin: http://localhost:3000

Connection: keep-alive

Cookie: language=en; welcomebanner_status=dismiss; cookieconsent_status=dismiss; continueCode=Ko9y8OR4z7avbBQW3X5DYVnNKlMdE1SKKdEejZLm6pw812rqk9xgPoyJBLqJ

Priority: u=0



{"email":"ankit@gmail.com","password":"Ankit@123"}

# Response 
HTTP/1.1 200 OK

Access-Control-Allow-Origin: *

X-Content-Type-Options: nosniff

X-Frame-Options: SAMEORIGIN

Feature-Policy: payment 'self'

X-Recruiting: /#/jobs

Content-Type: application/json; charset=utf-8

Content-Length: 792

ETag: W/"318-QPE9GdHxvPBi9CX3Xl/j0bLbWwY"

Vary: Accept-Encoding

Date: Mon, 26 Oct 2026 23:49:28 GMT

Connection: keep-alive

Keep-Alive: timeout=5



{"authentication":{"token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJkYXRhIjp7ImlkIjoyNSwidXNlcm5hbWUiOiIiLCJlbWFpbCI6ImFua2l0QGdtYWlsLmNvbSIsInBhc3N3b3JkIjoiNWRlNTJlYTlkNzg3OTY2ZThiNTk4NzIwMjU1YTM3YTciLCJyb2xlIjoiY3VzdG9tZXIiLCJkZWx1eGVUb2tlbiI6IiIsImxhc3RMb2dpbklwIjoiMTI3LjAuMC4xIiwicHJvZmlsZUltYWdlIjoiL2Fzc2V0cy9wdWJsaWMvaW1hZ2VzL3VwbG9hZHMvZGVmYXVsdC5zdmciLCJ0b3RwU2VjcmV0IjoiIiwiaXNBY3RpdmUiOnRydWUsImNyZWF0ZWRBdCI6IjIwMjYtMTAtMjYgMjM6MzQ6MjYuMDY5ICswMDowMCIsInVwZGF0ZWRBdCI6IjIwMjYtMTAtMjYgMjM6MzU6MTkuOTUxICswMDowMCIsImRlbGV0ZWRBdCI6bnVsbH0sImJpZCI6NiwiaWF0IjoxNzkzMDU4NTY4fQ.y8kwQIZfKWpOOS2wRTRMZrH4pu15DHWABhaNeZTEC4F44-oYq0WbeW1xW-_V5KwJV47Sg3ZQY325V0FUtqC7gH8Uj4Iku23ydlNDdg1LdSuWYHbUPeBJ85xYcNeL_0SNnTCACvF4gUUHrMEUrjcvXLVJYgnLDmfILoiJVi6xLRM","bid":6,"umail":"ankit@gmail.com"}}