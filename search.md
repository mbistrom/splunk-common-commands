# Useful SPL snippets

## Convert epoch time to human readable

```spl
| convert timeformat="%Y-%m-%d %H:%M:%S" ctime(_time) AS human_time
```
