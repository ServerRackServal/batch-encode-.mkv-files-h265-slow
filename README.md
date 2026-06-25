Batch Encode .mkv Files to h265 Script README

**Prerequisites**
- Your OS should be Linux. I do not use Windows or MacOS and cannot guarantee success in these environments.
- ffmpeg should be installed before running this script.

**Description**

I created this script to prevent my Jellyfin server from transcoding video files, which is difficult on the hardware and causes lag.

This program, when run, will take every **.mkv** file in the same directory/folder as it and encode it using the h265 compression codec. This process takes a long time. In my experience, with the settings that I use in this file, it's roughly 1:1 with the video itself. This is likely depenent on your CPU.

It is **highly recommended** to run the file from the terminal so that you can visibly see the process and make sure there are no errors. The steps to run it in the terminal are down below. You can technically run the file by double clicking it after it's turned into an executable, but I wouldn't recommend it. If you need to stop the code, it becomes difficult to do so when not starting in the terminal.

If there are no errors, the file will create a new video with the same name as the video being
encoded + " H265" at the end. You do not need to rename the files to remove spaces;
this has been accounted for when creating the script.

**Warning**

There are _no protections_ built in to prevent the program from overwriting the copy if you run this
program more than once without moving any videos. Run at your own risk.

**How to run the file in terminal**

- Copy and paste the entire code into a .sh file.
- Open your terminal and move to the directory/folder that you have the .sh file saved in.
- Run command 'chmod u+x [file name].sh'. This will make the program executable.
- Place .mkv files in the same directory/folder as the .sh file.
- In the same terminal you just opened, run command './[file name].sh'
- Wait until the file is done. This can take awhile. If you're doing several hour-long videos, I'd recommend doing this overnight.
- The file will stop running on its own when there are no more valid videos to encode.

**Notes**

- CRF value is set to _22_. 18-22 is considered visually lossless for h265. You can put a higher number to increase compression and lower the time spent compressing, but the video may lose visual quality.
- Valid CRF Values: (1 - 51)
- All attached audio tracks will be carried over to the new file.
- All attached subtitle tracks will carried over to the new file.
- The preset time is set to _slow_. This is to improve compression and quality, but increases time spent compressing.
- All audio tracks will be converted to _aac_. This is done because Jellyfin supports aac universally. If you want to preserve your audio file's typing, change '-c:a aac' to '-c:a copy'.
