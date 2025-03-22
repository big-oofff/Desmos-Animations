# Desmos-Animations
All my animations from DesmosBezierRenderer, a program that draws bezier curves to resemble inputted png frames.

https://github.com/user-attachments/assets/27ff7aa9-3f17-44bc-93db-a0c32bd37503

 For video animations, cnvmp3 is used to download youtube videos, which is parsed into individual frames by ffmpeg in my wsl terminal:

`ffmpeg -i "<VIDEO_FILE>" -vf "fps=<VIDEO_FPS>" "frame%d.png"` 


Pressing `Windows + R` and inputting `\\wsl$\Ubuntu\home\{USER}\DesmosBezierRenderer\frames` puts you in the frames folder, where you can copy all of the ffmpeg frames into the folder. 

To speed up the render video, run `ffmpeg -i input.mp4 -vf "setpts=0.5*PTS" output.mp4`. This speeds it up by 2x. Making the `setps` element smaller increases video speed, and vice versa. However, this doesn't auto trim the video.

To trim, run `ffmpeg -ss {START_TIME} -i example.mp4 -to {END_TIME} -c:v copy -c:a copy trimmed_example.mp4`. For instance, `ffmpeg -ss 00:01:00 -i example.mp4 -to 00:01:30 -c:v copy -c:a copy trimmed_example.mp4` trims from 1 minute to 1 minute and 30 seconds with respect to the video timestamps. 

To split audio from original video, run `ffmpeg -i infile.mp4 -an -c:v copy videoout.mp4 -vn -c:a copy audioout.mp4`. Then, merge into the trimmed sped up video: `ffmpeg -i input.mp4 -i input.mp3 -c copy -map 0:v:0 -map 1:a:0 output.mp4`


