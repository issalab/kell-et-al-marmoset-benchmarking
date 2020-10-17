# kell-et-al-marmoset-benchmarking
This repository describes data and images used to benchmark marmosets, human, macaque, and rats. It corresponds to the preprint:

<p align="center"> <b>Conserved core visual object recognition across simian primates: <br> Marmoset image-by-image behavior mirrors that of humans and macaques</b></p>

<p align="center">by</p>

<p align="center"> <a href="http://www.alexkell.org">Alexander J.E. Kell</a>, Sophie L. Bokor, You-Nah Jeon, Tahereh Toosi, <a href="https://zuckermaninstitute.columbia.edu/elias-b-issa-phd">Elias B. Issa</a></p>

The data and images for the experiments (including the images used to train the animals) can be downloaded <a href="https://www.dropbox.com/sh/ro27d32o9rmd3m1/AABxXtZvSW40vHLEHHlU0t6Va?dl=0">here</a>. 

The structure of the data and image directories is briefly described with some code snippets. For further questions, please email: first.last@columbia.edu (where first and last are, respectively, "alex" and "kell").

<br/>

## Images and data for benchmarking marmoset with macaques and humans 

*Images originally employed in <a href="https://www.jneurosci.org/content/38/33/7255.short">Rajalingham et al., 2018</a>.*

![](https://www.dropbox.com/s/0bihfi0llr7j6iy/objectome_camel_3b9c0ce77203c956815755b6936d9f2a08772aa7_ty-0.69818_tz0.27398_rxy161.9692_rxz-143.9815_ryz163.001_s1.6173.png?raw=true) ![](https://www.dropbox.com/s/4gw78g9s799ye8o/objectome_wrench_2bd241b57de60b75eebfe0936dda2c26b369063b_ty0.043184_tz0.50711_rxy134.5441_rxz-160.7258_ryz131.2947_s0.72706.png?raw=true) ![](https://www.dropbox.com/s/aybu243idggtsmr/objectome_rhino_3f47f215207f7778b30e7657a51e3f356d57cf05_ty-0.34168_tz0.73404_rxy96.0619_rxz-68.7854_ryz111.0928_s1.5602.png?raw=true)

### Images
Images are in the directory `images-marmosetMacaqueHuman`, with a subdirectory for each of the four objects. The 400 images on which we compared marmosets with macaques and humans are in the `evaluation` subdirectory (e.g., `images-marmosetMacaqueHuman/wrench/evaluation`). We are also including the images used across the three stages of training (`token`, `training-low-variation`, and `training-high-variation`). The images used in the decision stage of the task, which the subjects touch to indicate their choice, are these same `token` images.

### Data
The data are pickled in Python. To load:

```python
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

"dva" denotes degrees of visual angle and `marmoset_sr2_pooledOverSize` is simply the sum of the data from two different image sizes `marmoset_sr2_22dva` and `marmoset_sr2_11dva`.

The data is arranged in a 5d array, the following indices: (subjects, days, target_object, distractor_object, image_idx). E.g.,
```python
arr_n_trials['marmoset_sr2_22dva'].shape == (5, 42, 4, 4, 100)
```

The data for `marmoset_sr2_pooledOverSize` and `macaque_mts24_from_rajalinghamEtAl` are pooled over subjects. Objects are in the order: `['camel', 'rhino', 'leg', 'wrench']`.

<br/>

## Images and data for benchmarking marmoset with rats

*Images originally employed in <a href="https://www.pnas.org/content/106/21/8748">Zoccolan et al., 2009</a>.*

![](https://www.dropbox.com/s/2qsjmzmesv5daqm/objectome_blob_e600cc291cb9f7227091183c95297153ddf9c856320c9906e8413640_N1_ty-10.0000_tz-10.0000_rxy0.0000_rxz60.0000_ryz0.0000_s30.0000.png?raw=true) ![](https://www.dropbox.com/s/0huszfp6abxbchh/objectome_blob_a1fca6246cdec0805476d9881060671d65994fca7f846140c78eeb43_N2_ty-10.0000_tz-10.0000_rxy0.0000_rxz60.0000_ryz0.0000_s30.0000.png?raw=true)

### Images 
Images are in subdirectories for each of the two stimuli `one-blob` and `two-blob`. The original 14 training images for each object are in the `original-training` subdirectory; all 54 images are in the `all-images` subdirectory.


### Data
To load:

```python
tmp = pickle.load(open('marmoset_and_rat.pkl','rb'))
```

The variable `tmp` is simply a dictionary with the matrices of rat and marmoset data as plotted in Figure 3 in Kell et al.: `rat_proportion_correct` and `marmoset_proportion_correct`. 
