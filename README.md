# WackyWebM

[![Weblate project translated](https://img.shields.io/weblate/progress/wackywebm?server=https%3A%2F%2Ftranslate.kiaibot.com&style=for-the-badge)](https://translate.kiaibot.com/projects/wackywebm/wackywebm)
![GitHub contributors](https://img.shields.io/github/contributors/oirnoir/wackywebm?style=for-the-badge)
![GitHub Repo stars](https://img.shields.io/github/stars/oirnoir/wackywebm?style=for-the-badge)

WackyWebM is a tool that allows you to create WebM video files with changing aspect ratios.

If you're having issues or want to share your custom modes, join the Discord Server at the bottom of this Readme.

## Dependencies

- [NodeJS v16.6 or higher](https://nodejs.org/en/download/)
- [FFmpeg](https://ffmpeg.org/download.html)
- FFprobe (included with FFmpeg)
- Various NPM packages (simply run `npm i` in the project directory after installing node to install them automatically)

Further information about dependencies and help installing them can be found [on this page](docs/dependencies.md)

## Running

After you have finished installing the dependencies, download the WackyWebM source code by either running `git clone https://github.com/OIRNOIR/WackyWebM.git` or by clicking the green button to the top right of the directory listing, then clicking "Download ZIP" and then extracting the downloaded archive.

![image](https://user-images.githubusercontent.com/69131802/182936318-d3c542bc-99a6-4f01-91e0-944c4e9bc0b0.png)

After downloading the code, you can either use one of the wrapper scripts or use the command-line interface, which is slightly less intuitive, but, for some purposes, more powerful.

### General Notes

- All arguments are entirely optional, with the one exception of the Keyframe file if you are using the corresponding `Keyframes` mode (The wrapper scripts force you to enter it, and you encounter an error when not specifying it on the command-line interface)
- The bitrate is, by default, measured in single bits per second and values that are significantly too low (like 10 bits/sec) will cause errors. Some suffixes are supported, like `k` for kilobits per second or `M` for megabits per second.
- FFmpeg can error if a file does not have a file extension, like `*.webm`. This is the case for both input and output files, even if the file content is otherwise valid data.
- "Compression", in our sense, does *not* refer to intra-frame compression, like decreasing frames' resolution. Instead, it makes the transition between different video sizes less "smooth" by updating the size less often. Reasonable values for this are typically in the range of 10 to 20.


### Using the Wrapper Scripts

On Unix-Like Operating Systems, like Linux or MacOS, run `run.sh` by running `sh run.sh` (or, in some cases, double-clicking the file - this might not always work though)

On Windows, double-click `run.bat`.

In case of an error, please run the script again from a terminal you manually started (by navigating to the folder and then running the appropriate command), instead of just double-clicking the file, so that it stays open after crashing and you can read the error (and potentially ask about it)

### Using the Command-Line Interface

To get an accurate and up-to-date list of all recognized arguments, simply run `node wackywebm.js --help` from within the project directory. Then, just run `node wackywebm.js <ARGUMENTS> <input file>`, where `<ARGUMENTS>` is simply a list of arguments like `-b 500000 -o path/to/output/file.webm`.

You do not need to quote the input file's path, even if it contains spaces, however it is recommended and if you experience issues that involve not finding the input file, please try that first.

## Modes

- `Bounce` (Default): The video's height periodically increases and decreases.
- `Shutter`: The video's width periodically increases and decreases.
- `Sporadic`: The video glitches and wobbles randomly.
- `Shrink`: The video shrinks vertically from full height to just one pixel over its entire duration.
- `AudioBounce`: The video's height changes relative to the current audio level compared to the highest within the video.
- `AudioShutter`: The video's width changes relative to the current audio level compared to the highest within the video.
- `Transparency`: Crops the video so that transparent pixels are excluded from the final result. (the result will still always be a rectangle)
- `Keyframes`: The video's height and width change based on a number of keyframes outlined in the file given as an argument. The format for said file is Described [Here](docs/keyframes.md).

Additionally, any 2 modes can be combined using a + symbol, like `Bounce+Shutter`. If one of the modes only specifies width, and one only specifies height, then those respective values are used. If there is a conflict, the value from the latter of the 2 modes is used (so `Shrink+Bounce` would result in the same effect as just `Bounce`, since it overwrites `Shrink`'s change in height.)

## Support

Common issues and questions are addressed in [the FAQ](docs/faq.md).

~~If you encounter bugs or issues and want personal help, or have recommendations, feel free to join the Discord.~~ Update 14th March 2024: The Discord has now been archived.
