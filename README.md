# alexa-youtube
## Unofficial YouTube skill for Alexa
__Last update: 27 Dec 2019__


## Sponsorship
* First things first, I am asking for **$3/month** to use this skill. You can test it for free, but it will only ever play Gangnam Style.
* You can donate through https://www.patreon.com/alexayoutube, or by clicking the **Sponsor** button at the top of this page. For just **$3/month**, I will give you a unique ARN which you can use to run this skill.
* Email me at ndg63276@gmail.com to receive your ARN. Let me know what country you are in, and I will make sure the server is close to you, which makes it respond slightly faster.

## Features
* Play audio from YouTube videos
* Play video (if supported) on live videos or if you ask for just one specific video (command 8)
* Makes a list of all the videos played, in the Alexa app

## Launching
* In English, say "Alexa, launch YouTube". 
* In German, say "Alexa, öffne YouTube". 
* In Italian, say "Alexa, avvia YouTube".
* In Spanish, say "Alexa, abrir YouTube".

## Skill Commands

1. Play a video, eg "Alexa, ask YouTube to play Gangnam Style"
2. Play a playlist, eg "Alexa, ask YouTube to play playlist Ultimate Beyonce"
3. Play a channel, eg "Alexa, ask YouTube to play channel Fall Out Boy Vevo"
4. You can replace "play" with "shuffle" to get a randomized version of the search results/channel/playlist, eg "Alexa, ask YouTube to shuffle channel Nicki Minaj"
5. Next / Previous / Start Over / Pause / Resume should all work
6. Ask what is playing by "Alexa, ask YouTube what song is playing" (or just "Alexa, can you repeat that?" should tell you)
7. Skip forward or back in the video by "Alexa, ask YouTube to skip forward/backward to/by one minute and one second"
8. Just play one video by "Alexa, ask YouTube to play one video Gangnam Style". You can switch in and out of "autoplay" mode by "Alexa, ask YouTube to turn on/off autoplay."
9. Find the current time in the video by "Alexa, ask YouTube what is the timestamp?"
10. If you want to play your own playlists, and the search feature finds other people's, send me a link to your youtube page.
11. Play related videos, by "Alexa, ask YouTube to play more like this". This is a YouTube feature, don't ask me why it plays what it plays.

Command 7 doesn't seem to work on Generation 1 Echo's, no idea why.
Commands 8, 9, 10 and 11 are only available in English at the moment. Need them in your language? Drop me an email and we can figure out the translation.

## Known issues

1. Some videos just fail, it's not clear why, they just do. The skill just moves to the next video on the playlist, but this can mean sometimes she announces a video that doesn't play.
2. It appears this skill only works on Amazon Echo products, not on 3rd party products that support Alexa. If you get it to work on another device, please let me know.
3. Live videos work on Gen 2 devices onwards, not on the original Gen 1 Echo.

## Setup Instructions

