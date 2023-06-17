# Twitch-OBS-Bridge

<p align="center"><i>
Twitch-OBS-Bridge enables a pseudo code approach to manage and automatically handle Twitch Channel Points, Twitch Chat, OBS or SLOBS, and StreamElements or Streamlabs alerts.
</i></p>
<p align="center"><b>
  <a href="https://youtu.be/YaXLsWQuhLE">Tutorial</a> |
  <a href="https://github.com/Sneaky-amxx/TwitchOBS-Bridge/releases/download/Release/TwitchOBS-Bridge.rar">Download</a> |
  <a href="https://github.com/Sneaky-amxx/TwitchOBS-Bridge/blob/main/js/Documentation.md">Documentation</a> |
  <a href="https://github.com/Sneaky-amxx/TwitchOBS-Bridge/blob/main/settings/Settings.md">Settings</a>
</b></p>

***

## Table of Contents

- [FGC Trigger Scripts *Read After Finishing Setup Guide](#fgc-trigger-scripts)
- [Setup Guide](#setup-guide)
- [Compatibility](#compatibility)
- [Installation](#installation)
  + [OBS Websocket](#obs-websocket)
  + [Settings](#settings)
  + [Add as Browser Source](#add-as-browser-source)
- [Usage](#usage)
  + [Pseudo Code Format](#pseudo-code-format)
  + [triggers.txt](#triggerstxt)
  + [fileTriggers.txt and the triggers folder](#filetriggerstxt-and-the-triggers-folder)
  + [sounds folder](#sounds-folder)

***

## Setup Guide

- (If using OBS) Install the [OBS Websocket Plugin](https://github.com/Palakis/obs-websocket/releases/latest) (version 5.0.0 or above). Reopen OBS after installing.
- Fill out [the settings files](https://github.com/Sneaky-amxx/TwitchOBS-Bridge/blob/main/settings/Settings.md) in the settings folder.
- Add the **index.html** to OBS/SLOBS as a browser source.
- Type `!example` in your twitch chat. If your user responds with `Success! It worked!`, you're good to go!
- Customize the _triggers.txt_ with your own triggers from the [the documentation](https://github.com/Sneaky-amxx/TwitchOBS-Bridge/blob/main/js/Documentation.md).

***

## FGC Trigger Scripts

### triggers.txt
```
OnCommand b 0 !p1name
OBS Source p1name Text {after}
Chat Send "Player 1 Name Changed!"

OnCommand b 0 !p2name
OBS Source p2name Text {after}
Chat Send "Player 2 Name Changed!"

OnCommand b 0 !roundformat
OBS Source RoundFormat Text {after}
Chat Send "Round Format Changed"
```

## Compatibility

Twitch-OBS-Bridge supports
- Twitch Channel Points
- Twitch Chat
- Twitch Hype Trains
- Streamlabs Alerts
- StreamElements Alerts
- OBS scene, source, and filter changes
- SLOBS scene and source changes
- Playing music (mp3, wav, ogg)
- Timers (triggering on an interval)
- Sending API calls

and more in [the documentation](https://github.com/Sneaky-amxx/TwitchOBS-Bridge/blob/main/js/Documentation.md)!

The script should run on any broadcast software that supports browser sources, however only OBS and SLOBS support changing scenes and sources.

OBS.Live should also be supported but is untested.

***

## Installation

### OBS Websocket (if using OBS)
To use this script with OBS, install the [obs-websocket](https://github.com/Palakis/obs-websocket/releases/latest) plugin (version 5.0.0 or above). Reopen OBS after installing.

In OBS, click **Tools** > **WebSockets Server Settings** and enable the websocket server.

It is **highly recommended** to use a password!

### Settings
Before the script will work, you'll need to fill out all of the settings files. Please see the [settings description](https://github.com/Sneaky-amxx/TwitchOBS-Bridge/blob/main/settings/Settings.md) for more information.

### Add as Browser Source
Add the **index.html** file as a browser source within your broadcast software. It is *recommended* to add this source to one scene that is included in all other scenes (like your alert scene) rather than recreate this source in every scene.

#### Steps for adding to OBS/SLOBS
- In OBS, under **Sources** click the + icon to add a new **Browser** source.
- Name it and select OK.
- Check the `Local file` checkbox.
- Click **Browse** and open the **index.html** file within the Twitch-OBS-Bridge script directory.
- Recommended to set the width/height to 100 or less to reduce the size of the source.

***

## Usage

### Pseudo Code Format
For information on the pseudo code format, please see [the documentation](https://github.com/Sneaky-amxx/TwitchOBS-Bridge/blob/main/js/Documentation.md).

### triggers.txt
Setup your triggers inside of this file if you do not need actions to be run one after another.

As an example, if the below is in the _triggers.txt_ file, then both sounds can be played at the same time.

#### triggers.txt
```
OnChannelPoint SHIKAKA
Play 30 wait Shikaka.mp3

OnCommand sbvm 0 !intervention
Play 45 nowait MashiahMusic__Kygo-Style-Melody.wav
```

### fileTriggers.txt and the triggers folder
When you need actions to be run one-after-another, create a file in the _triggers_ folder and add the name of the folder to _fileTriggers.txt_.

As an example, here's a setup to make sure multiple scene changes don't happen simultaneously.

#### _fileTriggers.txt_
```
obs.txt
```
#### _triggers/obs.txt_
```m
OnSLDonation
OBS Scene DonationCelebration
Delay 4

OnCommand mb 0 !brb
OBS Scene BRB
Delay 5
```

### sounds folder
In order to use a sound with [`Play`](https://github.com/Sneaky-amxx/TwitchOBS-Bridge/blob/main/js/Documentation.md#play), add the sound file to the *sounds* folder. The supported audio formats are mp3, wav, and ogg.

***


***

## Support the Project
There are a number of ways to support this project.

- Support Kruiser through <a href="https://patreon.com/kruiser8">Patreon</a>.
- <a href="https://github.com/Kruiser8/Kruiz-Control-Documentation">Translate the documentation</a>.
- Help others in the <a href="https://discord.gg/wU3ZK3Q">Support Discord</a>.
- Contribute ideas for the <a href="https://trello.com/b/oIV3q6Im/kruiz-control">roadmap</a>.
- Spread the word!

I do take commissions to implement custom functionality when necessary. Please reach out if you have a specific request.

***

## Credits
- [Kruiz Control](https://github.com/Kruiser8/Kruiz-Control/tree/master) (Kruiser8 - The main author)
- [async](https://github.com/caolan/async) by Caolan McMahon (caolan)
- [comfyjs](https://github.com/instafluff/ComfyJS) by Instafluff (instafluff)
- [node-shlex](https://github.com/rgov/node-shlex) by Ryan Govostes (rgov)
- [obs-websocket-js](https://github.com/haganbmj/obs-websocket-js) by Brendan Hagan (haganbmj)

## License
<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivs 4.0 Generic License</a>.
