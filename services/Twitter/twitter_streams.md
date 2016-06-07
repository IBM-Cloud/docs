{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Decahose and PowerTrack streams {: #decahose_powertrack}

*Last updated: 13 May 2016*

{{site.data.keyword.twittershort}} provides access to Twitter Decahose and PowerTrack streams, based on {{site.data.keyword.Bluemix_notm}} plan enrollment. 
Both streams deliver real-time feeds and different characteristics to suit your needs.
{:shortdesc}

The Decahose stream is a 10% random sampling of the Twitter Firehose. Tweets are derived from Twitter in real-time and the stream is determined by Twitter's sampling algorithms. For most statistical analytics, a 10% random sample is sufficiently accurate. Decahose data is indexed for a 2-year period, so query responses might not return Tweets that are older than 2 years. Access to the Decahose is available in the Free Plan and Entry Plan, while access to the PowerTrack stream is exclusive to Entry Plan users.

The PowerTrack stream offers the added benefit of filtering incoming Tweets, based on a user-defined rules-based filter known as a track. As an Entry Plan user, you can create up to 1,000 rules per account. For advanced filtering, multiple tracks can be combined to form an aggregated track. The following sections describe track states, properties, and supported actions you can perform on tracks, such as editing, deleting, and more.

**Note**: Indexing of the PowerTrack stream is limited to 1 million Tweets per calendar month. Once the limited is reached, indexing stops for the month. At the start of the next month, you can reactivate your tracks; they are not activated automatically. To maximize usage of the stream, proper management of your tracks is highly recommended. For example, redundant tracks can be made inactive.

## Track types {: #track_types}

Entry Plan users can create customizable tracks to filter messages collected in the PowerTrack data stream.  {{site.data.keyword.twittershort}} supports the following two track types.

<dl>
<dt>Rule</dt>
<dd>All the messages collected in this track match at least one of the rules associated with the track. You can add, edit, and delete rules within this track type.

The complete [GNIP PowerTrack Rules syntax](http://support.gnip.com/apis/powertrack/rules.html) is supported within rule-based tracks. All queries must conform to the {{site.data.keyword.twittershort}} [Query language](twitter_rest_apis.html#querylanguage "Query language").
</dd>

<dt>Aggregated</dt>
<dd>A combination of two or more rule or aggregated tracks. Aggregated tracks are used for arbitrary grouping of multiple tracks. You can add and delete individual tracks from an aggregated track type. Individual rules cannot be added to aggregated tracks; use a rule track instead for this purpose. Aggregated tracks are stateless, but their constituent rule tracks are either **Active** or **Inactive**.</dd>
</dl>

## Track properties {: #track_properties}
Tracks contain the following properties. Some properties do not apply to both rule-based and aggregated tracks. For example, the rules property does not apply to aggregated tracks.

<dl>
<dt>createdDate</dt>
<dd>Indicates when the track was created; specified as `YYYYMMDDHHMM`.</dd>

<dt>endDate</dt>
<dd>Indicates when the track stops collecting messages. The specified value must be in the future and follow one of the following formats: `YYYY-MM-DD` or `YYYY-MM-DDTHH:MM:SSZ`. Specifying a date in the past returns an HTTP 400 error.

This property does not apply to aggregated tracks.</dd>

<dt>id</dt>
<dd>A unique ID reference that is assigned to a track upon creation. The ID is represented in a GUID string format (for example, 3F2504E0-4F89-41D3-9A0C-0305E82C3301) for rule and aggregated tracks.</dd>

<dt>name</dt>
<dd>Descriptive name of the track. Uniqueness of this property is not guaranteed.</dd>

<dt>rules</dt>
<dd>An array of rules, including query keywords and other parameters that define the track filters. This property applies to rule-based tracks, but does not apply to aggregated tracks.</dd>

<dt>state</dt>
<dd>Must be either **Active** or **Inactive**. An active track collects messages, while an inactive track does not. You can change the state of a track at any time.

This property does not apply to aggregated tracks.</dd>

<dt>trackIds</dt>
<dd>An array of track IDs. This property applies to aggregated tracks only.</dd>

<dt>type</dt>
<dd>Indicates whether the track type is **Rule** or **Aggregated**.

For more information on track properties, including track operations and model schema, refer to the {{site.data.keyword.twittershort}} REST API documentation.</dd>
</dl>

