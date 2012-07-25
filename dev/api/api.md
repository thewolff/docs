# API

Generic information about our API capabilites

## Host name

`tweetriver.com`

Unless otherwise noted please use this domain

**Example URL:** http://tweetriver.com/bdainton/kindle.json

## SSL

`tweetriver.com` supports requests over SSL. Use `https` as the protocol
instead of `http`

**Example URL:** https://tweetriver.com/bdainton/kindle.json

## Status codes

When possible we respond with valid response codes (200 for valid requests, 404 for streams that do not exist, and 500 for things that are the servers fault). However the API does not support "304 Not Modified" responses.

## Encoding (gzip)

The API can gzip responses. We prefer clients enabling this because it makes your app performance better and decreases our bandwidth costs.

To enable gzip ensure the HTTP client has the `Accept-Encoding: gzip` header added to requests.

## JSONP

Most of the `json` endpoints support JSONP requests. Use `callback` or
`jsonp` query parameter on `json` endpoints.
