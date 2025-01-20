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

## Detect outliers

### Detect spikes in volume

```spl
index=netdns sourcetype="MSAD:NT6:DNS" 
```| append 
    [makeresults count=8000
    | eval time=now()-7200
    | eval _time=time, kallekula="outlier"]```
| timechart count as num_events partial=f
| streamstats window=10 current=true avg("num_events") as avg stdev("num_events") as stdev
| eval stdev=stdev*2
| eval lowerBound=(avg-stdev)
| eval upperBound=(avg+stdev) 
| eval is_outlier=if('num_events' < lowerBound OR 'num_events' > upperBound, 1, 0)
| fields - stdev, - avg
```

## Time token - post search

```spl
| eval tte="$time_token.earliest$"
| eval tte_orig=tte
| eval tte=if(match(tte,"now"),0,tte)
| eval tte=if(tte<1,"1000",tte)
| eval tte=relative_time(now(),tte)
| eval tte=if(tte_orig<1,0,tte)
| eval tte=if(len(tte_orig)>8,tte_orig,tte)

| eval ttl="$time_token.latest$"
| eval ttl_orig=ttl
| eval ttl=if(len(ttl)<1,"now",ttl)
| eval ttl=if(match(ttl,"now"),now(),relative_time(now(),ttl))
| eval ttl=if(len(ttl_orig)>8,ttl_orig,ttl)

| eval epoch_time=_time
| eval within=if(epoch_time<ttl AND epoch_time>tte,1,0)
| where within=1
```
