# slogctx

slogctx provides a slog [Handler](https://pkg.go.dev/log/slog#Handler) that wraps around
another Handler and appends attributes that was added do the context using the `Attach`
function, before logging.

Example:

```go
var h slog.Handler = slog.NewJSONHandler(os.Stdout, nil)
h = slogctx.NewHandler(h)
l := slog.New(h)

ctx := context.Background()
ctx = slogctx.Attach(ctx, slog.String("k1", "v1"), slog.Int("k2", 2))

l.InfoContext(ctx, "my message")

// Output:
// {"time":"2024-02-17T14:31:26.573761853+01:00","level":"INFO","msg":"my message","k1":"v1","k2":2}
```
