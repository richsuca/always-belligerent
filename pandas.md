# Pandas

## Get min(), max() value for all columns (only use for date, numbers, not string)
```
df.min()
df.max()
```

For strings, it returns the min/max of the first character only, use below for strings:

```
x = bf["routeCode"].str.len()
x.min(), x.max()
```

## Get column info
```
df.info()
```

## Set some columns as dates
```
bf = pd.read_csv('~/big.csv', parse_dates=['date', 'stopTimeSchedule', 'stopTimeReal'])
```

## Set two columns as String [^1]
```
bf = pd.read_csv('~/big.csv', parse_dates=['date', 'stopTimeSchedule', 'stopTimeReal'], 
                  dtype={'routeCode': pd.StringDtype(), 'serviceVehicle': pd.StringDtype()})
```

[^1]: to avoid object type, we can't apply min/max on object with mix number and string.

## Find rows where _Grade_ column isn't numeric
```
df = pd.read_csv('data/data_8.csv')
is_error = pd.to_numeric(df['Grade'], errors='coerce').isna()
df[is_error]
```
