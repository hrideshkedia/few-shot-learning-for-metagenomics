# Few Shot Learning -- Learning to Classify Diseases from a few Microbiome Samples

A [recent study](https://pubmed.ncbi.nlm.nih.gov/27400279/) from the [Segata Lab](http://segatalab.cibio.unitn.it/) analyzes human microbiome data obtained using shotgun metagenomic analysis.

"Shotgun metagenomic analysis of the human associated microbiome provides a rich set of microbial features for prediction and biomarker discovery in the context of human diseases and health conditions. However, the use of such high-resolution microbial features presents new challenges, and validated computational tools for learning tasks are lacking."

The dataset used in the study is available freely at [MetAML - Metagenomic prediction Analysis based on Machine Learning](https://github.com/SegataLab/metaml) and on [kaggle](https://www.kaggle.com/antaresnyc/metagenomics). 

The dataset gives abundances of different microbial species present in microbiome samples from healthy people and patients  with a variety of different diseases. The goal of the above mentioned study was to correctly predict whether a patient had a given disease or was healthy from the species abundance data for the patient's microbiome sample, after training on healthy samples and samples from patients with the given disease. 

In a practical setting, one may not have access to many samples from patients with a given disease and would want to be able to predict from a patient's microbiome data whether they have one of two possible diseases given only a few labeled examples for each of the two diseases. This problem belongs to a class of problems known as "Few-shot learning" studied in the Machine Learning Literature.

Our goal will be train a model to classify a given microbiome sample as having one of two previously unseen diseases (not present in the training set), from only a few labeled examples for each of the two diseases. I use a recent elegant and general algorithm known as [Model Agnostic Meta-Learning algorithm](https://arxiv.org/abs/1703.03400) to learn to classify the species abundance data into two unseen disease classes, given only 3 labeled examples, i.e. the 3-shot 2-way classification task. 

In the following, I classify species abundance samples into 'Obesity' vs 'Type 2 Diabetes' given only 3 labeled examples for each, and by training on the data for the remaining diseases. Guided by the performance comparison of different model architechtures on a similar task [studied here](https://www.nature.com/articles/s41598-019-46649-z), I use a single hidden layer Multi-Layer Perceptron with 128 neurons.

I use the idea of derivative-order annealing from the paper ["How to train your MAML"](https://arxiv.org/abs/1810.09502), and use first-order MAML for the first 20% of the epochs and use second-order MAML for the rest. 

The model achieves an impressive performance comparable to the best previous results on this dataset, with an accuracy (> 80 %), an F1 score (> 0.8), an ROC AUC score (> 0.8), and a Confusion Matrix ~((8x, x),(x, 8x)).

It is worth noting that the validation and training data in this case have no disease classes in common, and that both are balanced, i.e. have equal numbers of samples for each disease.

Different seed choices lead to different choices of diseases for testing. 

I build on the previous notebooks using this [metagenomics dataset](https://www.kaggle.com/antaresnyc/metagenomics): 
* [sklasfeld/starter-metagenomics](https://www.kaggle.com/sklasfeld/starter-metagenomics)
* [antaresnyc/cirrhosis-classification/notebook](https://www.kaggle.com/antaresnyc/cirrhosis-classification/notebook)
* [tmathieu/feature-selection-to-predict-diabetes](https://www.kaggle.com/tmathieu/feature-selection-to-predict-diabetes)

I closely follow the excellent [MAML implementation by Oscar Knagg](https://github.com/oscarknagg/few-shot) and the Perceptron implementation [described here](https://colab.research.google.com/github/bentrevett/pytorch-image-classification/blob/master/1_mlp.ipynb#scrollTo=C6gprB1sO7fy).

This notebook is also available on [kaggle here](https://www.kaggle.com/hrideshkedia/few-shot-learning-for-metagenomics).
