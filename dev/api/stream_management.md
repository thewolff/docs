# Stream Management API

You can clone, edit, and delete streams using your [API Key](http://massrelevance.com/profile/edit).

# Cloning streams

## Resources URL

POST http://tweetriver.com/streams/:id

id: the stream's id (e.g. `123`)<br />

**Example URL:** http://tweetriver.com/streams/123

## Standard Parameters

<table>
  <tr>
    <td>
      <strong>api_key</strong>
      <br /><span style="color: #999;">required</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Your API key. You can find it here: http://massrelevance.com/profile/edit
    </td>
  </tr>
  <tr>
    <td>
      <strong>name</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Name of stream. Defaults to the original stream's name with a modifier number appended.
    </td>
  </tr>
  <tr>
    <td>
      <strong>keywords</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Keywords to source. Defaults to original stream's keywords.
    </td>
  </tr>
  <tr>
    <td>
      <strong>description</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Stream's description. Defaults to original stream's description.
    </td>
  </tr>
 </table>
 
## Advanced Parameters

<table>
  <tr>
    <td>
      <strong>enabled_at</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>timestamp</td>
    <td></td>
    <td>
      Time you want to enable your stream. Defaults to enabled on create.
    </td>
  </tr>
  <tr>
    <td>
      <strong>disabled_at</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>timestamp</td>
    <td></td>
    <td>
      Time you want to disable your stream. Defaults to never.
    </td>
  </tr>
  <tr>
    <td>
      <strong>disabled</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>bit</td>
    <td>0</td>
    <td>
      Creates a disabled stream.
    </td>
  </tr>
</table>

## Response

The response is a JSON hash. See below.

## Example Request

    $ curl -X POST --data "name=new-stream;keywords=new keywords;description=my new stream;api_key=YOUR_API_KEY" \
      http://massrelevance.com/streams/STREAM_ID/clone

```json
{
  "data": {
    "public_url":"http://massrelevance.com/YOUR_LOGIN/new-stream",
    "stream_id":26941,
    "url":"http://massrelevance.com/streams/NEW_STREAM_ID"
  },
  "status":"success"
}
```

# Editing streams

## Resources URL

PUT http://tweetriver.com/streams/:id

## Standard Parameters

<table>
  <tr>
    <td>
      <strong>api_key</strong>
      <br /><span style="color: #999;">required</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Your API key. You can find it here: http://massrelevance.com/profile/edit
    </td>
  </tr>
  <tr>
    <td>
      <strong>stream[description]</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Modify the stream's description.
    </td>
  </tr>
</table>

## Example Request

    $ curl -X PUT --data "stream[description]=hi;api_key=YOUR_API_KEY" \
      http://massrelevance.com/streams/YOUR_STREAM

```json
{"data":{},"status":"success"}
```

# Deleting streams

## Resource URL

DELETE http://tweetriver.com/streams/:id 

## Standard Parameters

<table>
  <tr>
    <td>
      <strong>api_key</strong>
      <br /><span style="color: #999;">required</span>
    </td>
    <td>string</td>
    <td></td>
    <td>
      Your API key. You can find it here: http://massrelevance.com/profile/edit
    </td>
  </tr>
</table>

## Example Request

    $ curl --request DELETE -d 'api_key=YOUR_API_KEY' http://massrelevance.com/streams/STREAM_ID

```json
{
  "data": {
    "public_url":"http://massrelevance.com/YOUR_LOGIN/STREAM_NAME",
    "url":"http://massrelevance.com/streams/STREAM_ID"
  },
  "status":"success"
}
```