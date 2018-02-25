# PSFGAN

This project is the implementation of the paper "<tt>PSFGAN</tt>: a generative adversarial network system for separating quasar point sources and host galaxy light". This code can be used to create images for training sets and to apply pretrained models to new data.

## Prerequisites
Linux or OSX
NVIDIA GPU + CUDA CuDNN for training on GPU's

We further use the following tools to create training and testing sets:
<tt>GALFIT</tt>, <tt>Source Extractor</tt>

## Dependencies
Training requires the following python packages: <tt>tensorflow</tt>, <tt>numpy</tt>

Testing requires the following python packages: <tt>tensorflow</tt>, <tt>numpy</tt>, <tt>astropy</tt> (testing output is saved as a .fits file)

Creating training and testing sets requires the following python packages: <tt>numpy</tt>, <tt>scipy</tt>, <tt>matplotlib</tt>, <tt>astropy</tt>, <tt>photutils</tt>,

## Get our code
Clone this repo:
```bash
git clone https://github.com/SpaceML/PSFGAN.git
cd  PSFGAN/
```

## Run our code
The first step always is modifying the file config.py. The most important parameters are the following:
* core_path: Path to directory containing all the subdirectories.
* redshift: Unique redshift identifier used for naming the subdirectories.
* filter_: Unique identifier to distinguish images observed in different filters.
* model_path: Path to .ckpt file of pretrained model used in test.py. Should be an empty string if PSFGAN is used in training mode.

### Create training/validation/testing sets
The original images to be used for training should be in a folder "fits_train" and the original images for the test (validation) set in a folder "fits_test" ("fits_eval"). The script roou.py then adds simulated AGN point sources to the centers of the original galaxies, preprocesses the images, and saves them as .npy files so that they can be importet by the GAN. 

```python
python roou.py --mode 1 --mcombine 1 # Create a test and median combine stars to extract the PSF.
```

* mode: If set to 0, the images from "fits_train" are used; if set to 1, the images from "fits_test" are used; if set to 2, the images from "fits_eval" are used.
* mcombine: If set to False, the SDSS PSF tool is used to extract a PSF for each image. If mcombine is set to True, the PSF is extracted by median combining stars from the neighborhood of the galaxy.

### Train PSFGAN


### Run a trained model