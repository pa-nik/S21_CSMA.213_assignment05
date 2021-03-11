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

**Q5.** [2 points] Using `bag_of_words` as input, create a Pandas dataframe `df` that contains the BOW feature matrix as row data and feature names as column headers.  Print the head of df.

