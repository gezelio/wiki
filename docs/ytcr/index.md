---
title: YouTube Channel Rewards Tutorial - Powered by Gezel.io
description: How to set up YTCR for YouTube Channel Rewards on your Streamerbot application
---

# YouTube Channel Rewards
Bring the features you love from Twitch to your `YouTube` livestreams!\
A missing feature on YouTube streams is user input, and this is how we fixed that. Our YTCR ties directly to your StreamerBot application, so whatever you can imagine you can do, it’s possible now on YouTube. Unlike Twitch, with YTCR you have the ability to give (and take) channel points away from specific users, which gives you even more control behind your channel!
The only thing your viewers have to do is download the Chrome Extension

---
## Video Guide
<iframe
    width="640"
    height="360"
    src="https://www.youtube.com/embed/AVUB1xe1_po"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>

---

## Prerequisites
- [**Streamerbot**](https://streamer.bot)
	- Must be version `v0.1.8` or newer.
- Affiliated [Twitch](https://twitch.tv) account
	- This is due to how you'll implement channel rewards on Streamerbot.

---
# Streamerbot Settings
### Download & Import 
<ul class="links-list">
<li><a rel="noreferrer" target="_blank" class="" href="https://github.com/gezelio/YTCR-Streamerbot/releases/tag/v0.1.2">Click me to download YTCR v0.1.2 here</em></a> | You want the "ytcr_v.0.1.2.gezel" file</li>
</ul>

Import the file
1. Launch Streamer.bot
2. Select 'Import' from the top right panel
3. Drag the file you downloaded from our GitHub into the empty `import string` box.

You should now have three new `Actions` inside your Streamerbot:

- Clipping Tool
- Execute Channel Reward Rededem
- Set Channel Rewards

Click the `Set Channel Rewards` action and you should see two Sub-Actions. Double click `Set global "youtube_channel_id"`\
Where it says `CHANGEME` beside `value`, update this to your YouTube channel ID. You can get that [here](https://www.youtube.com/account_advanced) if you aren't aware of it.

### Clipping Tool
The Clipping Tool is a new feature from `v0.1.2` that adds a clipping feature to your stream. This utilizes the OBS `Replay Buffer` feature and would require additional setup. 
We made this because YouTube's clipping feature doesn't actually create a downloadable clip to post on other social media platforms, so we hope this will be a good alternative to Twitch's clip feature.
>**If you don't plan on using Clipping Tool, feel free to move to the [next section](#WebSocket).**
### How does it work?
It only allows one clip every minute. It does this by renaming the files by 'year-month-day_hour-minute' while also thanking the user who created the clip.
- Example of a clip name: `"2022-06-24_16-04 (clipped by trent1605)"`
## OBS Settings
- `Output` > `Replay Buffer` and select `Enable Replay Buffer`
	- You can also change the length of your clips here. We recommend 30/60 seconds.
- Head into `settings`
	- Under `General`, tick the box for `Automatically start replay buffer when streaming`\
*This will help you ensure it's always running when streaming.*
- Inside the `Recording` tab, these are also your settings for the `Replay Buffer`
	- Take note of the recording path and format, we'll need these for StreamerBot. 
## Streamerbot Settings
- Select the `Clipping Tool` Action and update the following;
	- Set global "yourReplayPath"
  		- This is where your `recording path` was from OBS.
  - Set global "yourOutputPath"
  		- This is where you want the new files to go to.
  - Set global "yourFileFormat"
  		- This is what format you are using, such as mp4/mkv/etc
>It's important to note that the paths are written in `C#` and may not appear as you'd expect. For example, my Replay Path on Windows is `D:\rec` but in `C#` it's `D:\\rec\\`.
> I haven't found a good converter for those who aren't aware, so if you get super stuck on this, please feel free to jump into our [Discord](https://gezel.io/discord) and either us or someone from the community I'm sure will be able to help!

This is a fork of [HYP3RSTRIKE](https://youtube.com/hyp3rstrike)'s [Advanced OBS Clipper](https://github.com/hyp3rstrike/StreamerBot_CSharp/blob/main/AdvancedOBSClipper.cs) to function with YTCR as a separate icon within the extension. Credits go to him for giving us this idea, so I'd recommend dropping him a [sub](https://youtube.com/hyp3rstrike) to say thank you!

---
# Websocket Connection
Inside Streamerbot, head over to:
- Servers/Clients
    - Websocket Clients

Right click and select ‘Add’ and insert the following:

|SECTION | INPUT|
|-----------------------------------|-----------------------------------|
|               Name            |           Gezel's YTCR        |
|             Endpoint            |      ws://144.172.67.101:82/ws   |
|     Auto Connect on Startup    |✅|
|     Reconnect on Disconnect     |✅|
| TLS (tick the following boxes)  |TLS 1.0|
| Retry Interval | 5 seconds |

| Actions | |
|-----------------------------------|-----------------------------------|
|            Connected           |      Set Channel Rewards      |
|           Disconnected          |               NONE             |
|             Message           | Execute Channel Reward Redeem |

*screenshot for guidance*\
![](https://i.imgur.com/Y5u6N4l.png)\
**Once you've completed this, right-click and choose `connect`!**

>**Tip:** Anytime you add/remove/modify channel rewards while connected to the WebSocket, you must go into `Servers/Clients` > `Websocket Clients` and right-click `disconnect` and then `reconnect` to pull the changes. It only pulls the reward data on load at this present time.

---
# YTCR Dashboard
We'll go back over actually adding channel rewards once we get you connected on the site, as this completes the websocket connection and confirms you own the `Channel ID` you entered before.
1.  Navigate to [https://ytcr.gezel.io](https://ytcr.gezel.io)
2.  Create an account
3.  Authenticate with Discord
4.  Set the time and amount of points you'd like your viewers to earn each interval

>**Tip:** You can actually add a custom dock on your OBS to see how many points each user has! If you click `View Profile` on the YTCR site, you can see your username in the URL bar like this:
`ytcr.gezel.io/u/USERNAME`.\
Add the following URL (and update your username) to a `custom dock` inside `OBS > Docks > Custom Browser Docks` to see this from there;
` https://ytcr.gezel.io/obs/USERNAME?darkmode=true&refresh=true`

---
# Setting up channel points
It's likely you've set up channel points with StreamerBot before for your Twitch, but if you haven't, you can watch IRLCreates video [here](https://www.youtube.com/watch?v=nlNkGBWA1A0). This should give you an idea on how to get started.
The channel points used will be the ones under the “Twitch category” on StreamerBot.

## **There are some important things to know what we will pull into the YouTube Channel Points that you should pay attention to**

### Group
**The channel rewards you want on YouTube should be under a group called `YTCR`**
-   You can add rewards to a group by double clicking on one, and under ‘group’ type `YTCR`
    -   Any other channel points you want to add to the group can be done by right clicking and under group select `YTCR`
    
### The 'Enabled' status
**Any channel rewards with the ‘enabled’ setting set to ‘no’ will automatically be not pulled to the extension**
- This is to allow you to quickly enable/disable points that may not be working on your side, or are not fully complete.

### User Input Required
**Any reward that requires a user input will also automatically not be added to the extension, as this is a Twitch feature that currently cannot be replicated with our extension.**

> The cost of a channel point inside StreamerBot will also be the cost of the action inside YouTube. Users generate points every 5 minutes, so be sure you set these fair with how many points you offer every 5 minutes from the [Dashboard](https://ytcr.gezel.io).

---
# Install the Browser extension
It's important you and your viewers install the Chrome extension, as that's what will bring the buttons to you and your community. 
>As this is an extension, it's important to know that this will only work on Chrome or other Chromium based browsers (pretty much anything that's not Safari or Firefox) and will also not work on the YouTube app, nor in YouTube Studio view at this time.

The best way to ensure your community have the extension is to let them know it can be downloaded from `https://gezel.io/download` which will redirect them to the Chrome Extensions Store.