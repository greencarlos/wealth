# Wealth


*Reading is key. Reading has made me rich over time.* 

*- Warren Buffett*


Apple lost my e-books with the last update, so I'm backing them up here.

# EBooks and PDFs


The primary goal is freedom and to think about money less.

[PDF Drive](https://pdfdrive.com) | [Ocean of PDF](https://oceanofpdf.com) | [Yarrlist](https://yarrlist.net/ebooks-list) | [Berkshire Hathaway](https://berkshirehathaway.com/letters/letters.html)


# Audiobooks


[FREE audio books](https://youtube.com/results?search_query=free+audiobooks) | [Youtube to mp3 download](https://flvto.world) | [ffmpeg](https://ffmpeg.org) | [Git large file](https://git-lfs.com[](https://m.youtube.com/watch?v=phMoT_2rYN4&pp=QAFIAQ%3D%3D&ra=m))


`brew install ffmpeg`


**To convert every audio file in a folder to `.m4b` with FFmpeg**, use a simple loop in Terminal (or a shell script).

### Basic command (current folder)
Open Terminal, `cd` into the folder that contains your files, then run:

```bash
for f in *.{mp3,wav,flac,m4a,ogg,aac}; do
  [ -f "$f" ] || continue
  ffmpeg -n -i "$f" -c:a aac -b:a 128k -map_metadata 0 "${f%.*}.m4b"
done
```

### What the options do
- `-n` → skip files that already have an output (safe default; change to `-y` if you want to overwrite).
- `-c:a aac` → encode audio as AAC (required for M4B).
- `-b:a 128k` → good quality bitrate for audiobooks (use `64k` or `96k` for smaller files, `192k` for higher quality).
- `-map_metadata 0` → copy title, artist, album, etc. from the original file.
- `"${f%.*}.m4b"` → keeps the original name and changes the extension to `.m4b`.

### Convert a specific folder
```bash
FOLDER="/path/to/your/folder"

for f in "$FOLDER"/*.{mp3,wav,flac,m4a,ogg,aac}; do
  [ -f "$f" ] || continue
  ffmpeg -n -i "$f" -c:a aac -b:a 128k -map_metadata 0 "${f%.*}.m4b"
done
```

### Tips
- M4B is just an MPEG-4 container with AAC audio (often used for audiobooks). The command above produces valid M4B files.
- If you also want chapter markers, you need a separate step (FFmpeg can add them from a chapter file, but that’s more advanced).
- Test on one file first:  
  `ffmpeg -n -i "example.mp3" -c:a aac -b:a 128k -map_metadata 0 "example.m4b"`
- After conversion, you can verify a file with:  
  `ffprobe -hide_banner "example.m4b"`

Would you like a version that also creates chapters, uses a different bitrate, or processes subfolders?




### Linux / macOS (Terminal) Zip Files
Run this command in the target directory to create a .zip file for every file, preserving the original name:

`for f in *; do [ -f "$f" ] && zip "${f}.zip" "$f"; done`

To include hidden files (dotfiles), use: 

`for f in * .[!.]* ..?*; do [ -f "$f" ] && zip "${f}.zip" "$f"; done`

To use 7-Zip instead (better compression): 

`for f in *; do [ -f "$f" ] && 7z a "${f}.7z" "$f"; done`
