# chaiNNer

[![GitHub Latest Release](https://img.shields.io/github/v/release/joeyballentine/chaiNNer)](https://github.com/joeyballentine/chaiNNer/releases/latest)
[![GitHub Total Downloads](https://img.shields.io/github/downloads/joeyballentine/chaiNNer/total)](https://github.com/joeyballentine/chaiNNer/releases)
[![License](https://img.shields.io/github/license/joeyballentine/chaiNNer)](./LICENSE)
[![Discord](https://img.shields.io/discord/930865462852591648?label=Discord&logo=Discord&logoColor=white)](https://discord.gg/pzvAKPKyHM)

<p align="center">
  <a href="https://github.com/joeyballentine/chaiNNer/releases" target="_blank">
    <img src="src/public/banner.png" width="720" />
  </a>
</p>

A flowchart/node-based image processing GUI aimed at making chaining image processing tasks (especially upscaling done by neural networks) easy, intuitive, and customizable.

No existing upscaling GUI gives you the level of customization of your image processing workflow that chaiNNer does. Not only do you have full control over your processing pipeline, you can do incredibly complex tasks just by connecting a few nodes together.

chaiNNer is also cross-platform, meaning you can run it on Windows, MacOS, and Linux.

For help, suggestions, or just to hang out, you can join the [chaiNNer Discord server](https://discord.gg/pzvAKPKyHM)

Remember: chaiNNer is still a work in progress and in alpha. While it is slowly getting more to where we want it, it is going to take quite some time to have every possible feature we want to add. If you're knowledgeable in TypeScript, React, or Python, feel free to contribute to this project and help us get closer to that goal.

## Installation

Download the latest release from the [Github releases page](https://github.com/joeyballentine/chaiNNer/releases) and run the installer best suited for your system. Simple as that.

You don't even need to have Python installed, as chaiNNer will download an isolated integrated Python build on startup. From there, you can install all the other dependencies via the Dependency Manager.

If you do wish to use your system Python installation still, you can turn the system Python setting on. However, it is much more recommended to use the integrated Python. If you do wish to use your system Python, make sure the Python version you are using is either 3.8 or 3.9. 3.10 also should work for the most part, but it is not fully supported at this time.

If you are using the provided .zip portable version of chaiNNer, please be aware that the integrated Python it uses is not portable like the rest of it.

## How To Use

### Basic Usage

While it might seem intimidating at first due to all the possible options, chaiNNer is pretty simple to use. For example, this is all you need to do in order to perform an upscale:

<p align="center">
    <img src="src/public/simple_screenshot.png" width="480" />
</p>

Before you get to this point though, you'll need to install one of the neural network frameworks from the dependency manager. You can access this via the button in the upper-right-hand corner. ChaiNNer offers support for PyTorch (with select model architectures), NCNN, and ONNX. For Nvidia users, PyTorch will be the preferred way to upscale. For AMD users, NCNN will be the preferred way to upscale.

All the other Python dependencies are automatically installed, and chaiNNer even carries its own integrated Python support so that you do not have to modify your existing Python configuration.

Then, all you have to do is drag and drop (or double click) node names in the selection panel to bring them into the editor. Then, drag from one node handle to another to connect the nodes. Each handle is color-coded to its specific type, and while connecting will show you only the compatible connections. This makes it very easy to know what to connect where.

Once you have a working chain set up in the editor, you can press the green "run" button in the top bar to run the chain you have made. You will see the connections between nodes become animated, and start to un-animate as they finish processing. You can stop or pause processing with the red "stop" and yellow "pause" buttons respectively. Note: pressing stop is usually unable to kill an in-progress upscale during the actual upscaling step. This is a known issue without a workaround at the moment, so just be patient and wait for it to finish or restart chaiNNer.

<p align="center">
    <img src="src/public/screenshot.png" width="540" />
</p>

### Tips & Tricks

To select multiple nodes, hold down shift and drag around all the nodes you want selected. You can also select an individual node by just clicking on it. When nodes are selected, you can press backspace or delete to delete them from the editor.

To batch upscale, create an Image Iterator node and drag the nodes you want to use into the iterator's editor area. You can expand the iterator by clicking and dragging the bottom right corner outwards (like you would a UI window). Simply wire up a chain in an iterator the same as you would normally, and when you click run it will run on every image in the folder you chose. You also can select an entire existing chain, and drag it into the iterator's editor area to essentially convert the entire thing into an iterable chain.

You can right-click in the editor viewport to show an inline nodes list to select from. You also can get this menu by dragging a connection out to the editor rather than making an actual connection, and it will show compatible nodes to automatically create a connection with.

### Helpful Resources

- [Kim's chaiNNer Templates](https://github.com/kimberly990/kim-chaiNNer-Templates/)
  - A collection of useful chain templates that can quickly get you started if you are still new to using chaiNNer.
- [Upscale Wiki Model Database](https://upscale.wiki/wiki/Model_Database)
  - A very nice collection of mostly ESRGAN models that have been trained for various tasks.

## Compatibility Notes

- Arch Linux users may need to manually install libxcrypt before chaiNner's integrated Python will correctly start up.

- Apple M1 laptops are mostly untested, though they are theoretically supported.

## GPU Support

For PyTorch inference, only Nvidia GPUs are supported. If you do not have an Nvidia GPU, you will have to use PyTorch in CPU mode. This is because PyTorch only support's Nvidia's CUDA. MacOS also does not support CUDA at all, so PyTorch will only work in CPU mode on MacOS.

If you have an AMD or Intel GPU that supports NCNN however, chaiNNer now supports NCNN inference. You can use any existing NCNN .bin/.param model files (only ESRGAN-related SR models have been tested), or use chaiNNer to convert a PyTorch model to ONNX, and then convert that to NCNN (via convertmodel.com). Conversion straight from PyTorch to NCNN may come in the future, however I currently have no easy way of doing this.

For Nvidia GPUs, ONNX is also an option to be used. ONNX will use CPU mode on non-Nvidia GPUs, similar to PyTorch.

## Model Architecture Support

chaiNNer currently supports a limited amount of neural network architectures. More architectures will be supported in the future.

### Pytorch

- [ESRGAN](https://github.com/xinntao/ESRGAN) (RRDBNet)
  - This includes regular [ESRGAN](https://github.com/xinntao/ESRGAN), [ESRGAN+](https://github.com/ncarraz/ESRGANplus), "new-arch ESRGAN" ([RealSR](https://github.com/jixiaozhong/RealSR), [BSRGAN](https://github.com/cszn/BSRGAN)), [SPSR](https://github.com/Maclory/SPSR), and [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)
- [Real-ESRGAN Compact](https://github.com/xinntao/Real-ESRGAN) (SRVGGNet)
- [Swift-SRGAN](https://github.com/Koushik0901/Swift-SRGAN)

### NCNN

- Technically, almost any SR model should work assuming they follow a typical CNN-based SR structure, however I have only tested with ESRGAN (and its variants) and with Waifu2x

### ONNX

- Similarly to NCNN, technically almost any SR model should work assuming they follow a typical CNN-based SR structure, however I have only tested with ESRGAN.

## Building chaiNNer Yourself

I provide pre-built versions of chaiNNer here on GitHub. However, if you would like to build chaiNNer yourself, simply run `npm install` (make sure that you have at least npm v7 installed) to install all the nodejs dependencies, and `npm run make` to build the application.

## Planned Features

- Check the Discord server for a list of planned features.

## FAQ

**What does the name mean?**

- chaiNNer is a play on the fact that you can "chain" different tasks together, with the NN in the name being a common abbreviation for Neural Networks. This is following the brilliant naming scheme of victorca25's machine learning tools (traiNNer, iNNfer, augmeNNt) which he granted me permission to use for this as well.

**Why not just use Cupscale/IEU/CLI?**

- All of these tools are viable options, but as anyone who has used them before knows they can be limited in what they can do. Many features like chaining or interpolating models are hardcoded in and provide little flexibility. Certain features that would be useful, like being able to use a separate model on the alpha layer of an image for example, just do not exist in Cupscale. Inversely, you can pretty much do whatever you want with chaiNNer provided there are nodes implemented. Whatever weird feature you want implemented, you can implement yourself by connecting nodes however you want. Cupscale also does not have other image processing abilities like chaiNNer does, such as adjusting contrast.

- This all being said however, Cupscale, IEU, CLI, or other tools are still useful for things chaiNNer currently cannot do, like converting PyTorch models to NCNN without jumping through hoops. (That's pretty much it though)

**Wouldn't this make it more difficult to do things?**

- In a way, yes. Similarly to how programming your own script to do this stuff is more difficult, chaiNNer will also be a bit more difficult than simply dragging and dropping an image and messing with some sliders and pressing an upscale button. However, this gives you a lot more flexibility in what you can do. The added complexity is really just connecting some dots together to do what you want. That doesn't sound that bad, right?

**What platforms are supported?**

- Windows, Linux, and MacOS are all supported by chaiNNer. However, MacOS currently lacks GPU support for pytorch, so I highly recommend using another OS if you need that functionality. M1 MacBooks also are not very well tested, but should work now.
