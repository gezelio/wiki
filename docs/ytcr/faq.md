---
title: FAQ - YouTube Channel Rewards
description: A greater understanding of YTCR
---

# FAQ and known limitations
Our system won't work for every streamer and every community, so to help you decide if this is right for you, we've compiled this list of known limitations to help you understand.

It's important to note that these limitations may change over time, and we'll announce such changes on our [Twitter](https://twitter.com/gezel_io) and [Discord](https://gezel.io/discord), so ensure you're there to get updates!

---

# General Stuff

## Streamerbot Reliance
YTCR is built directly with Streamerbot in mind. It ties in and is only officially supported through the use of SB. This means that if you use something like MixItUp, SAMMI or equivelant, this most likely won't work. There may be ways to work around this and a way to link these together, but for the best out of our tool, we recommend using Streamerbot.

> This isn't a 'problem' but by design. We plan on sticking with SB for all of our development, and have no planning on adding this to platforms other than Streamerbot.
---
## Mobile Users
If most of your community watch your streams via the YouTube app etc, this won't offer much to those viewers that this time. YTCR is built with a Chrome Extension, and currently has 0 chat functionality. For your community to use YTCR, they must have Chrome (or a [Chromium based browser](https://www.zdnet.com/pictures/all-the-chromium-based-browsers/))
> This is something we plan on implementing down the road, however YouTube are quite strict with their "quota" and we'll see some serious problems if this isn't upgraded first.
---
## Discord Auth
Going back to the whole "***YouTube = strict business***", we've decided to verify the ownership of your channel via signing in to the site via Discord. This allows us to pull your connected YouTube channels, and verify the ownership through those means.
This can cause some problems should you want to add/change what channels are connected, so if you face any of these problems, please contact us via [Discord](https://gezel.io/discord).
> There is no easy work around for this problem, as we're a small team. If Google/YouTube is your thing and you want to help with the 'official' side of Google things, please also let us know!
---
## How Rewards Work
At time of writing, you must also have a Twitch account linked to your StreamerBot, and it must be a 'affiliate' account. This is due to the fact that YTCR will pull your Twitch rewards from SB (and only ones built inside SB) which will then be pushed over the websocket.
>We spoke quite publicly with Nate from Streamerbot on ways we could avoid this, which could lead to a direct integration from within SB, however this is long down the road.
**For now, you must have an affiliated Twitch channel linked also.**
---
## Updating Rewards
There can be a delay in the websocket in pulling your latest rewards to your stream, if you're connected to the socket while creating these. If the extension isn't updating with your latest rewards, head over to:
- Servers/Clients
	- Websocket Clients
		- Right-click > "Disconnect"
		- Right-click > "Connect"

This should check for your latest changes, and push them directly.
>If that gives you any problems, it's also a good idea to refresh your YouTube page.