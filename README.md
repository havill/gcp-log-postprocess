## Global Option Variables:
- `-v nohead=BOOLEAN`       Do not print a header on line 1 if true
- `-v show=id`              Show the id parameter for fast and slow methods
- `-v show=when`            Show local timestamps for the fast and slow methods
- `-v histogram=calls`      Show histogram for api calls over time
- `-v histogram=STRING`     Show histogram for api called 'method'/string over time
- `-v population=BOOLEAN`   Use population standard deviation if true
- `-v resolution=minutes`   Set time difference resolution to tens of minutes

## Input: RFC 4180 compliant CSV file with CRLF newlines generated by 'gcloud logging read' with at least the following fields:
- latency
- timestamp
- request_url

## Output: TSV (tab separated values) file with LF newlines with a histogram or call summary
- x̄ = sample mean (average)
- s = sample standard deviation
- μ = population mean (average)
- σ = population standard deviation

## Example Google Cloud SDK command:
```gcloud logging read 'httpRequest.userAgent:"menu/" AND (
      (timestamp >= \"2021-02-01T11:00:00+09\"
         AND timestamp < \"2021-02-01T14:00:00+09\") OR
      (timestamp >= \"2021-02-01T17:00:00+09\"
          AND timestamp < \"2021-02-01T22:00:00+09\")
      --format="csv(httpRequest.latency,timestamp,httpRequest.requestUrl)")'```
