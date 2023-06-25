# Kohya's GUI

This repository provides a Windows-focused Gradio GUI for [Kohya's Stable Diffusion trainers](https://github.com/kohya-ss/sd-scripts). The GUI allows you to set the training parameters and generate and run the required CLI commands to train the model.

## Table of Contents

1. [Tutorials](#tutorials)
2. [Installation](#installation)
   1. [Windows](#windows)
      1. [Windows Pre-requirements](#windows-pre-requirements)
      2. [Setup](#setup)
      3. [Optional: CUDNN 8.6](#optional-cudnn-86)
   2. [Linux and macOS](#linux-and-macos)
      1. [Linux Pre-requirements](#linux-pre-requirements)
      2. [Setup](#setup-1)
      3. [Install Location](#install-location)
   3. [Runpod](#runpod)
   4. [Docker](#docker)
3. [Upgrading](#upgrading)
   1. [Windows Upgrade](#windows-upgrade)
   2. [Linux and macOS Upgrade](#linux-and-macos-upgrade)
4. [Starting GUI Service](#starting-gui-service)
   1. [Launching the GUI on Windows](#launching-the-gui-on-windows)
   2. [Launching the GUI on Linux and macOS](#launching-the-gui-on-linux-and-macos)
5. [Dreambooth](#dreambooth)
6. [Finetune](#finetune)
7. [Train Network](#train-network)
8. [LoRA](#lora)
9. [Sample image generation during training](#sample-image-generation-during-training)
10. [Troubleshooting](#troubleshooting)
   1. [Page File Limit](#page-file-limit)
   2. [No module called tkinter](#no-module-called-tkinter)
   3. [FileNotFoundError](#filenotfounderror)
11. [Change History](#change-history)

## Tutorials

[How to Create a LoRA Part 1: Dataset Preparation](https://www.youtube.com/watch?v=N4_-fB62Hwk):

[![LoRA Part 1 Tutorial](https://img.youtube.com/vi/N4_-fB62Hwk/0.jpg)](https://www.youtube.com/watch?v=N4_-fB62Hwk)

[How to Create a LoRA Part 2: Training the Model](https://www.youtube.com/watch?v=k5imq01uvUY):

[![LoRA Part 2 Tutorial](https://img.youtube.com/vi/k5imq01uvUY/0.jpg)](https://www.youtube.com/watch?v=k5imq01uvUY)

Newer Tutorial: [Generate Studio Quality Realistic Photos By Kohya LoRA Stable Diffusion Training](https://www.youtube.com/watch?v=TpuDOsuKIBo):

[![Newer Tutorial: Generate Studio Quality Realistic Photos By Kohya LoRA Stable Diffusion Training](https://user-images.githubusercontent.com/19240467/235306147-85dd8126-f397-406b-83f2-368927fa0281.png)](https://www.youtube.com/watch?v=TpuDOsuKIBo)

Newer Tutorial: [How To Install And Use Kohya LoRA GUI / Web UI on RunPod IO](https://www.youtube.com/watch?v=3uzCNrQao3o):

[![How To Install And Use Kohya LoRA GUI / Web UI on RunPod IO With Stable Diffusion & Automatic1111](https://github-production-user-asset-6210df.s3.amazonaws.com/19240467/238678226-0c9c3f7d-c308-4793-b790-999fdc271372.png)](https://www.youtube.com/watch?v=3uzCNrQao3o)

## Installation

### Windows

#### Windows Pre-requirements

To install the necessary dependencies on a Windows system, follow these steps:

1. Install [Python 3.10](https://www.python.org/ftp/python/3.10.9/python-3.10.9-amd64.exe).
   - During the installation process, ensure that you select the option to add Python to the 'PATH' environment variable.

2. Install [Git](https://git-scm.com/download/win).

3. Install the [Visual Studio 2015, 2017, 2019, and 2022 redistributable](https://aka.ms/vs/17/release/vc_redist.x64.exe).

#### Setup

To set up the project, follow these steps:

1. Open a terminal and navigate to the desired installation directory.

2. Clone the repository by running the following command:
   ```
   git clone https://github.com/bmaltais/kohya_ss.git
   ```

3. Change into the `kohya_ss` directory:
   ```
   cd kohya_ss
   ```

4. Run the setup script by executing the following command:
   ```
   .\setup.bat
   ```

#### Optional: CUDNN 8.6

The following steps are optional but can improve the learning speed for owners of NVIDIA 30X0/40X0 GPUs. These steps enable larger training batch sizes and faster training speeds.

Please note that the CUDNN 8.6 DLLs needed for this process cannot be hosted on GitHub due to file size limitations. You can download them [here](https://github.com/bmaltais/python-library/raw/main/cudnn_windows.zip) to boost sample generation speed (almost 50% on a 4090 GPU). After downloading the ZIP file, follow the installation steps below:

1. Unzip the downloaded file and place the `cudnn_windows` folder in the root directory of the `kohya_ss` repository.

2. Run .\setup.bat and select the option to install cudann.

### Linux and macOS

#### Linux Pre-requirements

To install the necessary dependencies on a Linux system, ensure that you fulfill the following requirements:

- Ensure that `venv` support is pre-installed. You can install it on Ubuntu 22.04 using the command:
  ```
  apt install python3.10-venv
  ```

- Install the cudaNN drivers by following the instructions provided in [this link](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64).

- Make sure you have Python version 3.10.6 or higher (but lower than 3.11.0) installed on your system.

- If you are using WSL2, set the `LD_LIBRARY_PATH` environment variable by executing the following command:
  ```
  export LD_LIBRARY_PATH=/usr/lib/wsl/lib/
  ```

#### Setup

To set up the project on Linux or macOS, perform the following steps:

1. Open a terminal and navigate to the desired installation directory.

2. Clone the repository by running the following command:
   ```
   git clone https://github.com/bmaltais/kohya_ss.git
   ```

3. Change into the `kohya_ss` directory:
   ```
   cd kohya_ss
   ```

4. If you encounter permission issues, make the `setup.sh` script executable by running the following command:
   ```
   chmod +x ./setup.sh
   ```

5. Run the setup script by executing the following command:
   ```
   ./setup.sh


   ```

   Note: If you need additional options or information about the runpod environment, you can use `setup.sh -h` or `setup.sh --help` to display the help message.

#### Install Location

The default installation location on Linux is the directory where the script is located. If a previous installation is detected in that location, the setup will proceed there. Otherwise, the installation will fall back to `/opt/kohya_ss`. If `/opt` is not writable, the fallback location will be `$HOME/kohya_ss`. Finally, if none of the previous options are viable, the installation will be performed in the current directory.

For macOS and other non-Linux systems, the installation process will attempt to detect the previous installation directory based on where the script is run. If a previous installation is not found, the default location will be `$HOME/kohya_ss`. You can override this behavior by specifying a custom installation directory using the `-d` or `--dir` option when running the setup script.

If you choose to use the interactive mode, the default values for the accelerate configuration screen will be "This machine," "None," and "No" for the remaining questions. These default answers are the same as the Windows installation.

### Runpod

To install the necessary components for Runpod, follow these steps:

1. Select the pytorch 2.0.1 template.

2. SSH into the Runpod.

3. In the terminal, navigate to the `/workspace` directory.

4. Clone the repository by running the following command:
   ```
   git clone https://github.com/bmaltais/kohya_ss.git
   ```

5. Run the setup script with the `-p` option:
   ```
   ./setup.sh -p
   ```

6. Connect to the public URL displayed after the installation process is completed.

### Docker

If you prefer to use Docker, follow the instructions below:

1. Ensure that you have Git and Docker installed on your Windows or Linux system.

2. Open your OS shell (Command Prompt or Terminal) and run the following commands:

   ```bash
   git clone https://github.com/bmaltais/kohya_ss.git
   cd kohya_ss
   docker compose build
   docker compose run --service-ports kohya-ss-gui
   ```

   Note: The initial run may take up to 20 minutes to complete.

   Please be aware of the following limitations when using Docker:

   - All training data must be placed in the `dataset` subdirectory, as the Docker container cannot access files from other directories.
   - The file picker feature is not functional. You need to manually set the folder path and config file path.
   - Dialogs may not work as expected, and it is recommended to use unique file names to avoid conflicts.
   - There is no built-in auto-update support. To update the system, you must run update scripts outside of Docker and rebuild using `docker compose build`.

   If you are running Linux, an alternative Docker container port with fewer limitations is available [here](https://github.com/P2Enjoy/kohya_ss-docker).

## Upgrading

To upgrade your installation to a new version, follow the instructions below.

### Windows Upgrade

If a new release becomes available, you can upgrade your repository by running the following commands from the root directory of the project:

1. Pull the latest changes from the repository:
   ```powershell
   git pull
   ```

2. Run the setup script:
   ```powershell
   .\setup.bat
   ```

### Linux and macOS Upgrade

To upgrade your installation on Linux or macOS, follow these steps:

1. Open a terminal and navigate to the root

 directory of the project.

2. Pull the latest changes from the repository:
   ```bash
   git pull
   ```

3. Refresh and update everything:
   ```bash
   ./setup.sh
   ```

## Starting GUI Service

To launch the GUI service, you can use the provided scripts or run the `kohya_gui.py` script directly. Use the command line arguments listed below to configure the underlying service.

```text
--listen: Specify the IP address to listen on for connections to Gradio.
--username: Set a username for authentication.
--password: Set a password for authentication.
--server_port: Define the port to run the server listener on.
--inbrowser: Open the Gradio UI in a web browser.
--share: Share the Gradio UI.
```

### Launching the GUI on Windows

On Windows, you can use either the `gui.ps1` or `gui.bat` script located in the root directory. Choose the script that suits your preference and run it in a terminal, providing the desired command line arguments. Here's an example:

```powershell
gui.ps1 --listen 127.0.0.1 --server_port 7860 --inbrowser --share
```

or

```powershell
gui.bat --listen 127.0.0.1 --server_port 7860 --inbrowser --share
```

### Launching the GUI on Linux and macOS

To launch the GUI on Linux or macOS, run the `gui.sh` script located in the root directory. Provide the desired command line arguments as follows:

```bash
gui.sh --listen 127.0.0.1 --server_port 7860 --inbrowser --share
```

## Dreambooth

For specific instructions on using the Dreambooth solution, please refer to the [Dreambooth README](train_db_README.md).

## Finetune

For specific instructions on using the Finetune solution, please refer to the [Finetune README](fine_tune_README.md).

## Train Network

For specific instructions on training a network, please refer to the [Train network README](train_network_README.md).

## LoRA

To train a LoRA, you can currently use the `train_network.py` code. You can create a LoRA network by using the all-in-one GUI.

Once you have created the LoRA network, you can generate images using auto1111 by installing [this extension](https://github.com/kohya-ss/sd-webui-additional-networks).

The following are the names of LoRA types used in this repository:

1. LoRA-LierLa: LoRA for Linear layers and Conv2d layers with a 1x1 kernel.

2. LoRA-C3Lier: LoRA for Conv2d layers with a 3x3 kernel, in addition to LoRA-LierLa.

LoRA-LierLa is the default LoRA type for `train_network.py` (without `conv_dim` network argument). You can use LoRA-LierLa with our extension for AUTOMATIC1111's Web UI or the built-in LoRA feature of the Web UI.

To use LoRA-C3Lier with the Web UI, please use our extension.

## Sample image generation during training

A prompt file might look like this, for example:

```
# prompt 1
masterpiece, best quality, (1girl), in white shirts, upper body, looking at viewer, simple background --n low quality, worst quality, bad anatomy, bad composition, poor, low effort --w 768 --h 768 --d 1 --l 7.5 --s 28

# prompt 2


masterpiece, best quality, 1boy, in business suit, standing at street, looking back --n (low quality, worst quality), bad anatomy, bad composition, poor, low effort --w 576 --h 832 --d 2 --l 5.5 --s 40
```

Lines beginning with `#` are comments. You can specify options for the generated image with options like `--n` after the prompt. The following options can be used:

- `--n`: Negative prompt up to the next option.
- `--w`: Specifies the width of the generated image.
- `--h`: Specifies the height of the generated image.
- `--d`: Specifies the seed of the generated image.
- `--l`: Specifies the CFG scale of the generated image.
- `--s`: Specifies the number of steps in the generation.

The prompt weighting such as `( )` and `[ ]` are working.

## Troubleshooting

If you encounter any issues, refer to the troubleshooting steps below.

### Page File Limit

If you encounter an X error related to the page file, you may need to increase the page file size limit in Windows.

### No module called tkinter

If you encounter an error indicating that the module `tkinter` is not found, try reinstalling Python 3.10 on your system.

### FileNotFoundError

If you come across a `FileNotFoundError`, it is likely due to an installation issue. Make sure you do not have any locally installed Python modules that could conflict with the ones installed in the virtual environment. You can uninstall them by following these steps:

1. Open a new PowerShell terminal and ensure that no virtual environment is active.

2. Run the following commands to create a backup file of your locally installed pip packages and then uninstall them:
   ```powershell
   pip freeze > uninstall.txt
   pip uninstall -r uninstall.txt
   ```

   After uninstalling the local packages, redo the installation steps within the `kohya_ss` virtual environment.

## Change History

- 2023/06/24 (v21.7.12)
  - Significantly improved the setup process on all platforms
  - Better support for runpod
* 2023/06/23 (v21.7.11)
- This is a significant update to how setup work across different platform. It might be causing issues... especially for linux env like runpod. If you encounter problems please report them in the issues so I can try to address them. You can revert to the previous release with `git checkout v21.7.10`

The setup solution is now much more modulat and will simplify requirements support across different environments... hoping this will make it easier to run on different OS.
* 2023/06/19 (v21.7.10)
- Quick fix for linux GUI startup where it would try to install darwin requirements on top of linux. Ugly fix but work. Hopefulle some linux user will improve via a PR.
* 2023/06/18 (v21.7.9)
- Implement temporary fix for validation of image dataset. Will no longer stop execution but will let training continue... this is changed to avoid stopping training on false positive... yet still raise awaireness that something might be wrong with the image dataset structure.
* 2023/06/14 (v21.7.8)
- Add tkinter to dockerised version (thanks to @burdokow)
- Add option to create caption files from folder names to the `group_images.py` tool.
- Prodigy optimizer is supported in each training script. It is a member of D-Adaptation and is effective for DyLoRA training. [PR #585](https://github.com/kohya-ss/sd-scripts/pull/585) Please see the PR for details. Thanks to sdbds!
  - Install the package with `pip install prodigyopt`. Then specify the option like `--optimizer_type="prodigy"`.
- Arbitrary Dataset is supported in each training script (except XTI). You can use it by defining a Dataset class that returns images and captions.
  - Prepare a Python script and define a class that inherits `train_util.MinimalDataset`. Then specify the option like `--dataset_class package.module.DatasetClass` in each training script.
  - Please refer to `MinimalDataset` for implementation. I will prepare a sample later.
- The following features have been added to the generation script.
  - Added an option `--highres_fix_disable_control_net` to disable ControlNet in the 2nd stage of Highres. Fix. Please try it if the image is disturbed by some ControlNet such as Canny.
  - Added Variants similar to sd-dynamic-propmpts in the prompt.
    - If you specify `{spring|summer|autumn|winter}`, one of them will be randomly selected.
    - If you specify `{2$$chocolate|vanilla|strawberry}`, two of them will be randomly selected.
    - If you specify `{1-2$$ and $$chocolate|vanilla|strawberry}`, one or two of them will be randomly selected and connected by ` and `.
    - You can specify the number of candidates in the range `0-2`. You cannot omit one side like `-2` or `1-`.
    - It can also be specified for the prompt option.
    - If you specify `e` or `E`, all candidates will be selected and the prompt will be repeated multiple times (`--images_per_prompt` is ignored). It may be useful for creating X/Y plots.
    - You can also specify `--am {e$$0.2|0.4|0.6|0.8|1.0},{e$$0.4|0.7|1.0} --d 1234`. In this case, 15 prompts will be generated with 5*3.
    - There is no weighting function.
- Add pre and posfix to wd14
* 2023/06/12 (v21.7.7)
- Add `Print only` button to all training tabs
- Sort json file vars for easier visual search
- Fixed a bug where clip skip did not work when training with weighted captions (`--weighted_captions` specified) and when generating sample images during training.
- Add verification and reporting of bad dataset folder name structure for DB, LoRA and TI training.
- Some docker build fix.
* 2023/06/06 (v21.7.6)
- Small UI improvements
- Fix `train_network.py` to probably work with older versions of LyCORIS.
- `gen_img_diffusers.py` now supports `BREAK` syntax.
- Add Lycoris iA3, LoKr and DyLoRA support to the UI
- Upgrade LuCORIS python module to 0.1.6
* 2023/06/05 (v21 7.5)
- Fix reported issue with LoHA: https://github.com/bmaltais/kohya_ss/issues/922
* 2023/06/05 (v21.7.4)
- Add manual accelerate config option
- Remove the ability to switch between torch 1 and 2 as it was causing errors with the venv
* 2023/06/04 (v21.7.3)
- Add accelerate configuration from file
- Fix issue with torch uninstallation resulting in Error sometimes
- Fix broken link to cudann files
* 2023/06/04 (v21.7.2)
- Improve handling of legacy installations
* 2023/06/04 (v21.7.1)
- This is mostly an update to the whole setup method for kohya_ss. I got fedup with all the issues from the batch file method and leveraged the great work of vladimandic to improve the whole setup experience.

There is now a new menu in setup.bat that will appear:

```
Kohya_ss GUI setup menu:

0. Cleanup the venv
1. Install kohya_ss gui [torch 1]
2. Install kohya_ss gui [torch 2]
3. Start GUI in browser
4. Quit

Enter your choice:
```

The only obscure option might be option 0. This will help cleanup a corrupted venv without having to delete de folder. This van be really usefull for cases where nothing is working anymore and you should re-install from scratch. Just run the venv cleanup then select the version of kohya_ss GUI you want to instal (torch1 or 2).

You can also start the GUI right from the setup menu using option 3.

After pulling a new version you can either re-run `setup.bat` and install the version you want... or just run `gui.bat` and it will update the python modules as required.

Hope this is useful.

* 2023/06/04 (v21.7.0)
- Max Norm Regularization is now available in `train_network.py`. [PR #545](https://github.com/kohya-ss/sd-scripts/pull/545) Thanks to AI-Casanova!
  - Max Norm Regularization is a technique to stabilize network training by limiting the norm of network weights. It may be effective in suppressing overfitting of LoRA and improving stability when used with other LoRAs. See PR for details.
  - Specify as `--scale_weight_norms=1.0`. It seems good to try from `1.0`.
  - The networks other than LoRA in this repository (such as LyCORIS) do not support this option.

- Three types of dropout have been added to `train_network.py` and LoRA network.
  - Dropout is a technique to suppress overfitting and improve network performance by randomly setting some of the network outputs to 0.
  - `--network_dropout` is a normal dropout at the neuron level. In the case of LoRA, it is applied to the output of down. Proposed in [PR #545](https://github.com/kohya-ss/sd-scripts/pull/545) Thanks to AI-Casanova!
    - `--network_dropout=0.1` specifies the dropout probability to `0.1`.
    - Note that the specification method is different from LyCORIS.
  - For LoRA network, `--network_args` can specify `rank_dropout` to dropout each rank with specified probability. Also `module_dropout` can be specified to dropout each module with specified probability.
    - Specify as `--network_args "rank_dropout=0.2" "module_dropout=0.1"`.
  - `--network_dropout`, `rank_dropout`, and `module_dropout` can be specified at the same time.
  - Values of 0.1 to 0.3 may be good to try. Values greater than 0.5 should not be specified.
  - `rank_dropout` and `module_dropout` are original techniques of this repository. Their effectiveness has not been verified yet.
  - The networks other than LoRA in this repository (such as LyCORIS) do not support these options.
  
- Added an option `--scale_v_pred_loss_like_noise_pred` to scale v-prediction loss like noise prediction in each training script.
  - By scaling the loss according to the time step, the weights of global noise prediction and local noise prediction become the same, and the improvement of details may be expected.
  - See [this article](https://xrg.hatenablog.com/entry/2023/06/02/202418) by xrg for details (written in Japanese). Thanks to xrg for the great suggestion!

* 2023/06/03 (v21.6.5)
- Fix dreambooth issue with new logging
- Update setup and upgrade scripts
- Adding test folder

* 2023/05/28 (v21.5.15)
- Show warning when image caption file does not exist during training. [PR #533](https://github.com/kohya-ss/sd-scripts/pull/533) Thanks to TingTingin!
  - Warning is also displayed when using class+identifier dataset. Please ignore if it is intended.
- `train_network.py` now supports merging network weights before training. [PR #542](https://github.com/kohya-ss/sd-scripts/pull/542) Thanks to u-haru!
  - `--base_weights` option specifies LoRA or other model files (multiple files are allowed) to merge.
  - `--base_weights_multiplier` option specifies multiplier of the weights to merge (multiple values are allowed). If omitted or less than `base_weights`, 1.0 is used.
  - This is useful for incremental learning. See PR for details.
- Show warning and continue training when uploading to HuggingFace fails.
