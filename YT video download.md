## Installation
- Get `yt-dlp.exe` and add it's path as environment variable.(I placed `yt-dlp.exe` in `C:\Users\rumin\AppData\Local\yt-dlp` and add this path in the system variables -> path)
- We need ffmpeg for merge video & audio track
	- to install that download `ffmpeg-master-latest-win64-gpl.zip` and add it's bin path as environment variable.[How to install ffmpeg on Windows](https://www.youtube.com/watch?v=JR36oH35Fgg)
	
## Download Video with Format Selection
``` bash 
yt-dlp -F https://youtu.be/d1pZMlNzOKc
```
- Then can see a list view like this ![](assets/Pasted%20image%2020250626172616.png)
``` bash 
# Here 248 and 251 one IDs of video and audio
# If the ffmpeg isn't installed merging will not work
yt-dlp -f "248+251" https://youtu.be/d1pZMlNzOKc
```

## Download You tube subtitle

``` bash 
yt-dlp --skip-download --write-subs --sub-langs en https://youtu.be/d1pZMlNzOKc
```

- `--skip-download` means no video file—just subtitles
- `--write-subs` fetches manual subtitles (not the auto-generated ones)
- `--sub-langs en` pulls the English track—change if the track’s in another language
- shows all available subtitle tracks
``` bash 
yt-dlp --list-subs [VIDEO_URL]
```

- [Learn more from github readme](https://github.com/yt-dlp/yt-dlp?tab=readme-ov-file#subtitle-options)

## Standard commands for downloading subtitles

Replace `[VIDEO_URL]` with the YouTube video URL and run the command from your terminal or command prompt. 

**Download all available subtitles in the SRT format** 

``` bash
yt-dlp --write-subs --convert-subs srt --all-subs --skip-download [VIDEO_URL]
```
This command does the following: 

- `--write-subs`: Requests that subtitles be written to a file.
- `--convert-subs srt`: Converts the subtitle file to the SRT format.
- `--all-subs`: Downloads all available subtitle languages.
- `--skip-download`: Prevents the video from being downloaded, saving time and disk space. 

**Download specific language subtitles**

``` bash
yt-dlp --write-subs --convert-subs srt --sub-langs en,fr --skip-download [VIDEO_URL]
```

- `--sub-langs en,fr`: Downloads subtitles only for English (`en`) and French (`fr`). You can specify multiple languages separated by commas. 

**Download automatic captions only** 

``` bash
yt-dlp --write-auto-subs --convert-subs srt --skip-download [VIDEO_URL]
```

- `--write-auto-subs`: Specifically targets and downloads the auto-generated captions provided by YouTube, which are often labeled `[lang]-orig`. 

### Steps for best results

1. **Check for available subtitles:** Before downloading, you can list all the available subtitle and caption tracks to see their language codes and formats.

``` bash
yt-dlp --list-subs [VIDEO_URL]
```
        
The output will show a list of languages, such as `en`, `fr`, or `es`. This helps you decide which language code to use in your download command.

2. **Ensure FFmpeg is installed:** `yt-dlp` relies on the external tool FFmpeg to convert subtitles from their original format (like `.vtt`) into other formats, such as `.srt`. If FFmpeg is not installed, the subtitles may be downloaded in the `.vtt` format by default. To check if you have FFmpeg, run `ffmpeg -version` in your terminal. If it is not found, you will need to install it.
  
3. **Update yt-dlp regularly:** Ensure you are using the latest version of the tool by running `yt-dlp -U` regularly, as changes on platforms like YouTube can sometimes break features.