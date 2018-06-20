# RRS (RSS Reader Spec or Remote RSS Subscription)

Subscribing to webfeeds today (as of May 2018) typically involves copying and pasting a URL into a prompt dialog. Needless to say this is not very user friendly, and it is to the benefit of those apps to recieve web feeds from other apps.

It is possible for them to do so today by indicating via the [Desktop Entry Spec](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-1.1.html) they can open `application/rss+xml` or `application/atom+xml` files (thereby implying they can also handle HTTP[S] links). But this doesn't allow those feed readers to specialize amongst the feeds the can handle, and it doesn't allow webfeed aware apps to indicate your subscription status or unsubscribe you. So as this is a strong fallback standard, it is ideal to define an enhancement.

## Basics
RRS extends .desktop files with extra keys specific to the field of feedreaders. Compatible .desktop files MUST declare within their `MimeType` entry that it supports  `application/rss+xml` and/or `application/atom+xml`, and the `Exec` entry must use the `%u` or `%U` field codes over `%f` and `%F`. By doing so the app implies it can handle HTTP URIs that delivers these `Content-Type`s.

## Subscribing to feeds
The semantics of opening a webfeed in a feedreader MUST have the effect of subscribing to that feed. That is the `Exec` entry is what should be used for subscribing to a feed.

If you're already subscribed, this should have no effect.

## Extra .desktop Keys
Keys are either OPTIONAL or REQUIRED. If a key is OPTIONAL it may or may not be present in the file. However, if it isn't, the implementation of the standard should not blow up, it must provide some sane defaults.

<table>
<tr><th>Key</th><th>Description</th><th>Value Type</th><th>Required?</th></tr>
<tr>
  <th>RRS</th>
  <td>If set to NO indicates that it should not be listed amongst RRS compatible apps. Otherwise it indicates the version of this standard it supports. For this version use `0.1`</td>
  <td>string</td><td>NO</td>
</tr>
<tr>
  <th>RRS-Status</th>
  <td><p>Specifies a command to run in order to check if the app is currently subscribed to that feed. The exit status should be 0 if it is, non-zero if not. This command MUST neither open nor close the app, and should incur minimal performance overhead.</p>
  
  <p>If this is not specified feed providing apps cannot indicate whether you are already subscribed to the feed, and will likely assume not.</p></td>
  <td>string</td><td>NO</td>
</tr>
<tr>
  <th>RRS-Unsubscribe</th>
  <td>Specifies a command to run in order to unsubscribe from an RSS feed within the app. The app SHOULD open a dialog asking if this is desired in order to ensure apps aren't unsubscribing to feeds without the user being aware of it.</td>
  <td>string</td><td>NO</td>
</tr>
<tr>
  <th>RRS-Enclosure</th>
  <td>Specifies MIME types that should be linked to by the webfeed, using the RSS `enclosure` element or the ATOM `content` element.</td>
  <td>string(s)</td><td>NO</td>
</tr>
<tr>
  <th>RRS-HTML</th>
  <td>Specifies an XPath expression that should consistantly be present in the description elements in order for this application to be offered as a feedreader for a given feed.</td>
  <td>string(s)</td>
</tr>
</table>

The `Status`, & `Unsubscribe` keys MUST be formatted similarly to `.desktop` files' `Exec` key, except the only supported field codes are `%u` & `%U`. These have the same meaning.
