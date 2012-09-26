# Stream Meta API

Provides information about and derived from the entities in a stream.

All streams have, by default, a set of meta information captured about them as they live. Most notably, this information includes...

<strong>counts</strong>:  total number of entities in a stream, split by their moderation state (pending, approved, rejected)<br />
<strong>activity</strong>: arrays of per-minute, per-hour, and per-day counts<br />

This [basic/standard meta information](#standard-meta-information)  is commonly used to render such visualizations as counters, progress meters, and social poll results.

Additionally, on a stream-by-stream basis, there are many advanced features that may be turned on (by Mass Relevance administrators). These features include...

<strong>top retweeted tweets</strong>: (Twitter only) the tweets in a stream that have been retweeted the most<br />
<strong>top hashtags</strong>: the hashtags that have been used the most over the last hour<br />
<strong>top links</strong>: the URLs that have been referenced the most over the last 18 hours<br />
<strong>top contributors</strong>: (Twitter only) the Twitter users whose tweets have been retweeted or replied to the most within the stream<br />
<strong>top topics</strong>: a tally of the number of times that specific keyword sets have been mentioned in the stream<br />
<strong>top moments</strong>: an extension to top topics, capturing the minutes (moments) when individual topics peaked in activity<br />

This [advanced stream meta information](#advanced-meta-information) is commonly used to render various leaderboard visualizations.

## Resource URL

http://tweetriver.com/:account/:stream_name/meta.:format

account: the stream owner's account name (e.g. `bdainton`)<br />
stream_name: the name of the stream (e.g. `kindle`)<br />
format: `json`, `xml`<sup>1</sup>

**Example URL:** http://tweetriver.com/bdainton/kindle/meta.json

## Parameters

### Standard

These parameters control the information you get back in the [basic/standard meta response](#standard-meta-information).

<table>
  <tr>
    <td>
      <strong>num_minutes</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>60</td>
    <td>
      Number of minutes of activity to include
      <br /><br/><strong>Note:</strong> Must be > 0
    </td>
  </tr>
  <tr>
    <td>
      <strong>num_hours</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>24</td>
    <td>
      Number of hours of activity to include
      <br /><br/><strong>Note:</strong> Must be > 0
    </td>
  </tr>
  <tr>
    <td>
      <strong>num_days</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>365</td>
    <td>
      Number of days of activity to include
      <br /><br/><strong>Note:</strong> Must be > 0
    </td>
  </tr>
  <tr>
    <td>
      <strong>activity</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>bit</td>
    <td>1</td>
    <td>
      Include `activity` and `count` properties in response
      <br /><br/><strong>Example values:</strong>0,1
      <br /><br/><strong>Note:</strong> Included by default
    </td>
  </tr>
  <tr>
    <td>
      <strong>finish</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td><em>now</em></td>
    <td>
      <a href="http://en.wikipedia.org/wiki/Unix_time">Unix time</a> of
the point of which activity data should end. This will be reflected by
the value of the last item of the minute activities.
      <br /><br/><strong>Note:</strong> Only use the seconds portion of
unix time (JavaScript will give use the number in milliseconds.
Divide by 1000).
    </td>
  </tr>
</table>

### Top Retweeted Tweets

This is an advanced feature<sup>2</sup>.

These parameters control the information you get back when requesting the [top retweeted tweets](#advanced-meta-information-top-retweeted-tweets) in a stream.

<table>
  <tr>
    <td>
      <strong>top_periods</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string(ish)</td>
    <td>a</td>
    <td>
      Include top tweets from specific hourly periods provided. "a" is
all time. "2012070412" is July 4, 2012 at 12PM UTC.
      <br /><br/><strong>Format:</strong> <em>yyyyMMddHH</em> in <a
href="http://developer.android.com/reference/java/text/SimpleDateFormat.html">Java
SimpleDateFormat</a> pattern<sup>3</sup>
      <br /><br/><strong>Example Values:</strong> a,2012070412
      <br /><br/><strong>Note:</strong> Accepts a string list delimited
by commas. All hour specified will be in UTC. Either `top_periods` or `top_periods_relative` can be used per request.
    </td>
  </tr>
  <tr>
    <td>
      <strong>top_periods_relative</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td></td>
    <td>
      Include top tweets from specific hourly periods ago from now. "0"
is right now. "1" is one hour ago.
      <br /><br/><strong>Example Values:</strong> 1,2,3
      <br /><br/><strong>Note:</strong> Accepts an integer list delimited by commas. Either `top_periods` or `top_periods_relative` can be used per request.
    </td>
  </tr>
  <tr>
    <td>
      <strong>top_count</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>5</td>
    <td>
      Number of tweets to include per period
    </td>
  </tr>
</table>

### Top Hashtags

This is an advanced feature<sup>2</sup>.

These parameters control the information you get back when requesting the [top discovered hashtags](#advanced-meta-information-top-hashtags) in a stream.

<table>
  <tr>
    <td>
      <strong>num_hashtags</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>10</td>
    <td>
      Number of discovered hashtags to return.
    </td>
  <tr>
</table>

### Top Links

This is an advanced feature<sup>2</sup>.

These parameters control the information you get back when requesting the [top discovered URLs/links](#advanced-meta-information-top-links) in a stream.

<table>
  <tr>
    <td>
      <strong>num_links</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>10</td>
    <td>
      Number of discovered URLs/links to return.
    </td>
  <tr>
</table>

### Top Contributors

This is an advanced feature<sup>2</sup>.

These parameters control the information you get back when requesting the [top contributors](#advanced-meta-information-top-contributors) in a stream.

<table>
  <tr>
    <td>
      <strong>num_contributors</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>10</td>
    <td>
      Number of contributor user handles return.
    </td>
  <tr>
</table>


### Top Topics

This is an advanced feature<sup>2</sup>.

These parameters control the information you get back when requesting the top topics in a stream.

<table>
  <tr>
    <td>
      <strong>num_trends</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>30</td>
    <td>
      Number of trends to return in response per bucket
      <br /><br/><strong>Note:</strong> Accepts a string list delimited
by commas
    </td>
  <tr>
  </tr>
    <td>
      <strong>disregard</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Exclude trends that match supplied values from buckets while trying to ensure `num_trends`
is met
      <br /><br/><strong>Example Values:</strong> obama,romney
      <br /><br/><strong>Note:</strong> Accepts a string list delimited
by commas
    </td>
  </tr>
</table>

### Top Moments

This is an advanced feature<sup>2</sup>.

These parameters control the information you get back when requesting the top moments in a stream.

<table>
  <tr>
    <td>
      <strong>top_moments</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string(ish)</td>
    <td>a</td>
    <td>
      Include moments from specific hourly periods provided. "a" is
all time. "2012070412" is July 4, 2012 at 12PM UTC.
      <br /><br/><strong>Format:</strong> <em>yyyyMMddHH</em> in <a
href="http://developer.android.com/reference/java/text/SimpleDateFormat.html">Java
SimpleDateFormat</a> pattern<sup>3</sup>
      <br /><br/><strong>Example Values:</strong> a,2012070412
      <br /><br/><strong>Note:</strong> Accepts a string list delimited
by commas. All hour specified will be in UTC. Either `top_moments` or `top_moments_relative` can be used per request.
    </td>
  </tr>
  <tr>
    <td>
      <strong>top_moments_relative</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td></td>
    <td>
      Include moments from specific hourly periods ago from now. "0"
is right now. "1" is one hour ago.
      <br /><br/><strong>Example Values:</strong> 1,2,3
      <br /><br/><strong>Note:</strong> Accepts an integer list delimited by commas. Either `top_moments` or `top_moments_relative` can be used per request.
    </td>
  </tr>
  <tr>
    <td>
      <strong>top_moments_count</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>1</td>
    <td>
      Number of moments to include per period
    </td>
  </tr>
</table>


## Example Requests

### Standard Meta Information

To get a stream's basic/standard count and activity rate information...

  $ curl http://tweetriver.com/bdainton/kindle.json

The response:

```json
{
  "name": "kindle",
  "full_name": "bdainton/kindle",
  "description": "The Twitterverse has some good things to say about the Amazon Kindle.",
  "created_at": "2010-09-21T19:18:20Z",
  "count": {
    "total": 19958828,
    "rejected": 14238898,
    "pending": 5704155,
    "approved": 15775
  },
  {
    "minute": {  // arrays of minute-by-minute counts
      "total": [],
      "rejected": [],
      "pending": [],
      "approved": []
    },
    "hourly": { // arrays of hour-by-hour counts
      "total": [],
      "rejected": [],
      "pending": [],
      "approved": []
    },
    "daily": { // arrays of day-by-day counts
      "total": [],
      "rejected": [],
      "pending": [],
      "approved": []
    }
  }
}
```


### Advanced Meta Information

A stream with other advanced features enabled will have far more information contained in its meta response.

  $ curl http://tweetriver.com/MassRelDemo/things-we-do/meta.json

The response:

```json
{
  // standard details
  "name": "things-we-do",
  "full_name": "MassRelDemo/things-we-do",
  "description": "This is what people are doing on Twitter.",
  "created_at": "2012-09-26T15:07:07Z",
  "count": {
    "total": 6210,
    "rejected": 314,
    "pending": 1260,
    "approved": 4636
  },
  "activity": {
    "daily": {},
    "hourly": {},
    "minute": {}
  },

  // top retweeted tweets
  "top": {},

  // a description of the time periods that have been returned in the above 'top' object
  "top_periods": [],

  // top hashtags
  "hashtags": [],

  // top links
  "links": [],

  // top contributors
  "contributors": [],

  // top topics
  "buckets": {},

  // top moments
  "moments": {},

  // a description of the time periods returned in the above 'moments' object
  "moments_periods": []
}
```

### Advanced Meta Information: Top Retweeted Tweets

Get the top retweeted tweets in this stream.

  $ curl http://tweetriver.com/MassRelDemo/things-we-do/meta.json?top_periods=a,20120926,2012092616&top_count=3

In this example, we're asking for the top 3 retweeted tweets in each for 3 specific time periods: all-time in this stream ('a'), within a specific day (Sept 26, 2012), and within a specific hour of that day (UTC 16:00, Sept 26, 2012).

The response:

```json
{
  // ... for this example, other meta details have been removed ...

  // top retweeted tweets
  "top": {
    "20120926": [
      {
        // ...top retweeted tweet 1 of the UTC Day Sept 26, 2012...
      },
      {
        // ...top retweeted tweet 2...
      },
      {
        // ...top retweeted tweet 3...
      }
    ],
    "2012092616": [
      {
        // ...top retweeted tweet 1 of the 16:00 UTC Hour Sept 26, 2012...
      },
      {
        // ...top retweeted tweet 2...
      },
      {
        // ...top retweeted tweet 3...
      }
    ],
    "a": [
      {
        // ...top retweeted tweet 1 of all time in this stream...
      },
      {
        // ...top retweeted tweet 2...
      },
      {
        // ...top retweeted tweet 3...
      }
    ]
  },

  // a description of the time periods that have been returned in the above 'top' object
  "top_periods": [
    "a",
    "20120926",
    "2012092616"
  ]
}
```

### Advanced Meta Information: Top Hashtags

Get the top discovered hashtags in this stream.

  $ curl http://tweetriver.com/MassRelDemo/things-we-do/meta.json?num_hashtags=5

The <em>count</em> indicated in the response indicates the number of approved entities <em>in the last hour</em> using that hashtag.

The response:

```json
{
  // ... for this example, other meta details have been removed ...

  // top hashtags
  "hashtags": [
    {
      "hashtag": "callmeoldfashioned",
      "count": 2409
    },
    {
      "hashtag": "m312",
      "count": 911
    },
    {
      "hashtag": "oomf",
      "count": 385
    },
    {
      "hashtag": "imhappiestwhen",
      "count": 385
    },
    {
      "hashtag": "lwwy",
      "count": 380
    }
  ]
}
```

### Advanced Meta Information: Top Links

Get the top discovered links in this stream.

  $ curl http://tweetriver.com/MassRelDemo/things-we-do/meta.json?num_links=5

The <em>count</em> indicated in the response indicates the number of approved entities <em>in the last 18 hours</em> containing that link.

The response:

```json
{
  // ... for this example, other meta details have been removed ...

  // top links
  "links": [
    {
      "count": 2194,
      "link": "http://youtu.be/jvHE70LZEOA"
    },
    {
      "count": 1079,
      "link": "http://viddy.it/PGptsX"
    },
    {
      "count": 360,
      "link": "http://www.massrelevance.com"
    },
    {
      "count": 300,
      "link": "http://x.co/oFxV"
    },
    {
      "count": 287,
      "link": "http://twitpic.com/ay2x06"
    }
  ]
}
```

### Advanced Meta Information: Top Contributors

Get the top contributors in this stream.

  $ curl http://tweetriver.com/MassRelDemo/things-we-do/meta.json?num_contributors=5

The <em>count</em> indicated in the response indicates the number of approved entities <em>in the last week</em> containing that user's handle (@name).

The response:

```json
{
  // ... for this example, other meta details have been removed ...

  // top links
  "contributors": [
    {
      "count": 39668,
      "name": "@techcrunch"
    },
    {
      "count": 21641,
      "name": "@mashable"
    },
    {
      "count": 8373,
      "name": "@intel"
    },
    {
      "count": 2768,
      "name": "@wired"
    },
    {
      "count": 2518,
      "name": "@drizzled"
    }
  ]
}
```


<sup>1</sup>Our docs only cover the `json` API, but the `xml` endpoint supports the same query parameters as the `json` endpoint and a similar response to the `json` endpoint.

<sup>2</sup>This feature is enabled on a stream by stream basis, by a Mass Relevance administrator (upon request). By default, this
feature is not enabled.

<sup>3</sup>I like Android's docs better for this class than Oracle's.
