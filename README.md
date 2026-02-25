# FreeClimber – McCabe Lab Edition (Video-enabled Negative Geotaxis Analysis)

This repository contains a McCabe Lab–maintained version of FreeClimber, 
extended to generate annotated climbing videos with overlaid particle detection 
and vial assignment.

## Differences from upstream FreeClimber

Compared to the original FreeClimber repository:

- Added automatic video generation (step_8) with particle overlays
- Custom vial colormap for consistent experimental visualization

Upstream repository:
https://github.com/adamspierer/FreeClimber

## Installation

Please follow the installation instructions in:

`README_UPSTREAM.md`

(Original FreeClimber installation guide preserved for completeness.)

## Additional requirements (for video generation)

Video export requires:

- ffmpeg
- matplotlib with animation support

On macOS:
brew install ffmpeg

On Ubuntu:
sudo apt install ffmpeg

## Running the analysis with video export

Ensure `makevideo = True` in `scripts/detector.py`.

This will:
- Detect climbing particles
- Compute group climbing velocity
- Generate an annotated MP4 video with overlaid detections

## License and Attribution

This repository includes and modifies code from:

FreeClimber (Adam Spierer et al.)
MIT License

See LICENSE.txt for details.
