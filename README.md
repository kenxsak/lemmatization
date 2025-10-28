## EXPERIMENT NO. 3

### 1. AIM
Apply various lemmatization and stemming techniques on text. Demonstrate at least one stemming algorithm (e.g., Porter Stemmer) and one lemmatization technique (e.g., WordNet lemmatizer).

### 2. REQUIREMENTS (Software / Hardware)

Software:
- Python 3.x
- NLTK Library

Hardware:
- A system with minimum 2 GB RAM (or as required)

### 3. PROGRAM

Example program using PorterStemmer and WordNetLemmatizer:
```python
# Stemming and Lemmatization Example with NLTK

import nltk
from nltk.stem import PorterStemmer
from nltk.stem import WordNetLemmatizer

# Download required NLTK data (only once)
nltk.download('wordnet')
nltk.download('omw-1.4')  # optional language resources for lemmatizer
nltk.download('punkt')    # for tokenization if needed

ps = PorterStemmer()
wnl = WordNetLemmatizer()

text = "The striped bats are hanging on their feet for best running faster studies."
words = nltk.word_tokenize(text)

print("Original words:")
print(words)

# Apply Porter stemming
stemmed = [ps.stem(w) for w in words]
print("\nPorter Stemmer output:")
print(stemmed)

# Apply Lemmatization (default POS = noun)
lemmatized_noun = [wnl.lemmatize(w) for w in words]
print("\nLemmatized (default POS=noun):")
print(lemmatized_noun)

# Better lemmatization with POS tagging (example mapping nouns/verbs/adjectives)
from nltk import pos_tag
nltk.download('averaged_perceptron_tagger')
pos_tags = pos_tag(words)
print("\nPOS tags:")
print(pos_tags)

# Simple POS mapper to wordnet POS tags
def get_wordnet_pos(treebank_tag):
    if treebank_tag.startswith('J'):
        return 'a'  # adjective
    elif treebank_tag.startswith('V'):
        return 'v'  # verb
    elif treebank_tag.startswith('N'):
        return 'n'  # noun
    elif treebank_tag.startswith('R'):
        return 'r'  # adverb
    else:
        return 'n'  # default to noun

lemmatized_pos = [wnl.lemmatize(word, get_wordnet_pos(tag)) for word, tag in pos_tags]
print("\nLemmatized with POS:")
print(lemmatized_pos)
```

### 4. OUTPUT (example)
```
Original words:
['The', 'striped', 'bats', 'are', 'hanging', 'on', 'their', 'feet', 'for', 'best', 'running', 'faster', 'studies', '.']

Porter Stemmer output:
['the', 'stripe', 'bat', 'are', 'hang', 'on', 'their', 'feet', 'for', 'best', 'run', 'faster', 'studi', '.']

Lemmatized (default POS=noun):
['The', 'striped', 'bat', 'are', 'hanging', 'on', 'their', 'foot', 'for', 'best', 'running', 'faster', 'study', '.']

POS tags:
[('The', 'DT'), ('striped', 'JJ'), ('bats', 'NNS'), ('are', 'VBP'), ('hanging', 'VBG'),
 ('on', 'IN'), ('their', 'PRP$'), ('feet', 'NNS'), ('for', 'IN'), ('best', 'JJS'),
 ('running', 'VBG'), ('faster', 'RBR'), ('studies', 'NNS'), ('.', '.')]

Lemmatized with POS:
['The', 'striped', 'bat', 'be', 'hang', 'on', 'their', 'foot', 'for', 'best', 'run', 'fast', 'study', '.']
```

Notes on the example output:
- Porter stemming is aggressive and reduces words to a stem that is not necessarily a valid word ("studi" from "studies").
- Lemmatization with correct POS tags produces dictionary forms (lemmas), giving more readable outputs ("study", "run", "foot").

### 5. CONCLUSION
Stemming is a faster, rule-based process that chops word endings to reduce inflected words to a stem, which may not be a valid word. Lemmatization uses vocabulary and morphological analysis (and POS information) to return meaningful base forms (lemmas). For tasks where semantic correctness and real-word forms are important (e.g., information retrieval ranking or NLP pipelines requiring normalized forms), lemmatization is generally preferred. For lightweight text normalization where performance matters more than perfect lexical forms, stemming (e.g., Porter) can be acceptable.

### 6. QUESTIONS

Q1. What is the main difference between stemming and lemmatization in text processing?

Answer:
- Stemming: A heuristic, rule-based process that removes word affixes to reduce words to a base "stem"; stems may not be valid words. It is fast and suitable when approximate normalization is acceptable.
- Lemmatization: A dictionary- and morphology-based process that reduces words to their canonical lemma (real dictionary form) using POS context; it is more accurate but typically slower and requires linguistic resources.

Q2. Name one scenario where using a Porter Stemmer might be preferred over a Lancaster Stemmer.

Answer:
Use Porter Stemmer when you want a balanced, moderately aggressive stemming that preserves more intelligible stems (and is widely used in IR tasks). For example, in a search engine indexing pipeline where you need reasonable normalization while maintaining some readability and compatibility with existing tools, Porter is often preferred over the more aggressive Lancaster Stemmer which can over-stem and produce less interpretable stems.

---

## NOTES / USAGE

- To run the examples, install NLTK and download required data:
```bash
pip install nltk
```
Then inside Python:
```python
import nltk
nltk.download('brown')
nltk.download('treebank')
nltk.download('punkt')
nltk.download('wordnet')
nltk.download('omw-1.4')
nltk.download('averaged_perceptron_tagger')
```

- Use a virtual environment (venv/conda) to keep dependencies isolated.

---

## AUTHOR / CONTACT
Prepared by: kenxsak
