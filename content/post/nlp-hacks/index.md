---
title: Tools and Techniques for NLProc

# Summary for listings and search engines
summary: In this post I will list useful tools/libraries/techniques for text processing for various downstream ML/DL tasks.

# Link this post with a project
projects: []

# Date published
date: "2021-10-07T00:00:00Z"

# Date updated
date: "2021-10-07T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags: [troubleshooting, tricks, hacks, howtos. python, NLP, text-processing]


categories:
- How-to
---



### Need Text Cleaning? You Need This👇 

**Solution**: Install `clean-text` library (`pip install clean-text,pip install Unidecode`). Import library and then simply use `clean()`method to *clean* your text documents.

```python
from cleantext import clean

final = """
 Zürich has a famous website https://www.zuerich.com/ 
 WHICH ACCEPTS 40,000 € and adding a random string, :
 abc123def456ghi789zero0 for this demo. ' 
      """


clean(final,
    fix_unicode=True,               # fix various unicode errors
    to_ascii=True,                  # transliterate to closest ASCII representation
    lower=True,                     # lowercase text
    no_line_breaks=False,           # fully strip line breaks as opposed to only normalizing them
    no_urls=False,                  # replace all URLs with a special token
    no_emails=False,                # replace all email addresses with a special token
    no_phone_numbers=False,         # replace all phone numbers with a special token
    no_numbers=False,               # replace all numbers with a special token
    no_digits=False,                # replace all digits with a special token
    no_currency_symbols=False,      # replace all currency symbols with a special token
    no_punct=False,                 # remove punctuations
    replace_with_punct="",          # instead of removing punctuations you may replace them
    replace_with_url="<URL>",
    replace_with_email="<EMAIL>",
    replace_with_phone_number="<PHONE>",
    replace_with_number="<NUMBER>",
    replace_with_digit="0",
    replace_with_currency_symbol="<CUR>",
    lang="en"                       # set to 'de' for German special handling
)
```

###Sentence Tokenization

**Solution**: I find NLTK's `sent_tokenize()`more useful than Spacy's `doc.sents()`method.

```python
import nltk
from nltk.tokenize import sent_tokenize

strings = '''
As we can see we need to do some cleaning. We have some oddly named categories and I also checked for null values. From our data exploration, we have a few handy functions to clean the data we will use here again. For example, remove all digits, HTML strings and stopwords from our text and to lemmatise the words.
'''
list_of_sents = sent_tokenize(strings)
print(list_of_sents)
```



### Removing Control Characters (`\n\r\t`)

**Solution**: `clean` from `clean-text` library can easily take care of that. But if you prefer regex, here's how you can take care of it:

```python
import re
s = "We have some \n oddly \t named categories and I also checked \r for null values."
regex = re.compile(r'[\n\r\t]')
s = regex.sub(" ", s)
print(s)
```

