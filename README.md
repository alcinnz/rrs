# RRS
Remote RSS Subscription (EARLY DRAFT protocol)

Feed readers commonly have really poor feed subscription UIs, so in the spirit of https://freedesktop.org/ this repository proposes a standard by which an application that's aware of the presence of a webfeed (which would typically be a web browser) can communicate with another application to subscribe and unsubscribe from that webfeed.

The hope is that having this bridge interface between web browsers and feed readers will help encourage the uptake of RSS/Atom via better user interfaces.

## Use Cases

1. An application is aware of a webfeed and wishes to present a menu of apps with which to subscribe/unsubscribe from it with. It also wishes to know whether the feed is subscribed to in each app so it can indicate whether the button for that app will subscribe or unsubscribe.
2. A feed reader wishes to be added to the menus describe in (1) so that it's users don't have to go through it's prompt dialog to add a new feed.
3. A video streaming app also wishes to be added to those menus, but only for video podcasts. A podcast app wants something similar.

## Design

The crucial constraint of this potential standard is that it needs to let apps enumerate compatible apps, whether or not they're currently running. This rules out DBus which can only enumerate apps compatible with a standard if they're running at the moment. As such this draft is based strongly on the [Desktop File Spec](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-1.1.html), and will build upon it.
