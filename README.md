# System Requirements:

* Python 3 or later

# How To Setup Environment

* install all requirements using pip:
``pip install -r requirements.txt``
* download necessary data for nltk by 
``python -m textblob.download_corpora``

# Models Description

| Model Name                 | Description                                       | Naive Bayes Parameters                                                                                                          | SVM Parameters                                                                                                                                                                                                                                            | Knn Parameters                                                                                                                                                                                                                           |
|----------------------------|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *_unoptimized-model.pkl    | First try of algorithms. No optimization applied. | `{}`                                                                                                                            | `{}`                                                                                                                                                                                                                                                      | `{}`                                                                                                                                                                                                                                     |
| *_optimized-model.pkl      | Optimized models.                                 | `{,'tfidf__use_idf': (True, False),,'bow__analyzer': (splitToLemmas_NoStopWord, splitToLemmas, splitToTokens, 'word')}`         | `{'tfidf__use_idf': (True, False),'bow__analyzer': (splitToLemmas_NoStopWord, splitToLemmas, splitToTokens, 'word'),'classifier__C': [1, 10, 100, 1000],'classifier__gamma': ['auto', 0.001, 0.0001],'classifier__kernel': ['rbf', 'linear']}`            | `{,'tfidf__use_idf': (True, False),'bow__analyzer': (splitToLemmas_NoStopWord, splitToLemmas, splitToTokens, 'word'),'classifier__n_neighbors': numpy.arange(start=1, stop=100),'classifier__weights': ['uniform', 'distance']}`         |
| *_optimized-model-char.pkl | Optimized models. whit 'char' bow analyzer.       | `{,'tfidf__use_idf': (True, False),,'bow__analyzer': (splitToLemmas_NoStopWord, splitToLemmas, splitToTokens, 'word', 'char')}` | `{'tfidf__use_idf': (True, False),'bow__analyzer': (splitToLemmas_NoStopWord, splitToLemmas, splitToTokens, 'word', 'char'), 'classifier__C': [1, 10, 100, 1000], 'classifier__gamma': ['auto', 0.001, 0.0001], 'classifier__kernel': ['rbf', 'linear']}` | `{,'tfidf__use_idf': (True, False),'bow__analyzer': (splitToLemmas_NoStopWord, splitToLemmas, splitToTokens, 'word', 'char'),'classifier__n_neighbors': numpy.arange(start=1, stop=100),'classifier__weights': ['uniform', 'distance']}` |
| *_model.pkl                | Composition of models                             | nb_optimized-model                                                                                                              | svm_optimized-model-char                                                                                                                                                                                                                                  | knn_optimized-model                                                                                                                                                                                                                      |

# How to use

run script using terminal:

```bash
python3 source.py [-h] [-m MESSAGE] [-d] [-p POSTFIX]
```

# Available Options:

+ -h: 
    prints help message

+ -d, --detail:
    Show models details.

+ -m MESSAGE, --message MESSAGE:
    The message to be checked for Spam.

+ -p POSTFIX, --postfix POSTFIX
    Model file postfix, what will be after "algorithm name" and before ".pkl". 
    please note the under lines.(example: -p "_optimized-model-char")
    
## Usage Example:

You can remove `-d` for less detail.

```bash
$ python3 source.py -d -m "Text you want to test."

                      .
                      .
                      .
        (Models details here, solong)
                      .
                      .

	============ Final Result ============

Message:

Text you want to test.

	------------ ------------ ------------

Support Vector Machine:	 ham
Naive Bayes:		     ham
K Nearest Neighbor:	     ham

```