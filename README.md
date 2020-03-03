# IDCE302_FinalProject
Name: Julia Wagner
Date: March 3, 2020
Python version 3.7

# Purpose
This script is a natural langugage processer for Wikipedia webpages. It includes downloading relevant libraries in NLTK (natural language toolkit) and Beautiful Soup to scrape and process the html text. The script tokenizes the scraped text and cleans it of stopwords using the NLTK package. The final product is a graph counting the frequency of meaningful words in the webpage text.
This script was developed based on a blog post by Raheel Shaikh. You can access it here: https://towardsdatascience.com/gentle-start-to-natural-language-processing-using-python-6e46c07addf3 

# Explanation of Code
First, we import the NLTK library. 
```
import nltk
nltk.download('stopwords')
```
Next, we create a website crawler that scrapes text from a Wikipedia page.
```
import urllib.request 
response =  urllib.request.urlopen('https://en.wikipedia.org/wiki/Hadwen_Arboretum')
html = response.read()
print(html)
```
Use Beautiful Soup to pull data out of html and xml files. Clean the data.
```
from bs4 import BeautifulSoup
soup = BeautifulSoup(html,'html5lib')
text = soup.get_text(strip = True) #this gets rid of all text that matches the html library
print(text)
```
Next, we convert the text into a list of tokens.
```
tokens = [t for t in text.split()]
print(tokens)
```
Finally, clean the text tokens of stop words like 'a', 'at', 'the', and 'for' using the stopwords function from the NLTK library. Count the word frequence and create a frequency plot. 
```
from nltk.corpus import stopwords
sr= stopwords.words('english') 
clean_tokens = tokens[:] #create a dictionary
for token in tokens:
    if token in stopwords.words('english'):
        
        clean_tokens.remove(token) 
freq = nltk.FreqDist(clean_tokens) 
for key,val in freq.items():
    print(str(key) + ':' + str(val))
freq.plot(20, cumulative=False) \
```

# Issues
In the future, I would like to develop this code to crawl and scrape Google Maps pages for parks so that I can read the words that are most associted with park properties. I tried to use this particular script to read Google Maps pages, but my output included a lot of words describing the page font and components. I would like tips on cleaning up the crawler to just read the comment text on Gooogle Maps. Issue requests are welcome!!

# Findings 
This particular script scrapes a Wikipedia page for Hadwen Arboretum in Worcester, MA, USA. It is a small, urban arboretum located in the city limits of Worcester, MA. The arboretum is owned and managed by Clark University, but is open to the public. Students and professors at Clark University are developing urban forest management practices. 
The output of the code demonstrates how aside from the name of the property, "Clark" and "species" are other commonly used words in the Wikipedia page. This makes sense as the arboretum is closely related to Clark University via ownership and management. It is likely that species is used to refer to the types of trees on the property. It is known as a diverse urban arboretum.

