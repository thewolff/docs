# Mass Relevance Platform API: An Overview

The Mass Relevance platform is an enterprise social curation platform for building and using **streams**. A stream is a focused, meaningful collection of social content that is aggregated in real time across multiple sources (Twitter, Facebook, Instagram, more), and filtered according to rules you specify.

![Mass Relevance Platform Overview](/MassRelevance/docs/blob/master/dev/img/platform-overview.png "Mass Relevance Platform Marketecture")

Each **entity** (a social social content item like a Tweet, Facebook post or comment, Instagram photo, etc.) flows into a stream and is, by default, held for moderation. Any entities you approve (either automatically via rules or manually via manual moderation) are immediately visible/usable via our [Stream API](/MassRelevance/docs/blob/master/dev/api/stream.md).

As entities flow into a stream, the Mass Relevance platform captures meta information about the content in this stream. This meta information is available via the [Stream Meta API](/MassRelevance/docs/blob/master/dev/api/meta.md) and includes details like stream volume (total number of approved, pending, and rejected entities) and stream activity rate (TPM, or Things Per Minute).

The [Compare API](/MassRelevance/docs/blob/master/dev/api/compare.md) is intended to programmatically surface a volume comparison, in percentages, between multiple streams. This is commonly used in social polls (like Hashtag Battles) to identify, in realtime, the volume of one topic vs others.


