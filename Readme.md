# Docker-based FFmpeg and FFprobe Wrappers

Wrapper scripts for FFmpeg and FFprobe that run these tools inside a Docker container. These scripts allow you to use FFmpeg and FFprobe without installing them directly on your system. Goal: enable speech models like Whisper without installing ffmpeg + depedencies on the host.

## Features

- Run FFmpeg and FFprobe commands using Docker
- Handle input from stdin and output to stdout
- Process local files by temporarily copying them into the Docker container
- Copy output files back to the host system
- Support for all FFmpeg and FFprobe command-line options

## Prerequisites

- Docker
- Zsh shell

## Installation

1. Clone this repository or download the script files.
2. Make the scripts executable:
   ```
   chmod +x ffmpeg ffprobe
   ```
3. Add the directory containing these scripts to your PATH:
   ```
   export PATH=$PATH:.
   ```

## Usage

Use these scripts just as you would use the regular ffmpeg and ffprobe commands. The scripts will handle the Docker setup and file management automatically.

### FFmpeg Example

```
./ffmpeg -i input.mp4 -c:v libx264 -crf 23 -c:a aac -b:a 128k output.mp4
```

### FFprobe Example

```
./ffprobe -v quiet -print_format json -show_format -show_streams input.mp4
```

## How It Works

1. The scripts create a temporary directory to store input and output files.
2. Input files are copied to this temporary directory.
3. The FFmpeg or FFprobe command is run inside a Docker container, with the temporary directory mounted as a volume.
4. Output files are copied back to the current directory.
5. The temporary directory is cleaned up.

## Notes

- The scripts use the `jrottenberg/ffmpeg` Docker image.
- Input and output via stdin/stdout is supported.
- File paths in the command arguments are automatically adjusted for use within the Docker container.
