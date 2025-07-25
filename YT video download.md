## Download Video with Format Selection
``` bash 
yt-dlp -F https://youtu.be/d1pZMlNzOKc
```
- Then can see a list view like this ![](assets/Pasted%20image%2020250626172616.png)
``` bash 
# Here 248 and 251 one IDs of video and audio
yt-dlp -f "248+251" https://youtu.be/d1pZMlNzOKc
```

## Download You tube subtitle

``` bash 
yt-dlp --skip-download --write-subs --sub-langs en https://youtu.be/d1pZMlNzOKc
```

- `--skip-download` means no video file—just subtitles
- `--write-subs` fetches manual subtitles (not the auto-generated ones)
- `--sub-langs en` pulls the English track—change if the track’s in another language
- [Learn more from github readme](https://github.com/yt-dlp/yt-dlp?tab=readme-ov-file#subtitle-options)
