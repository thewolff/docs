# Stream API

Provides approved status entities from a stream sorted from most recently approved to least recently approved (in most cases, this is reverse chronological order).

## Resource URL

http://tweetriver.com/:account/:stream_name.:format

account: the stream owner's account name (e.g. `bdainton`)<br />
stream_name: the name of the stream (e.g. `kindle`)<br />
format: `json`, `xml`<sup>1</sup>, `atom`<sup>2</sup>, `rss`<sup>2</sup>

**Example URL:** http://tweetriver.com/bdainton/kindle.json

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
      <strong>Note:</strong> API will return from the newest status entity to the supplied entity (but not including) or until `limit` is reached. Usage of `since_id`, `from_id`, and `start` is mutually exclusive; only one of these paramteres may be used in a single request.
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
      Only include status entities approved <em>before</em> supplied status entity `id`. This parameter is commonly used to implement 'More' functionality on a stream of content, wherein an end user sees a stream of content, then clicks on a 'More' link to display the next N entities. By supplying the `id` of the last viewed entity, you may request the set of entities that came before it in the stream.
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
      Enabled JSONP support. Wraps JSON response with a JavaScript function of given name. `jsonp` is a supported alias.
      <br /><br />
      <strong>Example Values:</strong> <pre>myfunction</pre>
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
      <strong>Note:</strong> Only for Twitter statuses. <a href="#geo-hint-object">More info below</a>
    </td>
  </tr>
  <tr>
    <td>
      <strong>replies</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>bit</td>
    <td>0</td>
    <td>Include the status entity that a status entity replied to. The
status entity is added to the `in_reply_to` property of a Twitter status
entity.</td>
  </tr>
  <tr>
    <td>
      <strong>reverse</strong>
      <br /><span style="color: #999;">optional</span>
    </td>
    <td>bit</td>
    <td>0</td>
    <td>Reverse the status entities in response to be in chronological order
(default is reverse chronolical order) so that entities approved earlier
are on top.</td>
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

## Response

The response is a JSON array. If no entities are available, then the response will be an empty JSON array. If an error occurs then the response will be empty (whitespace).

## Example Request

    $ curl http://tweetriver.com/bdainton/kindle.json

