# Polling Streams

The stream API is traversable, and will only return a fraction of the
data availble at a time.

The stream API was heavely influenced by Twitter's timeline APIs. Twitter's developer center
has [great documentation on how to use traversable APIs](https://dev.twitter.com/docs/working-with-timelines).

 * [Step-by-step](#step-by-step)
 * [Pseudo code](#pseudo-code)
 * [Frequency of polling](#frequency-of-polling)
 * [Difference between since_id, from_id, and start](since_id-vs-from_id-vs-start)
 * [If a supplied entity is not in the stream](if-a-supplied-entity-is-not-in-the-stream)

## Step-by-step

For the sake of this example, you are getting status entities about the Amazon Kindle using the following endpoint

http://tweetriver.com/bdainton/kindle.json

### Request the first set of items

Request the newest 50 items in the stream.

    curl http://tweetriver.com/bdainton/kindle.json?limit=50

### Request newer items

Use the `entity_id` property of the first status entity returned as the
value for the `since_id` param of the next request.

Status entities are sorted in **reverse chronological order** (most recently approved on top). Use the `since_id` param to get newer status entities. Set the value of `since_id` to the value of the `entity_id` property from the top most status entity in the array (index=0). If there were no entities in the last response, then continue to use the value from before.

    curl http://tweetriver.com/bdainton/kindle.json?limit=50&since_id=228210196055486464

### Request older items

Similar to requesting newer items. After the initial requests, use the
`entity_id` property of the first status entity returned as the value
for the `start` param of the next request.

    curl http://tweetriver.com/bdainton/kindle.json?limit=50&start=227581759888453632

## Pseudo code

```ruby
last_since_id = nil
base_url = "http://tweetriver.com/mr_nbc_oly/sport-swimming.json"
while true
  params = { "limit": 50 }

  # set the since_id if it exists
  if last_since_id != nil
    params["since_id"] = last_since_id
  end

  # get array of tweets
  url = generate_url(base_url, params)
  tweets = get_tweets(url)

  if tweets && tweets.length > 0
    newest_tweet = tweets[0]
    last_since_id = newest_tweet.entity_id
  end

  sleep(30) # wait 30 seconds before polling again
end
```

## Other considerations

### Frequency of polling

Limit polling to once every 15 seconds per stream per
client/browser (four times per minute).

Contact Mass Relevance if you plan on making requests at a higher rate.

### since_id vs. from_id vs. start

Each parameter will give you a different slice of a stream.

#### since_id

`since_id` will give you newer entities, not including the supplied entity, in a stream from the newest in the stream until `limit` is reached or until the supplied entity is reached (which ever is first). Essentially it will ensure that the polling stays realtime.

#### from_id

`from_id` will give you newer entities, not icluding the supplied
entity, in a stream from the supplied entity until the newest (top most)
entity is reach or until `limit` reached. Essentially it will ensure you
*see* every tweet in a stream, however it is likely that you will not
remain realtime. Using **`since_id` instead of `from_id` is highly recommended**.

#### start

`start` will give you older entities, not including the supplied entity, in a stream from the supplied entity.

If more than one is supplied the first of the following supplied is used: `since_id`, `from_id`, `start`.

### If a supplied entity is not in the stream

The API will return the newest status entity in a stream (just one).
