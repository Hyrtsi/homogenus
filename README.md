# Human Image Gender Classifier


This is the official repository of the Humun Gender Classifier (Homogenus) used in the paper 

***Expressive Body Capture: 3D Hands, Face, and Body from a Single Image.***

The codebase consists of the inference code. That is, given full-body human images, and their [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) 
output json files, one can augment the keypoint dectections of the openpose with the predicted gender of the detected human. 
The output classes would be either male, female, or neutral for undetected genders. 
For further details on the method please refer to the following publication,

```
Expressive Body Capture: 3D Hands, Face, and Body from a Single Image
G. Pavlakos*, V. Choutas*, N. Ghorbani, T. Bolkart, A. A. A. Osman, D. Tzionas and M. J. Black 
Computer Vision and Pattern Recognition (CVPR) 2019, Long Beach, CA
```

A pdf preprint is also available on the [project page](https://smpl-x.is.tue.mpg.de/).


## Installation

The code uses Python 3.7 and is tested on tensorflow-gpu version 1.13.1tensorboard==1.13.1
, with CUDA-10.0 and cuDNN-7.5, running on Ubuntu 18.04.

### Setup homogenus Virtual Environment

```bash
venv_dir=~/.virtualenvs/homogenus
python3 -m venv $venv_dir --system-site-packages
source $venv_dir/bin/activate
```
### Clone the project and install requirements

```bash
git clone https://github.com/nghorbani/homogenus.git
cd homogenus
python setup.py install
```

## Download models

* Download pretrained homogenus weights from the [project website](https://smpl-x.is.tue.mpg.de), downloads page. 
Uncompress the weights in a folder, *e.g. by default homogenus/trained_models/tf* , and use the directory path in the following commands.

## Run Homogenus
After installation and obtaining the weights for the model, inside the virtual environment, 
you should be able to run the homogenus_infer command to get the help:

```bash
python3 -m homogenus.tf.homogenus_infer -h

usage: homogenus_infer.py [-h] [-tm TRAINED_MODEL_DIR] -ii IMAGES_INDIR -oi
                          OPENPOSE_INDIR [-io IMAGES_OUTDIR]
                          [-oo OPENPOSE_OUTDIR]

optional arguments:
  -h, --help            show this help message and exit
  -tm TRAINED_MODEL_DIR, --trained_model_dir TRAINED_MODEL_DIR
                        The path to the directory holding homogenus trained
                        models in TF.
  -ii IMAGES_INDIR, --images_indir IMAGES_INDIR
                        Directory of the input images.
  -oi OPENPOSE_INDIR, --openpose_indir OPENPOSE_INDIR
                        Directory of openpose keypoints, e.g. json files.
  -io IMAGES_OUTDIR, --images_outdir IMAGES_OUTDIR
                        Directory to put predicted gender overlays. If not
                        given, wont produce any overlays.
  -oo OPENPOSE_OUTDIR, --openpose_outdir OPENPOSE_OUTDIR
                        Directory to put the openpose gendered keypoints. If
                        not given, it will augment the original openpose json
                        files.

```
As an example, inside the homogenus folder you can run the following to get the gender predictions for the sample images and their corresponding openpose keypoints.
This command will print the predictions as well as creating new gendered openpose keypoints and gender overlayed images.  

```bash
python3 -m homogenus.tf.homogenus_infer -ii ./samples/images/ -io ./samples/images_gendered/ -oi ./samples/openpose_keypoints/ -oo ./samples/openpose_keypoints_gendered/
```

## License

Free for non-commercial and scientific research purposes. By using this code, you acknowledge that you have read the license terms (https://smpl-x.is.tue.mpg.de/license), understand them, and agree to be bound by them. If you do not agree with these terms and conditions, you must not use the code. For commercial use please check the website (https://smpl-x.is.tue.mpg.de/license).

## Referencing SMPL-X

Please cite the following paper if you use this code directly or indirectly in your research/projects.
```
@inproceedings{SMPL-X:2019,
  title = {Expressive Body Capture: 3D Hands, Face, and Body from a Single Image},
  author = {Pavlakos, Georgios and Choutas, Vasileios and Ghorbani, Nima and Bolkart, Timo and Osman, Ahmed A. A. and Tzionas, Dimitrios and Black, Michael J.},
  booktitle = {Proceedings IEEE Conf. on Computer Vision and Pattern Recognition (CVPR)},
  year = {2019}
}
```

## Contact

If you have any questions you can contact us at smplx@tuebingen.mpg.de

## Acknowledgement

* We thank Benjamin Pellkofer and Jonathan Williams for helping with our [smpl-x project website](https://smpl-x.is.tue.mpg.de).