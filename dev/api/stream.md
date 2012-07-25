# Stream API

Provides approved status entities from a stream sorted from most recently approved to least recently approved (essentially reverse chronological order).

## Resource URL

http://tweetriver.com/:account/:stream_name.:format

account: the stream owner's account name (e.g. `bdainton`)<br />
stream_name: the name of the stream (e.g. `kindle`)<br />
format: `json`, `xml`<sup>1</sup>, `atom`<sup>2</sup>, `rss`<sup>2</sup>

**Example URL:** http://tweetriver.com/bdainton/kindle.json

    $ curl http://tweetriver.com/bdainton/kindle.json

## Standard Parameters

<table>
  <tr>
    <td>
      <strong>limit</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>integer</td>
    <td>50</td>
    <td>
      Number of status entities to return
      <br /><br/><strong>Note: Max value of 200</strong>
    </td>
  </tr>
  <tr>
    <td>
      <strong>since_id</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Only include status entities approved <em>after</em> supplied status entity `id` biasing towards real-time
      <br /><br />
      <strong>Note:</strong> API will return from the newest status entity to the supplied entity (but not including) or until `limit` is reached. Either `since_id`, `from_id`, or `since_id` can be used per request.
    </td>
  </tr>
  <tr>
    <td>
      <strong>from_id</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Only include status entities approved <em>after</em> supplied status entity `id` without skipping over status entities. It is noteworthy that `since_id` is prefered
      <br /><br />
      <strong>Note:</strong> API will return from the newest status entity to the supplied entity (but not including) or until `limit` is reached. Either `since_id`, `from_id`, or `since_id` can be used per request.
    </td>
  </tr>
  <tr>
    <td>
      <strong>start</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Only include status entities approved <em>before</em> supplied status entity `id`
      <br /><br />
      <strong>Note:</strong> Either `since_id`, `from_id`, or `since_id` can be used per request.
    </td>
  </tr>
  <tr>
    <td>
      <strong>callback</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Enabled JSONP support. Wraps JSON response with a JavaScript function of given name.
      <br /><br />
      <strong>Note:</strong> Only `json` endpoint support
    </td>
  </tr>
  <tr>
    <td>
      <strong>geo_hint</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>bit</td>
    <td>0</td>
    <td>
      Adds inferred (if it can be) status entity location from the authoring user's
profile information. The data is added the to `geo_hint` property of a
Twitter status entity.
      <br /><br />
      <strong>Note:</strong> Only for Twitter statuses
    </td>
  </tr>
  <tr>
    <td>
      <strong>replies</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>bit</td>
    <td>0</td>
    <td>Include the status entity that a status entity replied to</td>
  </tr>
</table>

## Advanced Parameters

<table>
  <tr>
    <td>
      <strong>strip_links</strong><sup>3</sup>
      <br /><span style="color: #333;">Broadcast Only</span>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>bit</td>
    <td>0</td>
    <td>
      Removes trailing URLs from the text a status entity.
    </td>
  </tr>
  <tr>
    <td>
      <strong>keywords</strong>
      <br /><span style="color: #333;">Needs Authorization</span>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Return only entities that contain the keywords specified.
    </td>
  </tr>
</table>


<sup>1</sup>Our docs only cover the `json` API, but the `xml` endpoint supports the same query parameters as the `json` endpoint and a similar response to the `json` endpoint.

<sup>2</sup>Exclusively for television broadcast. You must not publicly display data from these feeds without consent from Mass Relevance.

<sup>3</sup>Exclusively for television broadcast. You must not use this functionality without consent from Mass Relevance.
