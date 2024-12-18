# DeepMerge

Code repository for the paper "DeepMerge: Classifying High-redshift Merging Galaxies with Deep Neural Networks", A. Ćiprijanovića, G.F. Snyder, B. Nord, J.E.G. Peek, Astronomy & Computing, submitted


### Abstract

We investigate and demonstrate the use of convolutional neural networks (CNNs) for the task of distinguishing between merging and non-merging galaxies in simulated images, and for the first time at high redshifts (i.e.,  z=2).
We extract images of merging and non-merging galaxies from the Illustris-1 cosmological simulation and apply observational and experimental noise that mimics that from the Hubble Space Telescope; the data without noise form a pristine data set and that with noise form a noisy data set.
The classification accuracy of the CNN is 76% for pristine and 79% for noisy. 
The CNN outperforms a Random Forest classifier, which was shown to be superior to conventional one- or two-dimensional statistical methods (Concentration, Asymmetry, the Gini, M_20 statistics etc.), which are commonly used when classifying merging galaxies.
We also investigate the selection effects of the classifier with respect to merger state and star formation rate, finding no bias.
Finally, we extract saliency maps from the results to further assess and interrogate the fidelity of the classification model.

### Architecture
![](images/arch.png)
DeepMerge has 3 convolutional layers (with 3 pooling layers) and 3 dense layers, added after flattening. It also has dropout after each convolutional layer, as well as weight regularization in the first two dense layers.

### Prepare Datasets
Images used can be found at https://doi.org/10.17909/t9-vqk6-pc80. Pristine and noisy images used in the paper can be found in pristine_2filt_X.npy and noisy_2filt_X.npy, respectively (label files: pristine_2filt_y.npy and noisy_2filt_y.npy). Images we use have 2 filters (they mimic those available onboard the Hubble Space Telescope). For use with more complex neural networks we also have 3-filter files available (pristine_X.npy, noisy_X.npy and pristine_y.npy, noisy_y.npy)

### Training
Training is performed with early stopping (with validation loss being monitored). To run training and plot training and classification diagnostics use DeepMerge.ipynb and DeepMerge.ipynb files. 
![](images/training.png)

### Galaxy properties
You can also use DeepMerge.ipynb and DeepMerge.ipynb files to plot information about galaxy morphology and physical properties, which is also available for our images - concentration, M20 and stellar mass (there are other parameters available to be extracted from the catalogue we use - illustris_morphs_rf.txt).

### Gradient-weighted Class Activation Maps (Grad-CAMs)
Grad-CAMs show which pixels of the image were the most important for the classification into a particular class. This is important as a sanity check when using neural networks, but it can also show how different architectures "look" at images differently when doing the same classification. It is also important if we want to track how additional noise or image resizing impacts decidion making of our neural network. For example, DeepMerge trained on pristine and noisy images looks at different regions of the same galaxy for the classification (see image below).
![](images/gradcam.png)

### Requirements
Code was developed using Python 3.7.4. The requirements.txt file should list all Python libraries that your notebooks depend on, and they can be installed using:
```
pip install -r requirements.txt
```


### Authors
- Aleksandra Ćiprijanović
- Brian Nord
- Gregory Snyder
- Joshua Peek

### References
If you use this code, please cite our paper:
```bibtex
@ARTICLE{2020A&C....3200390C,
       author = {{{\'C}iprijanovi{\'c}}, A. and {Snyder}, G.~F. and {Nord}, B. and {Peek}, J.~E.~G.},
        title = "{DeepMerge: Classifying high-redshift merging galaxies with deep neural networks}",
      journal = {Astronomy and Computing},
     keywords = {Merging galaxies, Cosmology, Deep learning, Convolutional neural networks, Astrophysics - Astrophysics of Galaxies, Astrophysics - Instrumentation and Methods for Astrophysics, Computer Science - Computer Vision and Pattern Recognition},
         year = 2020,
        month = jul,
       volume = {32},
          eid = {100390},
        pages = {100390},
          doi = {10.1016/j.ascom.2020.100390},
archivePrefix = {arXiv},
       eprint = {2004.11981},
 primaryClass = {astro-ph.GA},
       adsurl = {https://ui.adsabs.harvard.edu/abs/2020A&C....3200390C},
      adsnote = {Provided by the SAO/NASA Astrophysics Data System}
}
```