1. Go to the Alexa Console (https://developer.amazon.com/alexa/console/ask)
2. If you have not registered as an Amazon Developer then you will need to do so. Fill in your details and ensure you answer "NO" for "Do you plan to monetize apps by charging for apps or selling in-app items" and "Do you plan to monetize apps by displaying ads from the Amazon Mobile Ad Network or Mobile Associates?"
3. Once you are logged into your account click "Create Skill" on the right hand side.
4. Give your skill any name, eg "My YouTube Skill".
5. **Important** Set the language to whatever your Echo device is set to. If you are not sure, go to the Alexa app, go to Settings, Device Settings, then click on your Echo device, and look under Language. If your Echo is set to English (UK), then the skill must be English (UK), other types of English will not work!
6. Choose "Custom" as your model, and "Provision Your Own" as your method, then click "Create Skill". On the template page, choose "Start from scratch".
7. On the left hand side, click "JSON Editor".
8. Delete everything in the text box, and copy in the text from https://raw.githubusercontent.com/ndg63276/alexa-youtube/master/InteractionModel_en.json, (or use InteractionModel_fr.json, InteractionModel_it.json, InteractionModel_de.json, InteractionModel_es.json, InteractionModel_ja.json or InteractionModel_pt-br.json for French, Italian, German, Spanish, Japanese or Brazilian Portuguese.)
9. Click "Save Model" at the top.
10. Click "Interfaces" in the menu on the left, and enable "Audio Player" and "Video App". Click "Save Interfaces".
11. Click "Endpoint" in the menu on the left, and select "AWS Lambda ARN". Under "Default Region", put the ARN. You can get an ARN by sponsoring me on https://www.patreon.com/alexayoutube, or by clicking the **Sponsor** button at the top of this page. (If you would like to test the skill before sponsoring me, put arn:aws:lambda:eu-west-1:175548706300:function:YouTubeTest - but this will only play Gangnam Style.)
12. Click "Save Endpoints"
13. Click "Permissions", at the very bottom on the left.
14. Turn on "Lists Read" and "Lists Write".
15. Click "Custom" in the menu on the left.
16. Click "Invocation" in the menu on the left.
17. If you want to call the skill anything other than "youtube", change it here. Click "Save Model" if you change anything.
18. Click "Build Model". This will take a minute, be patient. It should tell you if it succeeded.
19. **Important:** At the top, click "Test". Where it says "Test is disabled for this skill", change the dropdown from "Off" to "Development". 

## Keeping a list of what you have played
This skill can make a list of the last 90 videos played, but you have to give it permissions in the Alexa app:
1. Go to the Alexa app on your phone. In the menu, go to "Skills & Games", then "Your Skills", then scroll to the right and click on "Dev".
2. Click on your YouTube skill. You should see a button marked "Settings", click that. 
3. Then press on "Manage Settings", and tick the boxes marked "Lists Read Access" and "Lists Write Access", and press "Save Settings".
4. Say "Alexa, launch YouTube", that will create the list, and from then on, videos will be added to it.
The list can be viewed in the Alexa app, click Lists from the main menu.

That's it!

## Deploying yourself (optional, advanced)
This skill currently runs on my Lambda instance, hopefully it won't get too popular. If you want to, and know how, you can deploy it on your own Lambda, you just need the lambda_function.zip file, and a YouTube developer key. (See [here](https://www.slickremix.com/docs/get-api-key-for-youtube/)).

[tal9000v2](https://github.com/tal9000v2) has put together a handy guide for deploying yourself [here](https://github.com/ndg63276/alexa-youtube/issues/15#issuecomment-447684487).

If you have a (public) playlists that you would like to play, get your channel ID from youtube. Find a video you have uploaded, then click on your name beneath it, it should take you to eg https://www.youtube.com/channel/UCDVYQ4Zhbm3S2dlz7P1GBDg, in which case your channel ID is UCDVYQ4Zhbm3S2dlz7P1GBDg. Then, when you add the environment variable DEVELOPER_KEY, add another environment variable called MY_CHANNEL_ID, with the value of that your channel ID. Then you can say, "Alexa, ask YouTube to play my playlist {name of your playlist}".

## Favorites List
If you enable list permissions as above, the skill will make a second list called "YouTube Favorites". You can use this to set shortcuts to videos you want often, or that are hard to find in search results.
Look in the lists in the Alexa app, or at alexa.amazon.com, and you will see how it works. You add an item like:

That song I like | https://youtu.be/ZyhrYis509A

super awesome playlist | https://www.youtube.com/playlist?list=PL1EQjK4xc6hsirkCQq-MHfmUqGMkSgUTn

Then you can just say "Alexa, ask YouTube to play that song I like" or "Alexa, ask YouTube to play super awesome playlist", and it shoulds play whatever you have linked. The | character separates the name from the link (on mobile it can be hard to find, on Android go to the second page of symbols).
If you find a video/playlist/channel that you like, and want to add it to your favorites, you can just say "Alexa, ask YouTube to add this video/playlist/channel to my favorites". It will then appear in the list, but you probably want to edit the name, as it just takes the video title. (Adding to favorites is currently only in English, email me if you want to translate.)

## FAQ
* **Alexa tells me she can't find any supported video skills, what does that mean?**
Alexa is trying to be too clever, and not launching this skill. Start your request by saying 'Alexa, launch YouTube' and then when she says 'Welcome to YouTube', ask for the video you want.
* **She still says she can't find any video skills.**
Make sure to follow step 19 above, enabling Testing for Development.
* **She still says she can't find any video skills!**
Try using a different word to start the skill. In English, say "Alexa, launch YouTube". In German, say "Alexa, öffne YouTube". In Italian, say "Alexa, avvia YouTube". In Spanish, say "Alexa, abrir YouTube".
* **I am getting another issue, can you fix it?**
Hopefully, drop me an email!
* **If I try and test in the Developer Console, it says 'Unsupported Directive. AudioPlayer is currently an unsupported namespace. Check the device log for more information.'**
That is normal, the Developer Console doesn't play audio. You just need to enable testing through the Developer Console, then you can use the skill through your Alexa device.
* **Why don't more videos work as video?**
Alexa doesn't provide any ability to enqueue videos, so you only get one video, then it stops. So it only plays videos if you ask for one specific video, or if it is a live video.
* **Didn't the code used to be freely available?**
Yes, it did. Unfortunately people started stealing my code and taking credit for it, and asking for donations, so now the code is private.
