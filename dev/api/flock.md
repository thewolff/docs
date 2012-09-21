# Flock to Unlock API

## Resource URL

http://tweetriver.com/flock/:account/:flock_name.:format

account: the flock owner's account name (e.g. `howardr`)<br />
flock_name: the name of the flock (e.g. `video-promotion`)<br />
format: `json`

**Example URL:** http://tweetriver.com/flock/howardr/example-flock.json

## Response

Reponse is a JSON object. If an error occurs then the response will be empty (whitespace).

### Example Request

    $ curl http://tweetriver.com/flock/howardr/example-flock.json

```json
{
    "thresholds": [{
        "payload": {
            "custom": "payload",
            "items": [0, 1, 2, 3]
        },
        "name": "",
        "pct": 100,
        "description": ""
    }],
    "kind": "flock-to-unlock",
    "full_name": "howardr/example-flock",
    "name": "example-flock",
    "description": ""
}
```

### Properties

#### Thresholds

The `thresholds` array within the response is where the the unlocked information is contained. A flock to unlock endpoint may have more than one unlock threshold. We use this when there is more than one payoff.

The items of the threshold are ordered. The order can be specified. We usually order thresholds such that thresholds that unlock first are earlier in the array. The order is preserved with each request.

The two important `threshold` properties are `payload` and `pct`

#### Payload

A `payload` can be specified with any data that can be serialized to JSON. **If the threshold condition has not been met, then the payload will NOT BE included**. When the threshold condition has been met then `pct` === 100

#### Pct

`pct` is an integer value where 0 >= `pct` <= 100. When `pct` === 100, then the threshold condition has been met and there will be a `payload` included in the threshold (if one has been defined).

Each `threshold`'s `pct` is independent* of all other thresholds within the array. e.g. if there are 10 thresholds, each one will calculate its own `pct` depending on its unlock condition. The only time when all thresholds are `pct` are 0 is when there are 0 tweets. This should not be an issue but it is worth noting.

_*= `pct` acts a little bit differently if the flock endpoint is artificial. i.e. the thresholds unlock at some predetermined time instead of organically through number of tweets. In this case each condition is dependent on the when the previous threshold unlocks._

#### Other properties

A `name` and a `description` can be defined per threshold. We usually do not use these fields.

## Annotated JSON Response

If there is 10k tweets there will be a video displayed, but there will be a new photo for each 1k of tweets tweeted up to that point. In this case, there would be 10 threshold items in the `thresholds` array.

```js
{
  //...
  "thresholds": [
  
    // picture 1:
    // unlocked. `payload` is given
    {
      "payload": {
        "thing": "that is awesome"
      },
      "pct": 100,
      "name": "",
      "description": ""
    }
    
    // picture 2:
    // not yet unlocked so `payload` is null
    {
      "pct": 62
      // + custom threshold name and description
    }
    
    //...7 other similar thresholds
    
    // final unlock (video):
    // not yet unlocked so `payload` is null
    {
      "pct": 12
      // + custom threshold name and description
    }
    
  ]
}
```    