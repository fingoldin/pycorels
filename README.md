# Pycorels

Welcome to the python binding of the Certifiably Optimal RulE ListS (CORELS) algorithm!

## Overview

CORELS (Certifiably Optimal RulE ListS) is a custom discrete optimization technique for building rule lists over a categorical feature space. Using algorithmic bounds and efficient data structures, our approach produces optimal rule lists on practical problems in seconds.

The CORELS pipeline is simple. Given a dataset matrix of size `n_samples x n_features` and a labels vector of size `n_samples`, it will compute a rulelist (similar to a series of if-then statements) to predict the labels with the highest accuracy.

Here's an example:
![Whoops! The image failed to load](https://raw.githubusercontent.com/fingoldin/pycorels/master/utils/Corels.png)

More information about the algorithm [can be found here](https://corels.eecs.harvard.edu/corels)

## Dependencies

CORELS uses [Python](https://www.python.org), [Numpy](https://www.numpy.org), and [GMP](https://gmplib.org).
GMP (GNU Multiple Precision library) is not required, but it is *highly recommended*, as it improves performance. If it is not installed, CORELS will run slower.

## Installation

CORELS exists on PyPI, and can be downloaded with
`pip install corels`

To install from this repo, simply run `pip install .` or `python setup.py install` from the `corels` directory.

#### Linux
~~~~
sudo apt install libgmp-dev
pip install corels
~~~~

#### Mac
~~~~
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install gmp
pip install corels
~~~~

#### Windows
~~~~
pip install corels
~~~~

## Documentation

The docs for this package are hosted on [our website](https://corels.eecs.harvard.edu/corels/pycorels/)

## Examples

### Large dataset, loaded from [this file](https://raw.githubusercontent.com/fingoldin/pycorels/master/examples/data/compas.csv)
~~~~
from corels import *

# Load the dataset
X, y = load_from_csv("data/compas.csv")

# Create the model, with 10000 as the maximum number of iterations 
c = CorelsClassifier(n_iter=10000)

# Fit, and score the model on the training set
a = c.fit(X, y).score(X, y)

# Print the model's accuracy on the training set
print(a)
~~~~

### Toy dataset (See picture example above)
~~~~
from corels import CorelsClassifier

# ["loud", "samples"] is the most verbose setting possible
C = CorelsClassifier(max_card=2, c=0.0, verbosity=["loud", "samples"])

# 4 samples, 3 features
X = [[1, 0, 1], [0, 0, 0], [1, 1, 0], [0, 1, 0]]
y = [1, 0, 0, 1]
# Feature names
features = ["Mac User", "Likes Pie", "Age < 20"]

# Fit the model
C.fit(X, y, features=features, prediction_name="Has a dirty computer")

# Print the resulting rulelist
print(C.rl())

# Predict on the training set
print(C.predict(X))
~~~~



### Questions?
Email the maintainer at: vassilioskaxiras@gmail.com
