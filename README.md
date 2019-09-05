Collection of small scripts to help me organize video files.

- videolinkgen
- simple-ffmpeg-thumbnailer

Those scripts might be useful when:
- Video files are stored in Pictures folder.  
  But you want to see them in Videos folder without having to copy or move them from Pictures folder.  
  You can use videolinkgen to create symbolic links in Videos folder, which point to videos in Pictures folder.
- File manager doesn't show thumbnails for some video files.
  You can use simple-ffmpeg-thumbnailer as a thumbnailer program to solve the problem.

## Prerequisites
The scripts are intended for use in the following environment.
- FreeBSD (12.0)
- XFCE4 (4.12)

The scripts also needs the following third-party software. I installed them using pkg.
- perl (for videolinkgen)
- ffmpeg (for simple-ffmpeg-thumbnailer)

## How to Use
### videolinkgen
It scans the specified source folder for video files, then creates a symlink to each video under the specified destination folder.  
Symlinks will be organized by subfolders like ~/Videos/2019, ~/Videos/2018, etc.

The script also deletes broken symlinks under the destination folder.

Typical usage is as follows.
```
videolinkgen ~/Pictures ~/Videos
```

### simple-ffmpeg-thumbnailer
This is a quick replacement for ffmpegthumbnailer.

In my environment, it seems ffmpegthumbnailer cannot create thumbnails for some video formats (e.g. avi(MJPEG) and some 3gp) even though ffmpeg alone can do it.

To solve this problem:
1. Uninstall ffmpegthumbnailer
   ```
   $ sudo pkg delete ffmpegthumbnailer
   ```
2. Register the script as a thumbnailer.
   ```
   $ sudo sh -c "simple-ffmpeg-thumbnailer -c > /usr/local/share/thumbnailers/simple-ffmpeg.thumbnailer"
   ```
3. Restart your tumblerd (XFCE4's thumbnailer service daemon)
   ```
   $ pkill tumblerd
   ```
