# Video Editing
This is a sideline hobby, enjoy the resources I have found.

## My Best Video Editors for Linux
I found these video editors to be outstanding:

[Kdenlive](https://kdenlive.org/) GPL.  
[Lightworks](http://www.lwks.com/) Commercial but free.
[Openshot](http://openshot.org/) GPL.

## Best list of free stock free videos to use
I needed clips for some of my videos, I use these resources;

[pond5](http://www.pond5.com/free-stock-footage/) Free clip per week.  
[motionelements](http://www.motionelements.com/) Affordable $1 videos.  
[vidsplay](http://www.vidsplay.com/) Free.  
[givemefreeart](http://givemefreeart.com/Downloads) Free collection.  
[footagecrate](http://footagecrate.com/backgrounds.html) Free collection.  
[partnersinrhyme](http://www.partnersinrhyme.com/video/) Free collection.  
[stockfootageforfree](http://www.stockfootageforfree.com/) Register and Free download.  

## Converting clips to mp4-h264
Without losing any quality use:  
`ffmpeg -i LostInTranslation.mkv -vcodec copy -acodec copy LostInTranslation.mp4`

Or use an application like [Handbrake](https://handbrake.fr/)

## Downloading playists from youtube
`youtube-dl -ix -k --audio-format mp3 http://www.youtube.com/playlist?list=XXXXXXXXXXX`

Or if you have a list id simply do:
`youtube-dl -ix -k --audio-format mp3 XXXXXXXXXXX`

PS: If you want, you can edit ~/.config/youtube-dl.conf to contain options you always want, such as -i or --audio-format mp3.



