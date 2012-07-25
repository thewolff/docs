# Displaying Status Entities

Special care must be taken when displaying status entities.

To access data from the API, a customer must have accepted Mass Relevance's
API usage agreement. This includes agreeing to comply with [Twitter Display
Guidelines](https://dev.twitter.com/terms/display-guidelines) when
displaying Twitter statuses. This document is supposed to supplement
Twitter's guidelines and not replace or supersede it.

*Twitter Display Guidelines*<br />
https://dev.twitter.com/terms/display-guidelines

## Anatomy of a Tweet

<div style="text-align: center;">
  <img src="/MassRelevance/docs/raw/master/dev/usage/anatomy.png" alt="" />
</div>

### Deriving URLs


The API will not provide you with relevant URLs for permalinks and profiles, etc. This is how you can build relevant URLs using tweet data.

_Assume that the a tweet's data is saved in a variable named `tweet`_

 * Tweet URL (permalink): `https://twitter.com/{{tweet.user.screen_name}}/status/{{tweet.id_str}}`
 * Tweet author's profile URL: `https://twitter.com/{{tweet.user.screen_name}}`
 * Avatar image URL: `{{tweet.user.profile_image_url}}`
 * Avatar image secure URL: `{{tweet.user.profile_image_url_https}}`
 * Reply to tweet URL: `https://twitter.com/intent/tweet?in_reply_to={{tweet.id_str}}`
 * Retweet tweet URL: `https://twitter.com/intent/retweet?tweet_id={{tweet.id_str}}`
 * Favorite tweet URL: `https://twitter.com/intent/favorite?tweet_id={{tweet.id_str}}`

**More info:** Twitter action URLs (aka "intents") https://dev.twitter.com/docs/intents

## Auto-linking t.co URLs with correct display URLs

As part of Twitter's analytics initiative they replace all URLs within a tweet with a "t.co" URL that you *must* preserve within a tweet. However these t.co links look ugly and hide what URL a person is linking to. The API includes the URL needed to replace the t.co link for display via the `entities` object within a tweet.

**More info:**

 * t.co best practices https://dev.twitter.com/docs/tco-url-wrapper/best-practices
 * Dev FAQ on t.co https://dev.twitter.com/docs/tco-link-wrapper/faq
 * General FAQ on t.co https://support.twitter.com/entries/109623

### Entities object example

Below is an example of the `entities` hash. The relevant portion to use when auto-linking is the `urls` child object

**More info:** About Twitter entities https://dev.twitter.com/docs/tweet-entities

```json
"entities": {
    "hashtags": [{
        "text": "2012Olympics",
        "indices": [
        89, 102]
    }, {
        "text": "Olympics",
        "indices": [
        103, 112]
    }],
    "urls": [{
        "url": "http://t.co/zgkQdeyG",
        "expanded_url": "http://www.nbcolympics.com/video/swimming/natalie-coughlin-profile-409643.html",
        "display_url": "nbcolympics.com/video/swimming…",
        "indices": [
        68, 88]
    }],
    "user_mentions": [{
        "screen_name": "NatalieCoughlin",
        "name": "Natalie Coughlin",
        "id": 26593416,
        "id_str": "26593416",
        "indices": [
        11, 27]
    }]
}
```

### Pseudo code for auto-linking
    
```ruby
tweet = get_newest_tweet()
tweet_text = tweet.text

url_entities = tweet.entities.urls
foreach entity in url_entities
  tco_url = entity.url
  display_url = entity.display_url
  
  # note: you must continue to link to the t.co link
  html_link = "<a href=\"#{tco_url}\">#{display_url}</a>"
  
  # replace tco with html link
  tweet_text = tweet_text.replace(tco_url, html_link)
end

print tweet_text
```

Twitter provides many open-source client libraries to correctly display and link
statuses

 * [JavaScript](https://github.com/twitter/twitter-text-js)
 * [Ruby](https://github.com/twitter/twitter-text-rb)
 * [Java](https://github.com/twitter/twitter-text-java)
 * [Objective C](https://github.com/twitter/twitter-text-objc)

### Rendering retweets

Retweets are tricky because the person that retweeted is the top level data that comes with a tweet. If you do not take any steps to handle retweets then nothing will break, but you won't see the original tweet's avatar, etc.

#### Pesudo on how we handle retweets


```ruby    
tweet = get_newest_tweet()

# it's a retweet if the tweet object contains
# the `retweeted_status` property
is_retweet = tweet.retweeted_status != nil

if is_retweet
  # user that pressed "retweet" button
  retweeter = tweet.user

  # make the original tweet that was retweeted the main tweet
  tweet = tweet.retweeted_status
  
  # now set the user info of the person that pressed
  # "retweet" on the retweeted tweet
  tweet.retweeter = retweeter
  tweet.is_retweet
end

render(tweet)
```

Mass Relevance has found that by augmenting the way the data of a retweet is stored, it allows us to reuse templates easier while displaying a retweet as Twitter.com would.
