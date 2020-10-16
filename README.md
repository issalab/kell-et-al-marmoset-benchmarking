# kell-et-al-marmoset-benchmarking
Behavioral data and images used to benchmark marmosets, human, macaque, and rats. 

From the preprint: 

**"Conserved core visual object recognition across simian primates: Marmoset image-by-image behavior mirrors that of humans and macaques" 
by Alexander J.E. Kell, Sophie L. Bokor, You-Nah Jeon, Tahereh Toosi, Elias B. Issa**

Below, the structure is briefly described with some code snippets. For further questions, please email: first.last@columbia.edu (where first and last are, respectively, "alex" and "kell").



## Data for benchmarking marmoset with macaques and humans 

Image-by-image behavioral data on discrimination task on images originally employed in <a href="https://www.jneurosci.org/content/38/33/7255.short">Rajalingham et al., 2018</a>.

The data are pickled in Python. To load:

```python
import numpy as np
import pickle

tmp = pickle.load(open('marmoset_macaque_and_human.pkl','rb'))
arr_n_trials, arr_n_correct = tmp['arr_n_trials'], tmp['arr_n_correct']
```

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

## Data for benchmarking marmoset with rats

Image-by-image behavioral data on discrimination task on images originally employed in <a href="https://www.pnas.org/content/106/21/8748">Zoccolan et al., 2009</a>.

To load:

```python
tmp = pickle.load(open('marmoset_and_rat.pkl','rb'))
```

The variable is simply a dictionary with the matrices of rat and marmoset data as plotted in Figure 3 in Kell et al -- respectively, `rat_proportion_correct` and `marmoset_proportion_correct`. 
