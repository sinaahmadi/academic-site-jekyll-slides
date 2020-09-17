---
title: Word Sense Alignment as a Classification Problem
description: 
theme: white
---


## Outline

### Context
### Objectives
### Methodology
### Datasets description
### Prelimenary results

---

### Context

<blockquote>
  <p>&ldquo; Dictionaries are treasure houses of data on the uses of words. They are also our best starting point for all questions regarding word sense distinctions, in NLP, the humanities or lexicography. But to reveal the dictionary's treasures in a systematic way is no simple.&rdquo;</p>
  <footer>— <a href="https://www.jstor.org/stable/30204631"> Adam Kilgarriff (Dictionary Word Sense Distinctions: An Enquiry into Their Nature)</a></footer>
</blockquote>



~~

#### Word senses
- Words have different meanings, i.e. *senses*
- Senses may be differently described in various resources:
	- dictionaries
	- encyclopedia
	- thesauri
	- WordNets

**Word sense alignment** ➡ linking senses across resources


~~

`entire` (adjective)

<p style="text-align:center;"><img src="../../imgs/entire_lemma.png" alt="entire adjective"  width="800"></p>

---

### Objectives

<p class="fragment">1. What are the relevant features that can be used for WSA? ➡ Manual extraction of features</p>
<p class="fragment">2. How representation learning can help in improving the results? ➡ Restricted Boltzmann machine</p>
<p class="fragment">3. Use the features for classifying semantic relationship between two given senses ➡ <q>exact</q>, <q>narrower</q>, <q>broader</q>, <q>related</q>, <q>none</q>  </p>

---

### Methodology

1. Feature extraction
2. Data augmentation:
	- symmetric relationships: `exact`, `related`
	- asymmetric relationships: `narrower`, `broader`
3. Representation learning
4. Classification: `SVM`, `Logistic regression`, etc.

~~ 

#### Feature extraction

<p style="text-align:center;"><img src="../../imgs/wsa_features.png" alt="WSA features"  height="500"></p>

- Incorporate **ConceptNet** ([https://conceptnet.io/](https://conceptnet.io/))

~~

##### Some instances


<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vS7Jc31ADjOb6_nLl-hm28JHCF-_fBU8RdKeXsjz7DMzrTys4WM8hcFHuR3NSpeWhb6xJAZ2_L94nPp/pubhtml?gid=1103311453&amp;single=true&amp;widget=true&amp;headers=true"  style="width: 100%; height: 60vh;"></iframe>


~~ 

#### Data augmentation
➡ Collecting new data instances by inverting sense order

Example: *observer*

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vS7Jc31ADjOb6_nLl-hm28JHCF-_fBU8RdKeXsjz7DMzrTys4WM8hcFHuR3NSpeWhb6xJAZ2_L94nPp/pubhtml?gid=1160046339&amp;single=true&amp;widget=true&amp;headers=true"  style="width: 100%; height: 30vh;"></iframe>

~~

#### Representation learning

Using a Restricted Boltzmann machine, map the extracted features (visible) to a set of hidden ones.


<p style="text-align:center;"><img src="../../imgs/rbm.png" alt="RBM"  height="300"></p>

---

### Preliminary results


<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vRAj6QkHULaAGvikiKuEhRTpCLlePkZQzgiy8NGzMXlRMz4oCJieaKyrPdpp2IAb1VmPuMgfEDIahhS/pubhtml?gid=217917983&amp;single=true&amp;widget=true&amp;headers=true"  style="width: 100%; height: 60vh;"></iframe>

---

### Next steps

- Complete experiments on datasets in other languages using the current approach
- How neural networks and deep learning can improve the current results?

---
## Thanks!

Any questions? 🙂