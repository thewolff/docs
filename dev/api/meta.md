# Stream Meta API

Provides information about and derived from the entities in a stream.

## Resource URL

http://tweetriver.com/:account/:stream_name/meta.:format

account: the stream owner's account name (e.g. `bdainton`)<br />
stream_name: the name of the stream (e.g. `kindle`)<br />
format: `json`, `xml`<sup>1</sup>

**Example URL:** http://tweetriver.com/bdainton/meta.json

## Parameters

### Standard

<table>
  <tr>
    <td>
      <strong>num_minutes</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>60</td>
    <td>
      Number of minute activity to include
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
      Number of minute activity to include
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
      Number of minute activity to include
      <br /><br/><strong>Note:</strong> Must be > 0
    </td>
  </tr>
  <tr>
    <td>
      <strong>activity</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>1</td>
    <td>bit</td>
    <td>
      Include `activity` and `count` properties in response
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

### Topics<sup>2</sup>

*Topics feature needs to be enabled for a stream by Mass Relevance*

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

### Top Tweets<sup>2</sup>

*Top tweets feature needs to be enabled for a stream by Mass Relevance*

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

## Top Moments<sup>2</sup>

*Top moments feature needs to be enabled for a stream by Mass Relevance*

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


<sup>1</sup>Our docs only cover the `json` API, but the `xml` endpoint supports the same query parameters as the `json` endpoint and a similar response to the `json` endpoint.

<sup>2</sup>Feature enabled on a stream by stream basis. By default the
feature is not enabled.

<sup>3</sup>I like Android's docs better for this class than Oracle's.
