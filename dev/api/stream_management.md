# Stream Management API

You can clone, edit, and delete streams using your [API Key](http://massrelevance.com/profile/edit).

# Cloning streams

## Resources URL

http://tweetriver.com/streams/:id

id: the stream's id (e.g. `123`)<br />

**Example URL:** http://tweetriver.com/streams/123

## Standard Parameters

<table>
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
    <td>boolean</td>
    <td></td>
    <td>
      Creates a disabled stream. Defaults to `false`.
    </td>
  </tr>
</table>

## Response

The response is a JSON hash. See below.

## Example Request

    curl -X POST --data "name=new-stream;keywords=new keywords;description=my new stream;api_key=YOUR_API_KEY" \
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

## Editing streams

You can edit streams:

    curl -X PUT --data "stream[description]=hi;api_key=YOUR_API_KEY" \
      http://massrelevance.com/streams/YOUR_STREAM

Which will reply with:

    {"data":{},"status":"success"}

## Deleting streams

You can delete streams:

    curl --request DELETE -d 'api_key=YOUR_API_KEY' http://massrelevance.com/streams/STREAM_ID

Which will reply with:

    {"data":{"public_url":"http://massrelevance.com/YOUR_LOGIN/STREAM_NAME","url":"http://massrelevance.com/streams/STREAM_ID"},"status":"success"} 
