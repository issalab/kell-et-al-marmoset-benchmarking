# kell-et-al-marmoset-benchmarking
Repository describing data and images used to benchmark marmosets, human, macaque, and rats.

The data described below and the images for the experiments can be downloaded <a href="https://www.dropbox.com/sh/ro27d32o9rmd3m1/AABxXtZvSW40vHLEHHlU0t6Va?dl=0">here</a>.

From the preprint: 

**"Conserved core visual object recognition across simian primates: Marmoset image-by-image behavior mirrors that of humans and macaques" 
by Alexander J.E. Kell, Sophie L. Bokor, You-Nah Jeon, Tahereh Toosi, Elias B. Issa**

Below, the structure is briefly described with some code snippets. For further questions, please email: first.last@columbia.edu (where first and last are, respectively, "alex" and "kell").

<br/>

## Images and data for benchmarking marmoset with macaques and humans 

*Images originally employed in <a href="https://www.jneurosci.org/content/38/33/7255.short">Rajalingham et al., 2018</a>.*

### Images
Images are in the directory `images-marmosetMacaqueHuman`, with a subdirectory for each of the four objects. The 400 images on which we compared marmosets with macaques and humans are in the `evaluation` subdirectory (e.g., `images-marmosetMacaqueHuman/wrench/evaluation`). We are also including the images used across the three stages of training (respectively: `token`, `training-low-variation`, and `training-high-variation`). Note that images used in the decision stage of the task are also the same `token` images.

### Data
The data are pickled in Python. To load:

```python
import numpy as np
import pickle

tmp = pickle.load(open('marmoset_macaque_and_human.pkl','rb'))
arr_n_trials, arr_n_correct, all_fnames = tmp['arr_n_trials'], tmp['arr_n_correct'], tmp['all_fns']
```

<br/>

`all_fnames` is a dictionary where each key is an object and each value is a list of the image filenames, in the order that they are indexed in the data arrays below. I.e.,

```python
[(k,len(all_fnames[k])) for k in all_fnames.keys()] == [('camel', 100), ('leg', 100), ('wrench', 100), ('rhino', 100)]
```

<br/>

`arr_n_trials` and `arr_n_correct` are dictionaries with values that are numpy arrays of, respectively, the number of trials and number of correct trials. 

The keys are as follows: 
```python
['human_sr2', 'marmoset_sr2_22dva', 'marmoset_sr2_11dva', 'marmoset_sr2_pooledOverSize', 'macaque_mts24_from_rajalinghamEtAl']
```

"dva" is short for degrees of visual angle and `marmoset_sr2_pooledOverSize` is simply the sum of the data from two different image sizes `marmoset_sr2_22dva` and `marmoset_sr2_11dva`.

The data is arranged in a 5d array, the following indices: (subjects, days, target_object, distractor_object, image_idx). E.g.,
```python
arr_n_trials['marmoset_sr2_22dva'].shape==(5, 42, 4, 4, 100)
```

The data for `marmoset_sr2_pooledOverSize` and `macaque_mts24_from_rajalinghamEtAl` are pooled over subjects. Objects are in the order: `['camel', 'rhino', 'leg', 'wrench']`.

<br/>

## Images and data for benchmarking marmoset with rats

*Images originally employed in <a href="https://www.pnas.org/content/106/21/8748">Zoccolan et al., 2009</a>.*

### Images 
Images are in subdirectories for each of the two stimuli `one-blob` and `two-blob`. The original 14 training images for each object are in the `original-training` subdirectory; all 54 images are in the `all-images` subdirectory.


### Data
To load:

```python
tmp = pickle.load(open('marmoset_and_rat.pkl','rb'))
```

The variable `tmp` is simply a dictionary with the matrices of rat and marmoset data as plotted in Figure 3 in Kell et al. -- respectively, `rat_proportion_correct` and `marmoset_proportion_correct`. 
