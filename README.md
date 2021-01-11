# Arabic Automatic Video Captioning

This repository utilizes the [Dense Video Captioning with Bi-modal Transformer (BMT) architecture](https://github.com/v-iashin/BMT) to produce automatic captions for videos (more can be read about it [here](https://towardsdatascience.com/dense-video-captioning-using-pytorch-392ca0d6971a) but that article has a slightly different implementation than this repository). These captions are then stored in a text file and utilized in the `Arabic_video_captioning.ipynb` notebook to produce the Arabic versions of the generated captions, and overlay them on the video for which they were generated.

# Caption Generation with BMT

The notebooks `I3D_generation.ipynb`, `VGGish_generation.ipynb`, and `Run_captioning.ipynb` can be used to generate captions for your desired video without need for the terminal. Because BMT (and these notebook implementations of BMT) require an NVIDIA GPU, I ran these on Google Colab. Make sure to connect to a GPU runtime on Colab before running these notebooks.

**The biggest issues I faced when trying to use BMT were dependencies and disk space:**
- At the time of writing this, I managed to get the appropriate dependencies (and their corresponding versions) set up in the notebooks listed above. If you face issues with them, you may need to play around with dependency versions to get everything to work.
- Regarding disk space, I had to split up BMT into 3 separate notebooks since I was kept running out of disk space when running them all together under the same GPU runtime.
- You may want to run this on videos of ~10 seconds due to disk space limitations in Google Colab.

**BMT Performance:**
- For me, I found that BMT worked best on videos with a steady camera, 1 main thing happening in the video, and little clutter/noise in the background. However, you might have more luck with other types of videos.

### `I3D_generation.ipynb` & `VGGish_generation.ipynb`

These notebooks generate the features to be used as input to the BMT model for the video in question. `I3D_generation.ipynb` will generate flow and rgb npy files (the visual features of the video), and `VGGish_generation.ipynb` will generate vggish npy file (the audio features of the video).

These notebooks use [this implementation](https://github.com/v-iashin/video_features) rather than what's described in the BMT repository (this is just a sub-module of the BMT repository) to generate the features. Both repositories are made by the same person.

**Please note that the `VGGish_generation.ipynb` notebook will require a pretrained model called vggish_model.ckpt, which is ~300MB. Details are listed in the notebook.**

### `Run_captioning.ipynb`

This notebook takes the npy files generated from the other 2 notebooks and uses them to generate captions for the video. It will generate a text file containing those captions, which you can then use in the `Arabic_video_captioning.ipynb` notebook to overlay on the video. Details are listed in the notebook.

# Generating Arabic Captions & Overlaying on Original Video

**DISCLAIMER:** This notebook was run on my desktop (MacOS) since it had dependencies that couldn't be installed on Google Colab.

Using the `Arabic_video_captioning.ipynb`, you can generate Arabic captions for the video. **Disclaimer: I deleted some of the suggestions made by the BMT network since not all of them were relevant and some overlapped others. This notebook is similarly a semi-automated process.**

You will need to make sure that you have the [google translate python library](https://github.com/lushan88a/google_trans_new) installed as well as moviePy (instructions can be found [here](https://towardsdatascience.com/rendering-text-on-video-using-python-1c006519c0aa)).

Because moviePy depends on ImageMagick, you may need to install a ttf font that is compatible with Arabic text in order to overlay onto the video. I used this one called [Sahel](https://github.com/rastikerdar/sahel-font/blob/master/dist/Sahel.ttf), but there are plenty of others that are free online.
