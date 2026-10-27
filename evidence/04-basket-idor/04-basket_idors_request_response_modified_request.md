# Request

GET /rest/basket/6 HTTP/1.1

Host: localhost:3000

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0

Accept: application/json, text/plain, */*

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate, br

Referer: http://localhost:3000/

Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJkYXRhIjp7ImlkIjoyNiwidXNlcm5hbWUiOiIiLCJlbWFpbCI6InVzZXJAZ21haWwuY29tIiwicGFzc3dvcmQiOiI0NDhkZGQ1MTdkM2FiYjcwMDQ1YWVhNjkyOWYwMjM2NyIsInJvbGUiOiJjdXN0b21lciIsImRlbHV4ZVRva2VuIjoiIiwibGFzdExvZ2luSXAiOiIwLjAuMC4wIiwicHJvZmlsZUltYWdlIjoiL2Fzc2V0cy9wdWJsaWMvaW1hZ2VzL3VwbG9hZHMvZGVmYXVsdC5zdmciLCJ0b3RwU2VjcmV0IjoiIiwiaXNBY3RpdmUiOnRydWUsImNyZWF0ZWRBdCI6IjIwMjYtMTAtMjcgMDA6MTg6MzcuMzAyICswMDowMCIsInVwZGF0ZWRBdCI6IjIwMjYtMTAtMjcgMDA6MTg6MzcuMzAyICswMDowMCIsImRlbGV0ZWRBdCI6bnVsbH0sImJpZCI6NywiaWF0IjoxNzkzMDYwMzUxfQ.OBumyBrJVWPKNwA1kI8bkesr6FdIvbnbM_pYpq-JJprKbUcnuKH1LKyrf7AkBye01yAQIkCdFXScGK8r_konme0qp5GKdQP_DqqxtP2UGCGX9b8oqLiybsPiahHTNv2w8TGyI_dDVESKhKewfruyeatA1ZVJt32EVoRIZUy-i_A

Connection: keep-alive

Cookie: language=en; welcomebanner_status=dismiss; cookieconsent_status=dismiss; continueCode=Ko9y8OR4z7avbBQW3X5DYVnNKlMdE1SKKdEejZLm6pw812rqk9xgPoyJBLqJ; token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJkYXRhIjp7ImlkIjoyNiwidXNlcm5hbWUiOiIiLCJlbWFpbCI6InVzZXJAZ21haWwuY29tIiwicGFzc3dvcmQiOiI0NDhkZGQ1MTdkM2FiYjcwMDQ1YWVhNjkyOWYwMjM2NyIsInJvbGUiOiJjdXN0b21lciIsImRlbHV4ZVRva2VuIjoiIiwibGFzdExvZ2luSXAiOiIwLjAuMC4wIiwicHJvZmlsZUltYWdlIjoiL2Fzc2V0cy9wdWJsaWMvaW1hZ2VzL3VwbG9hZHMvZGVmYXVsdC5zdmciLCJ0b3RwU2VjcmV0IjoiIiwiaXNBY3RpdmUiOnRydWUsImNyZWF0ZWRBdCI6IjIwMjYtMTAtMjcgMDA6MTg6MzcuMzAyICswMDowMCIsInVwZGF0ZWRBdCI6IjIwMjYtMTAtMjcgMDA6MTg6MzcuMzAyICswMDowMCIsImRlbGV0ZWRBdCI6bnVsbH0sImJpZCI6NywiaWF0IjoxNzkzMDYwMzUxfQ.OBumyBrJVWPKNwA1kI8bkesr6FdIvbnbM_pYpq-JJprKbUcnuKH1LKyrf7AkBye01yAQIkCdFXScGK8r_konme0qp5GKdQP_DqqxtP2UGCGX9b8oqLiybsPiahHTNv2w8TGyI_dDVESKhKewfruyeatA1ZVJt32EVoRIZUy-i_A

If-None-Match: W/"9a-LgzrJVq8SAIfLCUwhD35YfciMlY"

Priority: u=4

# Response

HTTP/1.1 200 OK

Access-Control-Allow-Origin: *

X-Content-Type-Options: nosniff

X-Frame-Options: SAMEORIGIN

Feature-Policy: payment 'self'

X-Recruiting: /#/jobs

Content-Type: application/json; charset=utf-8

Content-Length: 747

ETag: W/"2eb-Sjn4eSpnv2eSCoFjN7/ShXY3dyo"

Vary: Accept-Encoding

Date: Tue, 27 Oct 2026 00:25:08 GMT

Connection: keep-alive

Keep-Alive: timeout=5



{"status":"success","data":{"id":6,"coupon":null,"UserId":25,"createdAt":"2026-10-26T23:34:43.296Z","updatedAt":"2026-10-26T23:34:43.296Z","Products":[{"id":1,"name":"Apple Juice (1000ml)","description":"The all-time classic.","price":1.99,"deluxePrice":0.99,"image":"apple_juice.jpg","alternateImages":[{"file":"apple_juice-1x.avif","format":"image/avif","density":"1x"},{"file":"apple_juice-2x.avif","format":"image/avif","density":"2x"},{"file":"apple_juice-3x.avif","format":"image/avif","density":"3x"}],"createdAt":"2026-10-26T23:27:16.139Z","updatedAt":"2026-10-26T23:27:16.139Z","deletedAt":null,"BasketItem":{"ProductId":1,"BasketId":6,"id":9,"quantity":1,"createdAt":"2026-10-27T00:17:55.347Z","updatedAt":"2026-10-27T00:17:55.347Z"}}]}}
