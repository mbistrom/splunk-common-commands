# Useful SPL snippets

## Convert epoch time to human readable

```spl
| convert timeformat="%Y-%m-%d %H:%M:%S" ctime(_time) AS human_time
```

## strftime

```spl
| eval time=strftime(_time, "%F %T")
```
```2024-05-03 10:02:33```

```spl
| eval time=strftime(_time, "%F %T %Z")
```
```2024-05-03 10:02:33 CEST```

```spl
| eval time=strftime(_time, "%Y-%m-%dT%H:%M:%S.%Q")
```
```2024-05-03T10:02:33.803```

```spl
| eval time=strftime(_time, "%A %B %d %Y")
```
```Friday May 03 2024```

```spl
| eval time=strftime(_time, "%Y-%m-%dT%H:%M:%S.%Q%z")
```
ISO 8601 ```2024-05-03T10:04:17.183+0200``` 
