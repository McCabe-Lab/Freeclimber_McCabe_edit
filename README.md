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

## Installation and requirements

> **Important:** This tutorial covers the **McCabe Lab fork** of FreeClimber, which includes video export functionality (annotated MP4 output with particle overlays). Do **not** clone or install from the upstream repository — follow the steps below instead.

### Requirements

```
- matplotlib    [3.x   ]
- numpy         [2.x   ]
- pandas        [2.x   ]
- scipy         [1.x   ]
- trackpy       [0.7   ]
- wxPython      [4.2.x ]
- ffmpeg        [7.x   ] (bundled via conda)
- ffmpeg-python [0.2.0 ]
- python        [3.10  ]
```

All dependencies are pinned in `environment.yml` and installed automatically in the steps below.

### Step 1 — Install Anaconda

We recommend running this package in an Anaconda-based virtual environment. Anaconda can be downloaded [here](https://docs.anaconda.com/anaconda/install/).

Make sure `conda` is installed (should return something like `conda 24.x.x`):

```bash
conda -V
```

Update conda if needed (press `y` when prompted):

```bash
conda update conda
```

### Step 2 — Clone this repository

```bash
cd <folder of interest>
git clone https://github.com/McCabe-Lab/Freeclimber_McCabe_edit.git
cd Freeclimber_McCabe_edit
```

### Step 3 — Create and activate the conda environment

The repository includes an `environment.yml` file that installs all required dependencies, including ffmpeg, at the correct versions. No separate `pip install` steps are needed.

```bash
conda env create -f environment.yml
conda activate fc
```

This will create an environment named `fc` running Python 3.10.

> If you already have an `fc` environment from a previous install and want to start fresh:
> ```bash
> conda env remove -n fc
> conda env create -f environment.yml
> ```

### Step 4 — Verify the installation

Run a quick test using the provided example video to confirm everything is working:

**macOS:**
```bash
pythonw ./scripts/FreeClimber_gui.py --video_file ./example/w1118_m_2_1.h264
```

**Linux:**
```bash
python ./scripts/FreeClimber_gui.py --video_file ./example/w1118_m_2_1.h264
```

The GUI should open with the example video loaded. Common errors and fixes:

| Error | Fix |
|---|---|
| `This program needs access to the screen...` | Use `pythonw` instead of `python` (macOS only) |
| `ModuleNotFoundError: No module named 'ffmpeg'` | Make sure you activated the correct environment: `conda activate fc` |
| `ModuleNotFoundError: No module named 'wx'` | Same as above — wxPython is installed inside the `fc` environment |


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

## Tutorial
Refer to TUTORIAL.md

## License and Attribution

This repository includes and modifies code from:

FreeClimber (Adam Spierer et al.)
MIT License

See LICENSE.txt for details.
