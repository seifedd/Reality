

```python
Idea by Jesse Steinweg-Woods
```

# Scraping Indeed.com 
#### data science skills


- We want to scrape the information from job advertisements for data scientists from indeed.com Let's scrape and find out! 
- What skills are in demand for data scientists?



```python
## all imports
from IPython.display import HTML
import numpy as np
import urllib.request as urllib2
import bs4 #this is beautiful soup
import time
import operator
import socket
import pickle
import re # regular expressions

from pandas import Series
import pandas as pd
from pandas import DataFrame

import matplotlib
import matplotlib.pyplot as plt
%matplotlib inline

# import seaborn as sns
# sns.set_context("talk")
# sns.set_style("white")

# from secret import *

```


```python
# Fixed url for job postings containing data scientist
url = 'http://www.indeed.com/jobs?q=data+scientist&l='
# read the website
source = urllib2.urlopen(url).read()
# parse html code
bs_tree = bs4.BeautifulSoup(source)



```


```python
# see how many job postings we found
job_count_string = bs_tree.find(id = 'searchCount').contents[0]


job_count_string=job_count_string.split()
job_count_string=[s.replace(',', '') for s in job_count_string ]


# not that job_count so far is still a string, 
# not an integer, and the , separator prevents 
# us from just casting it to int

job_count_digits = [int(d) for d in job_count_string if d.isdigit()]
print(job_count_digits)
job_count = np.sum([digit*(10**exponent) for digit, exponent in 
                    zip(job_count_digits[::-1], range(len(job_count_digits)))])

print("Search yielded %s hits." % (job_count))
```

    [1, 11064]
    Search yielded 11074 hits.
    

## Page after page


```python
# The website is only listing 10 results per page, 
# so we need to scrape them page after page
num_pages = int(np.ceil(job_count/10.0))
pages_where_to_stop=2;
base_url = 'http://www.indeed.com'
job_links = []
for i in range(pages_where_to_stop): #do range(num_pages) if you want them all
    
    if i%10==0:
        if i<10:
            print("remaining page num",pages_where_to_stop-i)
        else:
            print("remaining page num", pages_where_to_stop-i)
    url = 'http://www.indeed.com.au/jobs?q=data+scientist&start=' + str(i*10)
    html_page = urllib2.urlopen(url).read() 
    bs_tree = bs4.BeautifulSoup(html_page)
    
        
    job_link_area = bs_tree.find(id = 'resultsCol')
   
    
    job_postings = job_link_area.findAll("div")
    job_posting=[jp for jp in job_postings if   jp.get('class')=='jobsearch-SerpJobCard unifiedRow row result clickcard']
   
    job_ids = [jp.get('data-jk') for jp in job_postings if jp.get('data-jk') is not None]

 
    # go after each link
    for id in job_ids:
        job_links.append(base_url + '/rc/clk?jk=' + id)

    time.sleep(1)
    
print("We found a lot of jobs: ", len(job_links))
```

    remaining page num 2
    We found a lot of jobs:  20
    


## Some precautions to enable us to restart our search


```python
# Save the scraped links
with open('C:\\Users\\Seif\\OneDrive\\Documents\\cs209\\2015\\Lectures\\data\\scraped_links.pkl', 'wb') as f:
    pickle.dump(job_links, f)
    
# Read canned scraped links
with open('C:\\Users\\Seif\\OneDrive\\Documents\\cs209\\2015\\Lectures\\data\\scraped_links.pkl', 'rb') as f:
    job_links = pickle.load(f)
        
```

### Looking for skill set map reduce and Spark in job_links


```python
skill_set = {'mapreduce': 0, 'spark': 0}

# write initialization into a file, so we can restart later
with open('C:\\Users\\Seif\\OneDrive\\Documents\\cs209\\2015\\Lectures\\data\\scraped_links_restart.pkl', 'wb') as f:
   pickle.dump((skill_set, 0),f)    


```

This code below does the trick, but could be optimized for speed if necessary
e.g. skills are typically listed at the end of the webpage
might not need to split/join the whole webpage, as we already know
which words we are looking for 
and could stop after the first occurance of each word



```python

with open('C:\\Users\\Seif\\OneDrive\\Documents\\cs209\\2015\\Lectures\\data\\scraped_links_restart.pkl', 'rb') as f:
    skill_set, index = pickle.load(f)
    print(skill_set,index)
    print("How many websites still to go? ", len(job_links) - index)
```

    {'mapreduce': 0, 'spark': 0} 0
    How many websites still to go?  20
    


```python
counter = 0

for link in job_links[index:]:
    print(link)
    counter +=1  
    
    try:
        html_page = urllib2.urlopen(link).read()
    except urllib2.HTTPError:
        print("HTTPError:")
        continue
    except urllib2.URLError:
        print( "URLError:")
        continue
    except socket.error as error:
        print( "Connection closed")
        continue

    html_text = re.sub("[^a-z.+3]"," ", html_page.lower().decode('utf-8')) # replace all but the listed characters
        
    for key in skill_set.keys():
        if key in html_text:  
            skill_set[key] +=1
            
    if counter % 5 == 0:
        print (len(job_links) - counter - index)
        print (skill_set)
        with open('scraped_links_restart.pkl','wb') as f:
            pickle.dump((skill_set, index+counter),f)
```

    http://www.indeed.com/rc/clk?jk=9627034d8cd27792
    http://www.indeed.com/rc/clk?jk=1a622fdca8324636
    http://www.indeed.com/rc/clk?jk=43cbd0278042f1a9
    http://www.indeed.com/rc/clk?jk=90d9ce0ec817ce5d
    http://www.indeed.com/rc/clk?jk=f4a9d97c8c38a1bd
    15
    {'mapreduce': 0, 'spark': 0}
    http://www.indeed.com/rc/clk?jk=6cafcb785bf65e38
    http://www.indeed.com/rc/clk?jk=393d33212c837508
    HTTPError:
    http://www.indeed.com/rc/clk?jk=88e81abcc346e95d
    http://www.indeed.com/rc/clk?jk=dfc0cfbf1931b500
    http://www.indeed.com/rc/clk?jk=dd7b858f3353173f
    10
    {'mapreduce': 0, 'spark': 1}
    http://www.indeed.com/rc/clk?jk=105e3b6bfc20affd
    http://www.indeed.com/rc/clk?jk=6c02bb6797a35086
    http://www.indeed.com/rc/clk?jk=75dc4303c7b87e54
    http://www.indeed.com/rc/clk?jk=ff1e67cce888db12
    http://www.indeed.com/rc/clk?jk=b05e817b8ae5cd9b
    5
    {'mapreduce': 1, 'spark': 3}
    http://www.indeed.com/rc/clk?jk=2e2f62c635384bc7
    http://www.indeed.com/rc/clk?jk=70b15d3a545c78db
    http://www.indeed.com/rc/clk?jk=5c172b03ffbfed14
    http://www.indeed.com/rc/clk?jk=d7129f312b301b2e
    http://www.indeed.com/rc/clk?jk=74e3caaf3a793916
    0
    {'mapreduce': 1, 'spark': 3}
    


```python
print (skill_set)
```

    {'mapreduce': 1, 'spark': 3}
    


# Scraping data science skills results



```python
pseries = pd.Series(skill_set)
pseries.sort_values(ascending=False)

pseries.plot(kind = 'bar')
## set the title to Score Comparison
plt.title('Data Science Skills')
## set the x label
plt.xlabel('Skills')
## set the y label
plt.ylabel('Count')
## show the plot
plt.show()
```


![png](WebScraping_Indeed_files/WebScraping_Indeed_16_0.png)

