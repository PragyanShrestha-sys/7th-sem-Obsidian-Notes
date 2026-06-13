
| Code | Meaning |
|------|---------|
| 200 | OK (Success) |
| 201 | Created (POST successful) |
| 301 | Moved Permanently (redirect) |
| 400 | Bad Request (client error) |
| 401 | Unauthorized (need login) |
| 403 | Forbidden (no permission) |
| 404 | Not Found |
| 500 | Internal Server Error |

```java
switch (conn.getResponseCode()) {
    case HttpURLConnection.HTTP_OK:
        System.out.println("Success!");
        break;
    case HttpURLConnection.HTTP_NOT_FOUND:
        System.out.println("Page not found!");
        break;
    case HttpURLConnection.HTTP_INTERNAL_ERROR:
        System.out.println("Server error!");
        break;
}
```
