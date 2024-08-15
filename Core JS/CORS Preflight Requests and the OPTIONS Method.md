### CORS Preflight Requests and the OPTIONS Method

**CORS (Cross-Origin Resource Sharing)**:
- A mechanism to allow or restrict requested resources on a web server depending on where the HTTP request was initiated.

### Preflight Requests:
- **Purpose**: To determine if the server will allow a cross-origin request before sending the actual request.
- **Triggered**: Automatically by the browser for HTTP methods like `PUT`, `DELETE`, `PATCH`, or if custom headers are set.

### OPTIONS Method:
- **Role**: Used to perform a preflight request.
- **Response**: Server responds with allowed methods, headers, and origins.

### Example:
1. **Preflight Request**:
   - Method: `OPTIONS`
   - Headers: `Access-Control-Request-Method`, `Access-Control-Request-Headers`

2. **Server Response**:
   ```http
   HTTP/1.1 200 OK
   Access-Control-Allow-Origin: *
   Access-Control-Allow-Methods: POST, GET, OPTIONS
   Access-Control-Allow-Headers: X-Custom-Header
   ```

### Summary:
Preflight requests ensure that the actual request is safe to send. They are automatically handled by the browser and involve an `OPTIONS` request to the server to check for allowed methods and headers.