```json
[
 // this is a Tweet/Status response
 // https://dev.twitter.com/docs/api/1/get/statuses/show/%3Aid
 {
    // data added by Mass Relevance
    // mostly useless or for backwards compatibility
    "chained_stream_id": null,
    "adhoc_for_stream_id": null,
    "requeued": null,
    "entity_id": "200249547354669056", // == id_str
    "order_id": "200249547354669056",  // == id_str
    "score": "200249547354669056",     // == id_str

    "created_at": "Wed May 09 15:43:07 +0000 2012",
    "id": 200249547354669060,
    "id_str": "200249547354669056",
    "text": "Love this! @NatalieCoughlin Profile - Swimming Video | NBC Olympics http://t.co/zgkQdeyG #2012Olympics #Olympics",
    "source": "<a href=\"http://twitter.com/tweetbutton\" rel=\"nofollow\">Tweet Button</a>",
    "truncated": false,
    "in_reply_to_status_id": null,
    "in_reply_to_status_id_str": null,
    "in_reply_to_user_id": null,
    "in_reply_to_user_id_str": null,
    "in_reply_to_screen_name": null,
    "user": {
        "id": 20971136,
        "id_str": "20971136",
        "name": "Megan Coughlin",
        "screen_name": "MeganCoughlin",
        "location": "San Francisco, CA",
        "description": "SMB AE (midwest) at @InsideView, a Sales 2.0 company | Swimming Enthusiast | Gluten-free fanatic | http://www.linkedin.com/in/meganccoughlin ",
        "url": null,
        "protected": false,
        "followers_count": 641,
        "friends_count": 618,
        "listed_count": 9,
        "created_at": "Mon Feb 16 08:38:45 +0000 2009",
        "favourites_count": 0,
        "utc_offset": -32400,
        "time_zone": "Alaska",
        "geo_enabled": false,
        "verified": false,
        "statuses_count": 391,
        "lang": "en",
        "contributors_enabled": false,
        "is_translator": false,
        "profile_background_color": "709397",
        "profile_background_image_url": "http://a0.twimg.com/images/themes/theme6/bg.gif",
        "profile_background_image_url_https": "https://si0.twimg.com/images/themes/theme6/bg.gif",
        "profile_background_tile": false,
        "profile_image_url": "http://a0.twimg.com/profile_images/1780753484/headshot_normal.jpg",
        "profile_image_url_https": "https://si0.twimg.com/profile_images/1780753484/headshot_normal.jpg",
        "profile_link_color": "FF3300",
        "profile_sidebar_border_color": "86A4A6",
        "profile_sidebar_fill_color": "A0C5C7",
        "profile_text_color": "333333",
        "profile_use_background_image": true,
        "show_all_inline_media": false,
        "default_profile": false,
        "default_profile_image": false,
        "following": null,
        "follow_request_sent": null,
        "notifications": null
    },
    "geo": null,
    "coordinates": null,
    "place": null,
    "contributors": null,
    "retweet_count": 3,
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
    },
    "favorited": false,
    "retweeted": false,
    "possibly_sensitive": false
},


 // this is a Retweet response
 // it looks exactly like a normal tweet, except that it has the property `retweeted_status`
 // which is the original content that was retweeted
 //
 // https://dev.twitter.com/docs/api/1/get/statuses/show/%3Aid
 {
    // data added by Mass Relevance
    // mostly useless or for backwards compatibility
    "chained_stream_id": null,
    "adhoc_for_stream_id": null,
    "requeued": null,
    "entity_id": "192338599570702340", // == id_str
    "order_id": "192338599570702340",  // == id_str
    "score": "192338599570702340",     // == id_str

    "created_at": "Tue Apr 17 19:47:50 +0000 2012",
    "id": 192338599570702340,
    "id_str": "192338599570702336",
    "text": "RT @brainpicker: \"A fair and balanced guide to choosing between New York and San Francisco\" from @TheMorningNews http://t.co/KXaGg318",
    "source": "web",
    "truncated": false,
    "in_reply_to_status_id": null,
    "in_reply_to_status_id_str": null,
    "in_reply_to_user_id": null,
    "in_reply_to_user_id_str": null,
    "in_reply_to_screen_name": null,
    "user": {
        "id": 8435702,
        "id_str": "8435702",
        "name": "Craig Richards",
        "screen_name": "donkeyattack",
        "location": "",
        "description": "I am the lineman for the county and I work at Twitter",
        "url": null,
        "protected": false,
        "followers_count": 1679,
        "friends_count": 1011,
        "listed_count": 47,
        "created_at": "Sun Aug 26 04:22:08 +0000 2007",
        "favourites_count": 384,
        "utc_offset": -18000,
        "time_zone": "Eastern Time (US & Canada)",
        "geo_enabled": false,
        "verified": false,
        "statuses_count": 1893,
        "lang": "en",
        "contributors_enabled": true,
        "is_translator": false,
        "profile_background_color": "E7C490",
        "profile_background_image_url": "http://a0.twimg.com/profile_background_images/379104346/Twitter_1544x2000.png",
        "profile_background_image_url_https": "https://si0.twimg.com/profile_background_images/379104346/Twitter_1544x2000.png",
        "profile_background_tile": true,
        "profile_image_url": "http://a0.twimg.com/profile_images/1680486414/craig3_bigger_normal.png",
        "profile_image_url_https": "https://si0.twimg.com/profile_images/1680486414/craig3_bigger_normal.png",
        "profile_banner_url": "https://si0.twimg.com/brand_banners/donkeyattack/1327518376/live",
        "profile_link_color": "FF0000",
        "profile_sidebar_border_color": "E7C490",
        "profile_sidebar_fill_color": "12E39D",
        "profile_text_color": "FF03FF",
        "profile_use_background_image": true,
        "show_all_inline_media": true,
        "default_profile": false,
        "default_profile_image": false,
        "following": null,
        "follow_request_sent": null,
        "notifications": null
    },
    "geo": null,
    "coordinates": null,
    "place": null,
    "contributors": null,

    // this is the original tweet that was retweeted
    // this content is the same as a normal tweet
    "retweeted_status": {
        "created_at": "Tue Apr 17 14:01:32 +0000 2012",
        "id": 192251451500789760,
        "id_str": "192251451500789760",
        "text": "\"A fair and balanced guide to choosing between New York and San Francisco\" from @TheMorningNews http://t.co/KXaGg318",
        "source": "<a href=\"http://bufferapp.com\" rel=\"nofollow\">Buffer</a>",
        "truncated": false,
        "in_reply_to_status_id": null,
        "in_reply_to_status_id_str": null,
        "in_reply_to_user_id": null,
        "in_reply_to_user_id_str": null,
        "in_reply_to_screen_name": null,
        "user": {
            "id": 9207632,
            "id_str": "9207632",
            "name": "Maria Popova",
            "screen_name": "brainpicker",
            "location": "Brooklyn, NY",
            "description": "Interestingness hunter-gatherer obsessed with combinatorial creativity. Editor of @brainpickings & @explorer. Bylines for @WiredUK & @TheAtlantic. MIT Fellow.",
            "url": "http://brainpickings.org",
            "protected": false,
            "followers_count": 178020,
            "friends_count": 307,
            "listed_count": 10405,
            "created_at": "Tue Oct 02 14:18:16 +0000 2007",
            "favourites_count": 12,
            "utc_offset": -18000,
            "time_zone": "Eastern Time (US & Canada)",
            "geo_enabled": true,
            "verified": false,
            "statuses_count": 50866,
            "lang": "en",
            "contributors_enabled": false,
            "is_translator": false,
            "profile_background_color": "FFDB00",
            "profile_background_image_url": "http://a0.twimg.com/profile_background_images/3864643/bg.jpg",
            "profile_background_image_url_https": "https://si0.twimg.com/profile_background_images/3864643/bg.jpg",
            "profile_background_tile": true,
            "profile_image_url": "http://a0.twimg.com/profile_images/125575833/twitter_normal.jpg",
            "profile_image_url_https": "https://si0.twimg.com/profile_images/125575833/twitter_normal.jpg",
            "profile_link_color": "990000",
            "profile_sidebar_border_color": "EBEAE5",
            "profile_sidebar_fill_color": "EBEAE5",
            "profile_text_color": "3F3F3F",
            "profile_use_background_image": true,
            "show_all_inline_media": true,
            "default_profile": false,
            "default_profile_image": false,
            "following": null,
            "follow_request_sent": null,
            "notifications": null
        },
        "geo": null,
        "coordinates": null,
        "place": null,
        "contributors": null,
        "retweet_count": 19,
        "entities": {
            "hashtags": [],
            "urls": [{
                "url": "http://t.co/KXaGg318",
                "expanded_url": "http://j.mp/HUBAOn",
                "display_url": "j.mp/HUBAOn",
                "indices": [
                96, 116]
            }],
            "user_mentions": [{
                "screen_name": "TheMorningNews",
                "name": "The Morning News",
                "id": 16539190,
                "id_str": "16539190",
                "indices": [
                80, 95]
            }]
        },
        "favorited": false,
        "retweeted": false,
        "possibly_sensitive": false
    },
    "retweet_count": 19,
    "entities": {
        "hashtags": [],
        "urls": [{
            "url": "http://t.co/KXaGg318",
            "expanded_url": "http://j.mp/HUBAOn",
            "display_url": "j.mp/HUBAOn",
            "indices": [
            113, 133]
        }],
        "user_mentions": [{
            "screen_name": "brainpicker",
            "name": "Maria Popova",
            "id": 9207632,
            "id_str": "9207632",
            "indices": [
            3, 15]
        }, {
            "screen_name": "TheMorningNews",
            "name": "The Morning News",
            "id": 16539190,
            "id_str": "16539190",
            "indices": [
            97, 112]
        }]
    },
    "favorited": false,
    "retweeted": false,
    "possibly_sensitive": false
}]
```

### Geo Hint Object

Example of a geo hinted object added on a Twitter status entity

```json
{
    "geo_hint": {
        "country": "US",
        "state": "CA",
        "coordinates": [
          34.0522342, - 118.2436849]
    }
}
```

<sup>1</sup>Our docs only cover the `json` API, but the `xml` endpoint supports the same query parameters as the `json` endpoint and a similar response to the `json` endpoint.

<sup>2</sup>Exclusively for television broadcast. You must not publicly display data from these feeds without consent from Mass Relevance.

<sup>3</sup>Exclusively for television broadcast. You must not use this functionality without consent from Mass Relevance.
