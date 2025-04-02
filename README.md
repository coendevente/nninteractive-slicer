![alt text](img/header_image.png)

# `nnInteractiveSlicer`: nnInteractive meets 3D Slicer

This repository makes [nnInteractive](https://github.com/MIC-DKFZ/nnInteractive) available in [3D Slicer](https://www.slicer.org/). nnInteractive is a deep learning-based framework for interactive segmentation of 3D images, allowing for fast voxel-wise segmentation using prompts like points, scribbles, bounding boxes, and lasso. You can read more about nnInteractive in the [ArXiv paper](https://arxiv.org/abs/2503.08373), or in the original [GitHub repository](https://github.com/MIC-DKFZ/nnInteractive). 3D slicer is a free and open source medical image viewer, and can be downloaded [here](https://download.slicer.org/).

## Table of contents

- [Installation](#installation)
  - [Server side](#server-side)
  - [Client side: Installation in 3D Slicer](#client-side-installation-in-3d-slicer)
- [Usage](#usage)
  - [Editing an existing segment
](#editing-an-existing-segment)
  - [Keyboard shortcuts](#keyboard-shortcuts)
- [Common issues](#common-issues)
- [Contributing](#contributing)
- [Citation](#citation)
- [License](#license)

## Installation

`nnInteractiveSlicer` needs to be set up on the server side and the client side. The server side needs relatively heavy compute, as described here:

> You need a Linux or Windows computer with a Nvidia GPU. 10GB of VRAM is recommended. Small objects should work with <6GB. nnInteractive supports Python 3.10+
> 
> -- [The nnInteractive README](https://github.com/MIC-DKFZ/nnInteractive?tab=readme-ov-file#prerequisites)

The client machine _can_ be the same as the server machine.

### Server side

You can install the server side of `nnInteractiveSlicer` in two different ways:

#### Option 1: Using Docker

```
docker pull coendevente/nninteractive-slicer-server:latest
docker run --gpus all --rm -it -p 1527:1527 coendevente/nninteractive-slicer-server:latest
```

This will make the server available under port `1527` on your machine. If you would like to use a different port, say `1627`, replace `-p 1527:1527` with `-p 1627:1527`.

#### Option 2: Using `pip`

```
pip install nninteractive-slicer-server
nninteractive-slicer-server --host 0.0.0.0 --port 1527
```

If you would like to use a different port, say `1627`, replace `--port 1527` with `--port 1627`.

### Client side: Installation in 3D Slicer

For now, `nnInteractiveSlicer` is not yet available in the Extensions Manager of 3D Slicer. So, currently, the following steps are still needed to install the `nnInteractiveSlicer` extension on the client side in 3D Slicer:

1. `git clone git@github.com:coendevente/nninteractive-slicer.git` (or download the current project as a `.zip` file from GitHub).
2. Open 3D Slicer and click the Module dropdown menu in the top left of the 3D Slicer window:
	![Slicer dropdown menu](img/dropdown.png)
3. Go to `Developer Tools` > `Extension Wizard`.
4. Click `Select Extension`.
5. Locate the `nninteractive-slicer` folder you obtained in Step 1, and select the `slicer_plugin` folder and click "Open".
6. Go to the Module dropdown menu again and go to `Segmentation` > `nnInteractiveSlicer`. This should result in the following view:
  ![First view of the Slicer extension](img/plugin_first_sight.png)
7. Configure the right server settings by going to the `Configuration` tab. Then type in the URL of the server you set up in the [server side](#server side) installation procedure. This should look something like `http://remote_host_name:1527` or, if you run the server locally, `http://localhost:1527`.

## Usage

Once you have completed the installation above, you can use `nnInteractiveSlicer` as follows:

1. If you haven't done so already, load in your image (e.g., through dragging your image file into Slicer).

2. Click one of the Interaction Tool buttons from the Interactive Prompts tab (point, bounding box, scribble, or lasso) and place your prompt in the image. This should result in a segmentation.

3. If needed, you can correct the generated segmentation with positive and negative prompts (between which you can toggle using the Positive/Negative buttons). 

	a) Alternatively, you can reset the current segment using the "Reset segment button".

4. You can add a new segment by clicking the "Next segment" button, or clicking the "+ Add" button in the Segment Editor. You can always go back to previous segments by selecting it in the Segment Editor.

### Editing an existing segment
You can edit an existing segmentation (generated using this plugin, or obtained otherwise, such as through loading in a segmentation file), by selecting the segment in the Segment Editor. Prompts are always applied to the selected segment.

### Keyboard shortcuts
Each button in the Interactive Prompts tab has a keyboard shortcut, indicated by the underlined letter.


## Common issues

- When resetting the server, the Slicer extension sometimes fails silently. Reloading the plugin or restating Slicer often helps.

## Contributing
Read more on how to contribute to this repository [here](CONTRIBUTING.md), while taking into account the [code of conduct](CODE_OF_CONDUCT.md).

## Citation

When using `nnInteractiveSlicer`, please cite the original `nnInteractive` paper:

> Isensee, F.*, Rokuss, M.*, Krämer, L.*, Dinkelacker, S., Ravindran, A., Stritzke, F., Hamm, B., Wald, T., Langenberg, M., Ulrich, C., Deissler, J., Floca, R., & Maier-Hein, K. (2025). nnInteractive: Redefining 3D Promptable Segmentation. https://arxiv.org/abs/2503.08373
*: equal contribution

Link: [![arXiv](https://img.shields.io/badge/arXiv-2503.08373-b31b1b.svg)](https://arxiv.org/abs/2503.08373)

## License
This repository is available under a Apache-2.0 license (see [here](LICENSE)). **Please note** that the weights that are being downloaded when running the `nnInteractiveSlicer` server are available under a `Creative Commons Attribution Non Commercial Share Alike 4.0` license, as described in the original nnInteractive respository [here](https://github.com/MIC-DKFZ/nnInteractive/tree/master?tab=readme-ov-file#license).
