[![Build Status](https://travis-ci.org/cloudfoundry-incubator/uaa-go-client.svg?branch=master)](https://travis-ci.org/cloudfoundry-incubator/uaa-go-client)

# uaa-go-client
A go library for Cloud Foundry [UAA](https://github.com/cloudfoundry/uaa)


## Example
This example client connects to UAA using https and skips cert verification.
```go
cfg := &config.Config{
  ClientName:       "client-name",
	ClientSecret:     "client-secret",
	UaaEndpoint:      "https://uaa.service.cf.internal:8443",
	SkipVerification: true,
}

uaaClient, err = client.NewClient(logger, cfg, clock)
if err != nil {
  log.Fatal(err)
  os.Exit(1)
}

fmt.Printf("Connecting to: %s ...\n", cfg.UaaEndpoint)

token, err = uaaClient.FetchToken(true)
if err != nil {
  log.Fatal(err)
  os.Exit(1)
}

fmt.Printf("Token: %#v\n", token)
```

## Example command line
This example client connects to UAA using https, skips cert verification and fetches a token.

```
Usage: <client-name> <client-secret> <uaa-url> <skip-verification>
```

```
$ go run examples/main.go gorouter gorouter-secret https://uaa.service.cf.internal:8443 true

Connecting to: https://uaa.service.cf.internal:8443 ...
Response:
	token: eyJhbGciOiJSUzI1NiJ9.eyJqdGkiOiJlOGQ3NWJiNi1kMGMxLTRmMjEtYWMyMy05ZGRiNmY2MWI3ZjkiLCJzdWIiOiJnb3JvdXRlciIsImF1dGhvcml0aWVzIjpbInJvdXRpbmcucm91dGVzLnJlYWQiXSwic2NvcGUiOlsicm91dGluZy5yb3V0ZXMucmVhZCJdLCJjbGllbnRfaWQiOiJnb3JvdXRlciIsImNpZCI6Imdvcm91dGVyIiwiYXpwIjoiZ29yb3V0ZXIiLCJncmFudF90eXBlIjoiY2xpZW50X2NyZWRlbnRpYWxzIiwicmV2X3NpZyI6IjdmNTE1MmQyIiwiaWF0IjoxNDU0NzA5NTUxLCJleHAiOjE0NTQ3NTI3NTEsImlzcyI6Imh0dHBzOi8vdWFhLmJvc2gtbGl0ZS5jb20vb2F1dGgvdG9rZW4iLCJ6aWQiOiJ1YWEiLCJhdWQiOlsiZ29yb3V0ZXIiLCJyb3V0aW5nLnJvdXRlcyJdfQ.QSdLbdhDFWQXSJ3lPbTVUCj6zEH1DUPU3V-x8lX48qOPg99snalEEIBX5y5Ki6mZLWJ9p6UUIH1xANz4mGATcBIO282wcRBK0Pbc-r1OkjFNJTvwdV75kP9ovbGXGNbQZMksEvEtgOQ_icz7XsJrkTxtV29uPYDpKHbxtvqpPeU
	expires: 43199
```
