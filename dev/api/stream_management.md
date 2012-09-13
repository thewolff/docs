# Stream Management API

You can clone, edit, and delete streams using your [API Key](http://massrelevance.com/profile/edit).

## Cloning streams

    curl -X POST --data "name=new-stream;keywords=new keywords;description=my new stream;api_key=YOUR_API_KEY" \
      http://massrelevance.com/streams/STREAM_ID/clone

Make sure you replace `STREAM_ID` with your stream's id.

This will return a JSON response:

    {"data":{"public_url":"http://massrelevance.com/YOUR_LOGIN/new-stream","stream_id":26941,"url":"http://massrelevance.com/streams/NEW_STREAM_ID"},"status":"success"}

Optional Parameters:

    name - name of stream
    keywords - keywords for stream
    description - description for stream
    enable_at - time you want to enable your stream
    disable_at - time you want to disable your stream
    delete_at - time you want to delete your stream
    disabled - disable sources

## Editing streams

You can edit streams:

    curl -X PUT --data "stream[description]=hi;api_key=060c1ece812c38e8c04714ecb201f505" \
      http://massrelevance.com/streams/YOUR_STREAM

Which will reply with:

    {"data":{},"status":"success"}

## Deleting streams

You can delete streams:

    curl --request DELETE -d 'api_key=YOUR_API_KEY' http://massrelevance.com/streams/STREAM_ID

Which will reply with:

   {"data":{"public_url":"http://massrelevance.com/YOUR_LOGIN/STREAM_NAME","url":"http://massrelevance.com/streams/STREAM_ID"},"status":"success"} 
