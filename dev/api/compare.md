# Compare API

Provides an entity volume comparison, in percentages, between multiple streams. This is commonly used in social polls (like Hashtag Battles) to identify, in realtime, the volume of one topic vs others.

## Resource URL

http://tweetriver.com/compare.:format?streams=:full_stream_names

format: `json`, `xml`<br />
full_stream_names: a comma-delimited set of full stream names in the format of :account/:stream_name (e.g. `bdainton/kindle`)<br />

**Example URL:** http://tweetriver.com/compare.json?streams=bdainton/kindle,MassRelDemo/galaxy-topic1,MassRelDemo/galaxy-topic2

In this example, the response will sum the total number approved entities in the 3 specified streams (bdainton/kindle, MassRelDemo/galaxy-topic1, and MassRelDemo/galaxy-topic2), and provide the percentages that each stream's approved total represents.

## Standard Parameters

<table>
  <tr>
    <td>
      <strong>streams</strong>
    </td>
    <td>string</td>
    <td>
      Comma-delimited set of full stream names (:account/:stream_name) that will be compared.
    </td>
  </tr>
  <tr>
    <td>
      <strong>target</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>
      Instead of returning a stream's percentage of the total, indicate a stream's percentage progress towards the specified target value.
    </td>
  </tr>
</table>

## Example Response (Standard Comparison)

This is a standard compare request, asking for the volume percentages for 3 streams. Percentage values max out at 100.

    $ curl http://tweetriver.com/compare.json?streams=bdainton/kindle,MassRelDemo/galaxy-topic1,MassRelDemo/galaxy-topic2

Here is the response:

```json
 {
   "streams": [
     {
       "pct": 85,
       "approved_tpm": 0,
       "full_name": "bdainton/kindle",
       "name": "kindle",
       "tpm": 11,
       "count": {
         "total": 19956921,
         "rejected": 14237556,
         "pending": 5703592,
         "approved": 15773
       },
       "description": "The Twitterverse has some good things to say about the Amazon Kindle.",
       "created_at": "2010-09-21T19:18:20Z"
     },
     {
       "pct": 9,
       "approved_tpm": 0,
       "full_name": "MassRelDemo/galaxy-topic1",
       "name": "galaxy-topic1",
       "tpm": 0,
       "count": {
         "total": 1792,
         "rejected": 0,
         "pending": 0,
         "approved": 1792
       },
       "description": "Topic 1",
       "created_at": "2012-02-03T15:17:01Z"
     },
     {
       "pct": 6,
       "approved_tpm": 0,
       "full_name": "MassRelDemo/galaxy-topic2",
       "name": "galaxy-topic2",
       "tpm": 0,
       "count": {
         "total": 780,
         "rejected": 0,
         "pending": 0,
         "approved": 780
       },
       "description": "Topic 2",
       "created_at": "2012-02-03T15:18:50Z"
     }
   ]
 }
```

## Example Response (Targeted Comparison)

This is the same compare request, but instead of comparing the stream volumes against one another, we're comparing against a specific volume target of 5000 entities. Each stream's percentage value is relative to the target.

    $ curl http://tweetriver.com/compare.json?streams=bdainton/kindle,MassRelDemo/galaxy-topic1,MassRelDemo/galaxy-topic2&target=5000

The JSON response:

```json
{
  // the passed-in target value is echoed in the response
  "target": 5000,
  "streams": [
    {
      "count": {
        "total": 19957052,
        "rejected": 14237668,
        "pending": 5703610,
        "approved": 15774
      },
      "created_at": "2010-09-21T19:18:20Z",
      "tpm": 30,
      "full_name": "bdainton/kindle",
      "description": "The Twitterverse has some good things to say about the Amazon Kindle.",
      "name": "kindle",
      "pct": 100,
      "approved_tpm": 0
    },
    {
      "count": {
        "total": 1792,
        "rejected": 0,
        "pending": 0,
        "approved": 1792
      },
      "created_at": "2012-02-03T15:17:01Z",
      "tpm": 0,
      "full_name": "MassRelDemo/galaxy-topic1",
      "description": "Topic 1",
      "name": "galaxy-topic1",
      "pct": 35,
      "approved_tpm": 0
    },
    {
      "count": {
        "total": 780,
        "rejected": 0,
        "pending": 0,
        "approved": 780
      },
      "created_at": "2012-02-03T15:18:50Z",
      "tpm": 0,
      "full_name": "MassRelDemo/galaxy-topic2",
      "description": "Topic 2",
      "name": "galaxy-topic2",
      "pct": 15,
      "approved_tpm": 0
    }
  ]
}```
