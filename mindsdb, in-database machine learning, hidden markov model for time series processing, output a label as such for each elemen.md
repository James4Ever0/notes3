---
title: 'mindsdb, in-database machine learning, hidden markov model for time series processing, output a label as such for each element in the time series'
created: '2022-09-17T08:09:19.437Z'
modified: '2022-09-17T11:00:11.031Z'
---

# mindsdb, in-database machine learning, hidden markov model for time series processing, output a label as such for each element in the time series

## MindsDB

[documentation](https://docs.mindsdb.com/)

warning: this thing could break your dependencies. better use docker instead.
```bash
docker pull mindsdb/mindsdb
# pip3 install mindsdb
```

## HMMLearn (unsupervised)

most useful feature:
training and inferring the hidden states

## supervised hmm learning

### seqlearn

### pomegranate (both supervised and unsupervised)

While [probability Distributions](https://pomegranate.readthedocs.io/en/latest/Distributions.html#) are frequently used as components of more complex models such as mixtures and hidden Markov models, they can also be used by themselves. Many data science tasks require fitting a distribution to data or generating samples under a distribution. pomegranate has a large library of both univariate and multivariate distributions which can be used with an intuitive interface.

[General Mixture Models](https://pomegranate.readthedocs.io/en/latest/GeneralMixtureModel.html) (GMMs) are an unsupervised probabilistic model composed of multiple distributions (commonly referred to as components) and corresponding weights. This allows you to model more complex distributions corresponding to a singular underlying phenomena. For a full tutorial on what a mixture model is and how to use them, see the above tutorial.

[]
