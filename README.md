# Docs

Developer documentation for the Mass Relevance platform.

 * [Overview](/MassRelevance/docs/blob/master/dev/overview.md)
 * [Realtime](/MassRelevance/docs/blob/master/dev/realtime.md)
 * [API](/MassRelevance/docs/blob/master/dev/api/api.md)
   * [Stream](/MassRelevance/docs/blob/master/dev/api/stream.md) **/:account/:stream_name.json**
     * Authenticated actions
     * Sources
         * Twitter
         * Facebook
         * Google+
         * YouTube
         * Instagram
         * Custom Messages
    * [Stream Meta](/MassRelevance/docs/blob/master/dev/api/meta.md) **/:account/:stream_name/meta.json**
      * Basic (.full_name, .name, .description, .created_at)
      * Activity (.activity)
      * Count (.count)
      * Topics (.buckets)
      * Top Tweets (.top, .top_periods)
      * Moments (.moments, .moments_periods)
    * [Account Streams](/MassRelevance/docs/blob/master/dev/api/account.md) **/:account.json**
    * [Flock](/MassRelevance/docs/blob/master/dev/api/flock.md) **/flock/:account/:flock_name.json**
    * [Compare](/MassRelevance/docs/blob/master/dev/api/compare.md) **/compare.json**
 * [Stream Management API](/MassRelevance/docs/blob/master/dev/api/stream_management.md)
 * Using the API
   * [Polling streams](/MassRelevance/docs/blob/master/dev/usage/polling.md)
   * [Displaying stream entities](/MassRelevance/docs/blob/master/dev/usage/display.md)
     * Twitter
     * Facebook
     * Google+
     * YouTube
     * Instagram
     * Custom Messages
   * [Using meta.json](/MassRelevance/docs/blob/master/dev/api/counts.md)
 * Libraries
   * [JavaScript](/MassRelevance/docs/blob/master/dev/clients/javascript.md)
