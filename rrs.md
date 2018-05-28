Subscribing to webfeeds today (as of May 2018) typically involves copying and pasting a URL into a prompt dialog. Needless to say this is not very user friendly, and it is to the benefit of those apps to recieve web feeds from other apps.

It is possible for them to do so today by indicating via the [Desktop Entry Spec](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-1.1.html) they can open `application/rss+xml` or `application/atom+xml` files (thereby implying they can also handle HTTP[S] links). But this doesn't allow those feed readers to specialize amongst the feeds the can handle, and it doesn't allow webfeed aware apps to indicate your subscription status or unsubscribe you. So as this is a strong fallback standard, it is ideal to define an enhancement.

## File naming
RRS files MUST share the same name as their corresponding `.desktop` file, except with a `.rrs` extension instead of a `.desktop` extension. They MUST be stored in one of `$XDG_DATA_DIRS` directly under the `webfeedreaders` subdirectory.

## Basic Format of the File
RRS files share the same basic format as `.desktop` files.

## Recognized RRS Keys
Keys are either OPTIONAL or REQUIRED. If a key is OPTIONAL it may or may not be present in the file. However, if it isn't, the implementation of the standard should not blow up, it must provide some sane defaults.

<table>
<tr><th>Key</th><th>Description</th><th>Value Type</th><th>Required?</th></tr>
<tr>
  <th>Subscribe</th>
  <td>Specifies the command to run in order to subscribe to an RSS feed with that app.</td>
  <td>string</td><td>YES</td>
</tr>
<tr>
  <th>Status</th>
  <td>Specifies a command to run in order to check if the app is currently subscribed to that feed. The exit status should be 0 if it is, non-zero if not.</td>
  <td>string</td><td>YES</td>
</tr>
<tr>
  <th>Unsubscribe</th>
  <td>Specifies a command to run in order to unsubscribe from an RSS feed within the app. The app SHOULD open a dialog asking if this is desired in order to ensure apps aren't unsubscribing to feeds without the user being aware of it.</td>
  <td>string</td><td>NO</td>
</tr>
<tr>
  <th>Enclosure</th>
  <td>Specifies MIME types that should be linked to by the webfeed, using the RSS `enclosure` element or the ATOM `content` element.</td>
  <td>string(s)</td><td>NO</td>
</tr>
</table>

The `Subscribe`, `Status`, & `Unsubscribe` keys MUST be formatted similarly to `.desktop` files' `Exec` key, except the only supported field codes are `%u` & `%U`. These have the same meaning.
