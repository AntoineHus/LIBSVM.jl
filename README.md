LIBSVM.jl
=========

[![Build Status](https://travis-ci.org/AntoineHus/LIBSVM.jl.svg?branch=master)](https://travis-ci.org/AntoineHus/LIBSVM.jl)


Julia bindings for [LIBSVM](http://www.csie.ntu.edu.tw/~cjlin/libsvm/)

### Stable release [![Github release](https://img.shields.io/github/release/LIBSVM/LIBSVM.jl.svg)](https://github.com/simonster/LIBSVM.jl/releases/latest)

## Usage

```julia
using RDatasets, LIBSVM

# Load Fisher's classic iris data
iris = dataset("datasets", "iris")

# LIBSVM handles multi-class data automatically using a one-against-one strategy
labels = iris[:Species]

# First dimension of input data is features; second is instances
instances = array(iris[:, 1:4])'

# Train SVM on half of the data using default parameters. See the svmtrain
# function in LIBSVM.jl for optional parameter settings.
model = svmtrain(labels[1:2:end], instances[:, 1:2:end]);

# Test model on the other half of the data.
(predicted_labels, decision_values) = svmpredict(model, instances[:, 2:2:end]);

# Compute accuracy
@printf "Accuracy: %.2f%%\n" mean((predicted_labels .== labels[2:2:end]))*100
```


* [**Issues**](https://github.com/simonster/LIBSVM.jl/issues/new)

## Credits

Created by Simon Kornblith

[LIBSVM](http://www.csie.ntu.edu.tw/~cjlin/libsvm/) by Chih-Chung Chang and Chih-Jen Lin
