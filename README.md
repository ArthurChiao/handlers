handlers
================

The direct reason of this fork from [`gorilla/handlers`](github.com/gorilla/handlers) is that the logging handlers in
`gorilla/handlers` doesn't contain response time information, which not
satifies some monitoring cases, e.g. API response time over time.

## Changes of this fork with upstream `gorilla/handlers`

* LoggingHandler: add `response time` (in `ms`) as the last field
* CombinedLoggingHandler: add `response time` (in `ms`) as the last field

For original docs, see github.com/gorilla/handlers.

## Example

A simple example using `handlers.LoggingHandler` and `handlers.CompressHandler`:

```go
import (
    "net/http"
    "github.com/arthurchiao/handlers"
)

func main() {
    r := http.NewServeMux()

    // Only log requests to our admin dashboard to stdout
    r.Handle("/admin", handlers.LoggingHandler(os.Stdout, http.HandlerFunc(ShowAdminDashboard)))
    r.HandleFunc("/", ShowIndex)

    // Wrap our server with our gzip handler to gzip compress all responses.
    http.ListenAndServe(":8000", handlers.CompressHandler(r))
}
```

## License

BSD licensed. See the included LICENSE file for details.
