### S21_CSMA.213 assignment05

In this assignment you will apply a variety of Natural Language Processing (NLP) techniques, using a plain text version of *Alice’s Adventures in Wonderland* by Lewis Carroll as input.

Please refer to PDF files available on Discord, *Artificial Intelligence with Python*, Ch. 10 (pp. 248-263) and *Applied Text Analysis with Python*, Ch. 4 (pp. 55-64), for help and code samples dealing with specific NLP topics covered in this assignment.

To get started, you will need to read the included file `alice_in_wonderland.txt`.  The code snippet below shows how to read the file and store in into a variable `alice_text`. Create a Python file or Jupyter notebook cell to run this code and make sure you see the correct directory, file path and file output of the first few sentences printed.

```python

import os

cd = os.getcwd()
print("cd: ", cd)
filepath = os.path.join(cd, 'alice_in_wonderland.txt')
print("filepath: ", filepath)

#  Read text file
file = open(filepath, "r", encoding="utf8")
alice_text = file.read()

# Replace escape character with space
alice_text = alice_text.replace("\n", " ")

# Make all the text lowercase
alice_text = alice_text.lower()

print(alice_text[:885])

```

**Q1.** [1 point] Create an array `tokenized_sentences` containing `alice_text` data run through Natural Language Toolkit's (NLTK) sentence tokenizer.  

Print out the sentence at index 1 of the array. Then, create another array `tokenized_words` containing word tokenizer output of the sentence above and print it out.  Don’t forget to include the following at the top of your code:

```python
from nltk.tokenize import sent_tokenize, word_tokenize
```

**Q2.** [1 point] Using WordNetLemmatizer available in NLTK, create and print an array `lemmatized_words` containing lemmatized output of tokenized_words.

You can use the verb lemmatizer specified with argument `pos='v'` in `lemmatize()` function.  Start with:

```python
nltk.stem import WordNetLemmatizer
```

**Q3.** [1 point] Create and print an array `tagged_words` containing tagged parts of speech for `tokenized_words`, using the `pos_tag` module:

```python
from nltk import pos_tag
```

**Q4.** [1 point] Create an array titled `bag_of_words` that represents the  'bag of words' (BOW) derived from `tokenized_words`. 

Print the list of feature names and feature matrix contained in `bag_of_words`.  Include CountVectorizer module: 

```python
from sklearn.feature_extraction.text import CountVectorizer
```

**Q5.** [1 points] Using `bag_of_words` as input, create a Pandas dataframe `df` that contains the BOW feature matrix as row data and feature names as column headers.  Print the head of `df`.

**Q6.** [2 points] Create `tfidf` object containing Term Frequency - Inverse Document Frequency (TF-IDF) with 5 maximum `features` and `stop_words` arguments:

```python
from sklearn.feature_extraction.text import TfidfVectorizer
tfidf = TfidfVectorizer(max_features=5, stop_words='english')
```

Using first 20 items of tokenized_sentences as a corpus, extract TF-IDF of the data into `tfidf` and print the resulting feature names.  Try running the code without the stop word argument and compare the results. Explain the difference you observe in the outputs (one paragraph description in your own words).

**Q7.** [3 points] For this question, you’re going to build a Word2Vec vector representation of the data in the story.  To do that, create a new 2D array `alice_data` that contains all tokenized sentences and words. The array should be structured so that to access sentence index `si` and word index `wj` you would call: `alice_data[si][wj]`

For example, the output of of `alice_data[2][0]` would be 'there' and `alice_data[2]` would be:
```
['there', 'was', 'nothing', 'so', 'very', 'remarkable', 'in', 'that', ';', 'nor', 'did', 'alice', 'think', 'it', 'so', 'very', 'much', 'out', 'of', 'the', 'way', 'to', 'hear', 'the', 'rabbit', 'say', 'to', 'itself', ',', '‘', 'oh', 'dear', '!']
```

Next, create a Word2Vec model of `alice_data` with the following parameters:

```python
import gensim
model = gensim.models.Word2Vec(alice_data, min_count=1, size = 100, window = 5)
```

You should now be able to call `model.similarity()` function between any two words in the story, such as: `model.similarity('alice', 'wonderland')`

The computed similarity between these words is high (>0.99).  Explain what this means (one sentence in your own words), then try to find words in the text that will have substantially lower similarity score.  List at least 3 words pairs that have similarity below 0.90. Can you find any below 0.80? 

 