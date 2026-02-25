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

### Customizing vial color maps

Vial colors in the annotated video are controlled by the `vial_color_map`
defined in `scripts/detector.py`.

By default, this McCabe Lab edition uses a custom `LinearSegmentedColormap`
to ensure consistent visualization across experimental conditions.

To modify the color scheme:

1. Open `scripts/detector.py`
2. Locate the section defining:

```python
colors = [...]
cmap = LinearSegmentedColormap.from_list(...)
self.vial_color_map = cmap
```

Replace the RGB tuples in colors with your desired values.

RGB values must be floats between 0 and 1:

```python
colors = [
    (0.0, 0.0, 1.0),   # blue
    (1.0, 0.0, 0.0),   # red
    (0.0, 1.0, 0.0)    # green
]
```

Alternatively, you may revert to a standard matplotlib colormap:

```python
import matplotlib.cm as cm
self.vial_color_map = cm.viridis
```

Changing the colormap affects visualization only and does not alter
particle detection, tracking, or velocity computation.

## License and Attribution

This repository includes and modifies code from:

FreeClimber (Adam Spierer et al.)
MIT License

See LICENSE.txt for details.
