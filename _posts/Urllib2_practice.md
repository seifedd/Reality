
---
layout: post
title:  "Urllib2 library"
date:   2019-08-26 11:30:16 +0100
categories: ....
Description: .... 
Editor: S. Mejri
permalink: 0002.html
comments: true
---
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

# Urllib2


```python
htmlString = """<!DOCTYPE html>
<html>
  <head>
    <title>This is a title</title>
  </head>
  <body>
    <h2> Test </h2>
    <p>Hello world!</p>
  </body>
</html>"""
HTMLoutput=HTML(htmlString)
HTMLoutput
```




<!DOCTYPE html>
<html>
  <head>
    <title>This is a title</title>
  </head>
  <body>
    <h2> Test </h2>
    <p>Hello world!</p>
  </body>
</html>




```python
url="http://www.crummy.com/software/BeautifulSoup"
source = urllib2.urlopen(url).read()
print(source)
```

    b'<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"\n"http://www.w3.org/TR/REC-html40/transitional.dtd">\n<html>\n<head>\n<meta http-equiv="Content-Type" content="text/html; charset=utf-8">\n<title>Beautiful Soup: We called him Tortoise because he taught us.</title>\n<link rev="made" href="mailto:leonardr@segfault.org">\n<link rel="stylesheet" type="text/css" href="/nb/themes/Default/nb.css">\n<meta name="Description" content="Beautiful Soup: a library designed for screen-scraping HTML and XML.">\n<meta name="generator" content="Markov Approximation 1.4 (module: leonardr)">\n<meta name="author" content="Leonard Richardson">\n</head>\n<body bgcolor="white" text="black" link="blue" vlink="660066" alink="red">\n<img align="right" src="10.1.jpg" width="250"><br />\n\n<p>You didn\'t write that awful page. You\'re just trying to get some\ndata out of it. Beautiful Soup is here to help. Since 2004, it\'s been\nsaving programmers hours or days of work on quick-turnaround\nscreen scraping projects.</p>\n\n<div align="center">\n\n<a href="bs4/download/"><h1>Beautiful Soup</h1></a>\n\n<p>"A tremendous boon." -- Python411 Podcast</p>\n\n<p>[ <a href="#Download">Download</a> | <a\nhref="bs4/doc/">Documentation</a> | <a href="#HallOfFame">Hall of Fame</a> | <a href="https://code.launchpad.net/beautifulsoup">Source</a> | <a href="https://bazaar.launchpad.net/%7Eleonardr/beautifulsoup/bs4/view/head:/CHANGELOG">Changelog</a> | <a href="https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup">Discussion group</a>  | <a href="zine/">Zine</a> ]</p>\n\n<p><small>If you use Beautiful Soup as part of your work, please consider a <a href="https://tidelift.com/subscription/pkg/pypi-beautifulsoup4?utm_source=pypi-beautifulsoup4&utm_medium=referral&utm_campaign=website">Tidelift subscription</a>. This will support many of the free software projects your organization depends on, not just Beautiful Soup.\n<p>If Beautiful Soup is useful to you on a personal level, you might like to read <a href="zine/"><i>Tool Safety</i></a>, a short zine I wrote about what I learned about software development from working on Beautiful Soup. Thanks!</small></p>\n\n\n\n</div>\n\n<p><i>If you have questions, send them to <a\nhref="https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup">the discussion\ngroup</a>. If you find a bug, <a href="https://bugs.launchpad.net/beautifulsoup/">file it</a>.</i></p>\n\n<p>Beautiful Soup is a Python library designed for quick turnaround\nprojects like screen-scraping. Three features make it powerful:\n\n<ol>\n\n<li>Beautiful Soup provides a few simple methods and Pythonic idioms\nfor navigating, searching, and modifying a parse tree: a toolkit for\ndissecting a document and extracting what you need. It doesn\'t take\nmuch code to write an application\n\n<li>Beautiful Soup automatically converts incoming documents to\nUnicode and outgoing documents to UTF-8. You don\'t have to think\nabout encodings, unless the document doesn\'t specify an encoding and\nBeautiful Soup can\'t detect one. Then you just have to specify the\noriginal encoding.\n\n<li>Beautiful Soup sits on top of popular Python parsers like <a\nhref="http://lxml.de/">lxml</a> and <a\nhref="http://code.google.com/p/html5lib/">html5lib</a>, allowing you\nto try out different parsing strategies or trade speed for\nflexibility.\n\n</ol>\n\n<p>Beautiful Soup parses anything you give it, and does the tree\ntraversal stuff for you. You can tell it "Find all the links", or\n"Find all the links of class <tt>externalLink</tt>", or "Find all the\nlinks whose urls match "foo.com", or "Find the table heading that\'s\ngot bold text, then give me that text."\n\n<p>Valuable data that was once locked up in poorly-designed websites\nis now within your reach. Projects that would have taken hours take\nonly minutes with Beautiful Soup.\n\n<p>Interested? <a href="bs4/doc/">Read more.</a>\n\n<a name="Download"><h2>Download Beautiful Soup</h2></a>\n\n<p>The current release is <a href="bs4/download/">Beautiful Soup\n4.8.0</a> (July 20, 2019). You can install Beautiful Soup 4 with\n<code>pip install beautifulsoup4</code>.\n\n<p>In Debian and Ubuntu, Beautiful Soup is available as the\n<code>python-bs4</code> package (for Python 2) or the\n<code>python3-bs4</code> package (for Python 3). In Fedora it\'s\navailable as the <code>python-beautifulsoup4</code> package.\n\n<p>Beautiful Soup is licensed under the MIT license, so you can also\ndownload the tarball, drop the <code>bs4/</code> directory into almost\nany Python application (or into your library path) and start using it\nimmediately. (If you want to do this under Python 3, you will need to\nmanually convert the code using <code>2to3</code>.)\n\n<p>Beautiful Soup 4 works on both Python 2 (2.7+) and Python 3.\n\n<h3>Beautiful Soup 3</h3>\n\n<p>Beautiful Soup 3 was the official release line of Beautiful Soup\nfrom May 2006 to March 2012. It is considered stable, and only\ncritical security bugs will be fixed. <a\nhref="http://www.crummy.com/software/BeautifulSoup/bs3/documentation.html">Here\'s\nthe Beautiful Soup 3 documentation.</a>\n\n<p>Beautiful Soup 3 works only under Python 2.x. It is licensed under\nthe same license as Python itself.\n\n<p>The current release of Beautiful Soup 3 is <a\nhref="download/3.x/BeautifulSoup-3.2.1.tar.gz">3.2.1</a> (February 16,\n2012). You can install Beautiful Soup 3 with <code>pip install\nBeautifulSoup</code>. It\'s also available as\n<code>python-beautifulsoup</code> in Debian and Ubuntu, and as\n<code>python-BeautifulSoup</code> in Fedora.\n\n<p>You can also download the tarball and use\n<code>BeautifulSoup.py</code> in your project directly.\n\n\n<a name="HallOfFame"><h2>Hall of Fame</h2></a>\n\n<p>Over the years, Beautiful Soup has been used in hundreds of\ndifferent projects. There\'s no way I can list them all, but I want to\nhighlight a few high-profile projects. Beautiful Soup isn\'t what makes\nthese projects interesting, but it did make their completion easier:\n\n<ul>\n\n<li><a\n href="http://www.nytimes.com/2007/10/25/arts/design/25vide.html">"Movable\n Type"</a>, a work of digital art on display in the lobby of the New\n York Times building, uses Beautiful Soup to scrape news feeds.\n\n<li>Reddit uses Beautiful Soup to <a\nhref="https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py">parse\na page that\'s been linked to and find a representative image</a>.\n\n<li>Alexander Harrowell uses Beautiful Soup to <a\n href="http://www.harrowell.org.uk/viktormap.html">track the business\n activities</a> of an arms merchant.\n\n<li>The developers of Python itself used Beautiful Soup to <a\nhref="http://svn.python.org/view/tracker/importer/">migrate the Python\nbug tracker from Sourceforge to Roundup</a>.\n\n<li>The <a href="http://www2.ljworld.com/">Lawrence Journal-World</a>\nuses Beautiful Soup to <A\nhref="http://www.b-list.org/weblog/2010/nov/02/news-done-broke/">gather\nstatewide election results</a>.\n\n<li>The <a href="http://esrl.noaa.gov/gsd/fab/">NOAA\'s Forecast\nApplications Branch</a> uses Beautiful Soup in <a\nhref="http://laps.noaa.gov/topograbber/">TopoGrabber</a>, a script for\ndownloading "high resolution USGS datasets."\n\n</ul>\n\n<p>If you\'ve used Beautiful Soup in a project you\'d like me to know\nabout, please do send email to me or <a\nhref="http://groups.google.com/group/beautifulsoup/">the discussion\ngroup</a>.\n\n<h2>Development</h2>\n\n<p>Development happens at <a\nhref="https://launchpad.net/beautifulsoup">Launchpad</a>. You can <a\nhref="https://code.launchpad.net/beautifulsoup/">get the source\ncode</a> or <a href="https://bugs.launchpad.net/beautifulsoup/">file\nbugs</a>.<hr><table><tr><td valign="top">\n<p>This document (<a href="/source/software/BeautifulSoup/index.bhtml">source</a>) is part of Crummy, the webspace of <a href="/self/">Leonard Richardson</a> (<a href="/self/contact.html">contact information</a>). It was last modified on Sunday, July 21 2019, 17:41:10 Nowhere Standard Time and last built on Wednesday, August 14 2019, 23:00:01 Nowhere Standard Time.</p><p><table class="licenseText"><tr><td><a href="http://creativecommons.org/licenses/by-sa/2.0/"><img border="0" src="/nb//resources/img/somerights20.jpg"></a></td><td valign="top">Crummy is &copy; 1996-2019 Leonard Richardson. Unless otherwise noted, all text licensed under a <a href="http://creativecommons.org/licenses/by-sa/2.0/">Creative Commons License</a>.</td></tr></table></span><!--<rdf:RDF xmlns="http://web.resource.org/cc/" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><Work rdf:about="http://www.crummy.com/"><dc:title>Crummy: The Site</dc:title><dc:rights><Agent><dc:title>Crummy: the Site</dc:title></Agent></dc:rights><dc:format>text/html</dc:format><license rdf:resource=http://creativecommons.org/licenses/by-sa/2.0//></Work><License rdf:about="http://creativecommons.org/licenses/by-sa/2.0/"></License></rdf:RDF>--></p></td><td valign=top><p><b>Document tree:</b>\n<dl><dd><a href="http://www.crummy.com/">http://www.crummy.com/</a><dl><dd><a href="http://www.crummy.com/software/">software/</a><dl><dd><a href="http://www.crummy.com/software/BeautifulSoup/">BeautifulSoup/</a></dl>\n</dl>\n</dl>\n\n\nSite Search:\n\n<form method="get" action="/search/">\n        <input type="text" name="q" maxlength="255" value=""></input>\n        </form>\n        </td>\n\n</tr>\n\n</table>\n</body>\n</html>\n'
    


```python

```


```python
import re,string
# 'Soup' in str(source)
res = (re.findall(r'\w+', str(source))) 
'Soup' in res
source=str(source)
count = source.count('Soup')
print(count)
position=source.find('alien video games')
print(position)
substring=20;
print(source[substring:substring+2])
```

    45
    -1
    LI
    

# Beautiful Soup


```python
## get bs4 object
soup = bs4.BeautifulSoup(source)
 
## compare the two print statements
#print soup
#print soup.prettify()

## show how to find all a tags
soup.findAll('a')

## ***Why does this not work? ***
#soup.findAll('Soup')
```




    [<a href="bs4/download/"><h1>Beautiful Soup</h1></a>,
     <a href="#Download">Download</a>,
     <a href="#HallOfFame">Hall of Fame</a>,
     <a href="https://code.launchpad.net/beautifulsoup">Source</a>,
     <a href="https://bazaar.launchpad.net/%7Eleonardr/beautifulsoup/bs4/view/head:/CHANGELOG">Changelog</a>,
     <a href="https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup">Discussion group</a>,
     <a href="zine/">Zine</a>,
     <a href="https://tidelift.com/subscription/pkg/pypi-beautifulsoup4?utm_source=pypi-beautifulsoup4&amp;utm_medium=referral&amp;utm_campaign=website">Tidelift subscription</a>,
     <a href="zine/"><i>Tool Safety</i></a>,
     <a href="https://bugs.launchpad.net/beautifulsoup/">file it</a>,
     <a href="bs4/doc/">Read more.</a>,
     <a name="Download"><h2>Download Beautiful Soup</h2></a>,
     <a href="bs4/download/">Beautiful Soup\n4.8.0</a>,
     <a name="HallOfFame"><h2>Hall of Fame</h2></a>,
     <a href="http://www2.ljworld.com/">Lawrence Journal-World</a>,
     <a href="http://esrl.noaa.gov/gsd/fab/">NOAA\'s Forecast\nApplications Branch</a>,
     <a href="https://bugs.launchpad.net/beautifulsoup/">file\nbugs</a>,
     <a href="/source/software/BeautifulSoup/index.bhtml">source</a>,
     <a href="/self/">Leonard Richardson</a>,
     <a href="/self/contact.html">contact information</a>,
     <a href="http://creativecommons.org/licenses/by-sa/2.0/"><img border="0" src="/nb//resources/img/somerights20.jpg"/></a>,
     <a href="http://creativecommons.org/licenses/by-sa/2.0/">Creative Commons License</a>,
     <a href="http://www.crummy.com/">http://www.crummy.com/</a>,
     <a href="http://www.crummy.com/software/">software/</a>,
     <a href="http://www.crummy.com/software/BeautifulSoup/">BeautifulSoup/</a>]



Tag examples:
- heading <h1></h1> ... <h6></h6>

paragraph <p></p>

line break <br>

link with attribute


```python
url = 'http://www.crummy.com/software/BeautifulSoup'
source = urllib2.urlopen(url).read()
print(source)
```

    b'<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"\n"http://www.w3.org/TR/REC-html40/transitional.dtd">\n<html>\n<head>\n<meta http-equiv="Content-Type" content="text/html; charset=utf-8">\n<title>Beautiful Soup: We called him Tortoise because he taught us.</title>\n<link rev="made" href="mailto:leonardr@segfault.org">\n<link rel="stylesheet" type="text/css" href="/nb/themes/Default/nb.css">\n<meta name="Description" content="Beautiful Soup: a library designed for screen-scraping HTML and XML.">\n<meta name="generator" content="Markov Approximation 1.4 (module: leonardr)">\n<meta name="author" content="Leonard Richardson">\n</head>\n<body bgcolor="white" text="black" link="blue" vlink="660066" alink="red">\n<img align="right" src="10.1.jpg" width="250"><br />\n\n<p>You didn\'t write that awful page. You\'re just trying to get some\ndata out of it. Beautiful Soup is here to help. Since 2004, it\'s been\nsaving programmers hours or days of work on quick-turnaround\nscreen scraping projects.</p>\n\n<div align="center">\n\n<a href="bs4/download/"><h1>Beautiful Soup</h1></a>\n\n<p>"A tremendous boon." -- Python411 Podcast</p>\n\n<p>[ <a href="#Download">Download</a> | <a\nhref="bs4/doc/">Documentation</a> | <a href="#HallOfFame">Hall of Fame</a> | <a href="https://code.launchpad.net/beautifulsoup">Source</a> | <a href="https://bazaar.launchpad.net/%7Eleonardr/beautifulsoup/bs4/view/head:/CHANGELOG">Changelog</a> | <a href="https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup">Discussion group</a>  | <a href="zine/">Zine</a> ]</p>\n\n<p><small>If you use Beautiful Soup as part of your work, please consider a <a href="https://tidelift.com/subscription/pkg/pypi-beautifulsoup4?utm_source=pypi-beautifulsoup4&utm_medium=referral&utm_campaign=website">Tidelift subscription</a>. This will support many of the free software projects your organization depends on, not just Beautiful Soup.\n<p>If Beautiful Soup is useful to you on a personal level, you might like to read <a href="zine/"><i>Tool Safety</i></a>, a short zine I wrote about what I learned about software development from working on Beautiful Soup. Thanks!</small></p>\n\n\n\n</div>\n\n<p><i>If you have questions, send them to <a\nhref="https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup">the discussion\ngroup</a>. If you find a bug, <a href="https://bugs.launchpad.net/beautifulsoup/">file it</a>.</i></p>\n\n<p>Beautiful Soup is a Python library designed for quick turnaround\nprojects like screen-scraping. Three features make it powerful:\n\n<ol>\n\n<li>Beautiful Soup provides a few simple methods and Pythonic idioms\nfor navigating, searching, and modifying a parse tree: a toolkit for\ndissecting a document and extracting what you need. It doesn\'t take\nmuch code to write an application\n\n<li>Beautiful Soup automatically converts incoming documents to\nUnicode and outgoing documents to UTF-8. You don\'t have to think\nabout encodings, unless the document doesn\'t specify an encoding and\nBeautiful Soup can\'t detect one. Then you just have to specify the\noriginal encoding.\n\n<li>Beautiful Soup sits on top of popular Python parsers like <a\nhref="http://lxml.de/">lxml</a> and <a\nhref="http://code.google.com/p/html5lib/">html5lib</a>, allowing you\nto try out different parsing strategies or trade speed for\nflexibility.\n\n</ol>\n\n<p>Beautiful Soup parses anything you give it, and does the tree\ntraversal stuff for you. You can tell it "Find all the links", or\n"Find all the links of class <tt>externalLink</tt>", or "Find all the\nlinks whose urls match "foo.com", or "Find the table heading that\'s\ngot bold text, then give me that text."\n\n<p>Valuable data that was once locked up in poorly-designed websites\nis now within your reach. Projects that would have taken hours take\nonly minutes with Beautiful Soup.\n\n<p>Interested? <a href="bs4/doc/">Read more.</a>\n\n<a name="Download"><h2>Download Beautiful Soup</h2></a>\n\n<p>The current release is <a href="bs4/download/">Beautiful Soup\n4.8.0</a> (July 20, 2019). You can install Beautiful Soup 4 with\n<code>pip install beautifulsoup4</code>.\n\n<p>In Debian and Ubuntu, Beautiful Soup is available as the\n<code>python-bs4</code> package (for Python 2) or the\n<code>python3-bs4</code> package (for Python 3). In Fedora it\'s\navailable as the <code>python-beautifulsoup4</code> package.\n\n<p>Beautiful Soup is licensed under the MIT license, so you can also\ndownload the tarball, drop the <code>bs4/</code> directory into almost\nany Python application (or into your library path) and start using it\nimmediately. (If you want to do this under Python 3, you will need to\nmanually convert the code using <code>2to3</code>.)\n\n<p>Beautiful Soup 4 works on both Python 2 (2.7+) and Python 3.\n\n<h3>Beautiful Soup 3</h3>\n\n<p>Beautiful Soup 3 was the official release line of Beautiful Soup\nfrom May 2006 to March 2012. It is considered stable, and only\ncritical security bugs will be fixed. <a\nhref="http://www.crummy.com/software/BeautifulSoup/bs3/documentation.html">Here\'s\nthe Beautiful Soup 3 documentation.</a>\n\n<p>Beautiful Soup 3 works only under Python 2.x. It is licensed under\nthe same license as Python itself.\n\n<p>The current release of Beautiful Soup 3 is <a\nhref="download/3.x/BeautifulSoup-3.2.1.tar.gz">3.2.1</a> (February 16,\n2012). You can install Beautiful Soup 3 with <code>pip install\nBeautifulSoup</code>. It\'s also available as\n<code>python-beautifulsoup</code> in Debian and Ubuntu, and as\n<code>python-BeautifulSoup</code> in Fedora.\n\n<p>You can also download the tarball and use\n<code>BeautifulSoup.py</code> in your project directly.\n\n\n<a name="HallOfFame"><h2>Hall of Fame</h2></a>\n\n<p>Over the years, Beautiful Soup has been used in hundreds of\ndifferent projects. There\'s no way I can list them all, but I want to\nhighlight a few high-profile projects. Beautiful Soup isn\'t what makes\nthese projects interesting, but it did make their completion easier:\n\n<ul>\n\n<li><a\n href="http://www.nytimes.com/2007/10/25/arts/design/25vide.html">"Movable\n Type"</a>, a work of digital art on display in the lobby of the New\n York Times building, uses Beautiful Soup to scrape news feeds.\n\n<li>Reddit uses Beautiful Soup to <a\nhref="https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py">parse\na page that\'s been linked to and find a representative image</a>.\n\n<li>Alexander Harrowell uses Beautiful Soup to <a\n href="http://www.harrowell.org.uk/viktormap.html">track the business\n activities</a> of an arms merchant.\n\n<li>The developers of Python itself used Beautiful Soup to <a\nhref="http://svn.python.org/view/tracker/importer/">migrate the Python\nbug tracker from Sourceforge to Roundup</a>.\n\n<li>The <a href="http://www2.ljworld.com/">Lawrence Journal-World</a>\nuses Beautiful Soup to <A\nhref="http://www.b-list.org/weblog/2010/nov/02/news-done-broke/">gather\nstatewide election results</a>.\n\n<li>The <a href="http://esrl.noaa.gov/gsd/fab/">NOAA\'s Forecast\nApplications Branch</a> uses Beautiful Soup in <a\nhref="http://laps.noaa.gov/topograbber/">TopoGrabber</a>, a script for\ndownloading "high resolution USGS datasets."\n\n</ul>\n\n<p>If you\'ve used Beautiful Soup in a project you\'d like me to know\nabout, please do send email to me or <a\nhref="http://groups.google.com/group/beautifulsoup/">the discussion\ngroup</a>.\n\n<h2>Development</h2>\n\n<p>Development happens at <a\nhref="https://launchpad.net/beautifulsoup">Launchpad</a>. You can <a\nhref="https://code.launchpad.net/beautifulsoup/">get the source\ncode</a> or <a href="https://bugs.launchpad.net/beautifulsoup/">file\nbugs</a>.<hr><table><tr><td valign="top">\n<p>This document (<a href="/source/software/BeautifulSoup/index.bhtml">source</a>) is part of Crummy, the webspace of <a href="/self/">Leonard Richardson</a> (<a href="/self/contact.html">contact information</a>). It was last modified on Sunday, July 21 2019, 17:41:10 Nowhere Standard Time and last built on Thursday, August 15 2019, 04:00:01 Nowhere Standard Time.</p><p><table class="licenseText"><tr><td><a href="http://creativecommons.org/licenses/by-sa/2.0/"><img border="0" src="/nb//resources/img/somerights20.jpg"></a></td><td valign="top">Crummy is &copy; 1996-2019 Leonard Richardson. Unless otherwise noted, all text licensed under a <a href="http://creativecommons.org/licenses/by-sa/2.0/">Creative Commons License</a>.</td></tr></table></span><!--<rdf:RDF xmlns="http://web.resource.org/cc/" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><Work rdf:about="http://www.crummy.com/"><dc:title>Crummy: The Site</dc:title><dc:rights><Agent><dc:title>Crummy: the Site</dc:title></Agent></dc:rights><dc:format>text/html</dc:format><license rdf:resource=http://creativecommons.org/licenses/by-sa/2.0//></Work><License rdf:about="http://creativecommons.org/licenses/by-sa/2.0/"></License></rdf:RDF>--></p></td><td valign=top><p><b>Document tree:</b>\n<dl><dd><a href="http://www.crummy.com/">http://www.crummy.com/</a><dl><dd><a href="http://www.crummy.com/software/">software/</a><dl><dd><a href="http://www.crummy.com/software/BeautifulSoup/">BeautifulSoup/</a></dl>\n</dl>\n</dl>\n\n\nSite Search:\n\n<form method="get" action="/search/">\n        <input type="text" name="q" maxlength="255" value=""></input>\n        </form>\n        </td>\n\n</tr>\n\n</table>\n</body>\n</html>\n'
    


```python
'rights' in str(source)
##find index of 'alien video games'
position =  str(source).find('Soup')
print(position)
print(source[position:20+position])
```

    220
    b'e called him Tortois'
    


```python
#get bs4 object 
soup=bs4.BeautifulSoup(source)

```


```python
soup.findAll('a')
```




    [<a href="bs4/download/"><h1>Beautiful Soup</h1></a>,
     <a href="#Download">Download</a>,
     <a href="bs4/doc/">Documentation</a>,
     <a href="#HallOfFame">Hall of Fame</a>,
     <a href="https://code.launchpad.net/beautifulsoup">Source</a>,
     <a href="https://bazaar.launchpad.net/%7Eleonardr/beautifulsoup/bs4/view/head:/CHANGELOG">Changelog</a>,
     <a href="https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup">Discussion group</a>,
     <a href="zine/">Zine</a>,
     <a href="https://tidelift.com/subscription/pkg/pypi-beautifulsoup4?utm_source=pypi-beautifulsoup4&amp;utm_medium=referral&amp;utm_campaign=website">Tidelift subscription</a>,
     <a href="zine/"><i>Tool Safety</i></a>,
     <a href="https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup">the discussion
     group</a>,
     <a href="https://bugs.launchpad.net/beautifulsoup/">file it</a>,
     <a href="http://lxml.de/">lxml</a>,
     <a href="http://code.google.com/p/html5lib/">html5lib</a>,
     <a href="bs4/doc/">Read more.</a>,
     <a name="Download"><h2>Download Beautiful Soup</h2></a>,
     <a href="bs4/download/">Beautiful Soup
     4.8.0</a>,
     <a href="http://www.crummy.com/software/BeautifulSoup/bs3/documentation.html">Here's
     the Beautiful Soup 3 documentation.</a>,
     <a href="download/3.x/BeautifulSoup-3.2.1.tar.gz">3.2.1</a>,
     <a name="HallOfFame"><h2>Hall of Fame</h2></a>,
     <a href="http://www.nytimes.com/2007/10/25/arts/design/25vide.html">"Movable
      Type"</a>,
     <a href="https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py">parse
     a page that's been linked to and find a representative image</a>,
     <a href="http://www.harrowell.org.uk/viktormap.html">track the business
      activities</a>,
     <a href="http://svn.python.org/view/tracker/importer/">migrate the Python
     bug tracker from Sourceforge to Roundup</a>,
     <a href="http://www2.ljworld.com/">Lawrence Journal-World</a>,
     <a href="http://www.b-list.org/weblog/2010/nov/02/news-done-broke/">gather
     statewide election results</a>,
     <a href="http://esrl.noaa.gov/gsd/fab/">NOAA's Forecast
     Applications Branch</a>,
     <a href="http://laps.noaa.gov/topograbber/">TopoGrabber</a>,
     <a href="http://groups.google.com/group/beautifulsoup/">the discussion
     group</a>,
     <a href="https://launchpad.net/beautifulsoup">Launchpad</a>,
     <a href="https://code.launchpad.net/beautifulsoup/">get the source
     code</a>,
     <a href="https://bugs.launchpad.net/beautifulsoup/">file
     bugs</a>,
     <a href="/source/software/BeautifulSoup/index.bhtml">source</a>,
     <a href="/self/">Leonard Richardson</a>,
     <a href="/self/contact.html">contact information</a>,
     <a href="http://creativecommons.org/licenses/by-sa/2.0/"><img border="0" src="/nb//resources/img/somerights20.jpg"/></a>,
     <a href="http://creativecommons.org/licenses/by-sa/2.0/">Creative Commons License</a>,
     <a href="http://www.crummy.com/">http://www.crummy.com/</a>,
     <a href="http://www.crummy.com/software/">software/</a>,
     <a href="http://www.crummy.com/software/BeautifulSoup/">BeautifulSoup/</a>]




```python
first_tag=soup.findAll('a')


#get all link in the page 
link_list=[l.get('href') for l in first_tag]
link_list        

```




    ['bs4/download/',
     '#Download',
     'bs4/doc/',
     '#HallOfFame',
     'https://code.launchpad.net/beautifulsoup',
     'https://bazaar.launchpad.net/%7Eleonardr/beautifulsoup/bs4/view/head:/CHANGELOG',
     'https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup',
     'zine/',
     'https://tidelift.com/subscription/pkg/pypi-beautifulsoup4?utm_source=pypi-beautifulsoup4&utm_medium=referral&utm_campaign=website',
     'zine/',
     'https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup',
     'https://bugs.launchpad.net/beautifulsoup/',
     'http://lxml.de/',
     'http://code.google.com/p/html5lib/',
     'bs4/doc/',
     None,
     'bs4/download/',
     'http://www.crummy.com/software/BeautifulSoup/bs3/documentation.html',
     'download/3.x/BeautifulSoup-3.2.1.tar.gz',
     None,
     'http://www.nytimes.com/2007/10/25/arts/design/25vide.html',
     'https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py',
     'http://www.harrowell.org.uk/viktormap.html',
     'http://svn.python.org/view/tracker/importer/',
     'http://www2.ljworld.com/',
     'http://www.b-list.org/weblog/2010/nov/02/news-done-broke/',
     'http://esrl.noaa.gov/gsd/fab/',
     'http://laps.noaa.gov/topograbber/',
     'http://groups.google.com/group/beautifulsoup/',
     'https://launchpad.net/beautifulsoup',
     'https://code.launchpad.net/beautifulsoup/',
     'https://bugs.launchpad.net/beautifulsoup/',
     '/source/software/BeautifulSoup/index.bhtml',
     '/self/',
     '/self/contact.html',
     'http://creativecommons.org/licenses/by-sa/2.0/',
     'http://creativecommons.org/licenses/by-sa/2.0/',
     'http://www.crummy.com/',
     'http://www.crummy.com/software/',
     'http://www.crummy.com/software/BeautifulSoup/']




```python
## filter all external links
# create an empty list to collect the valid links
#filter 
link_list=[l.get('href') for l in first_tag]
link_list

external_link=[l  for l in link_list if l is not None and l.startswith('http') ]        
print(external_link)
        
```

    ['https://code.launchpad.net/beautifulsoup', 'https://bazaar.launchpad.net/%7Eleonardr/beautifulsoup/bs4/view/head:/CHANGELOG', 'https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup', 'https://tidelift.com/subscription/pkg/pypi-beautifulsoup4?utm_source=pypi-beautifulsoup4&utm_medium=referral&utm_campaign=website', 'https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup', 'https://bugs.launchpad.net/beautifulsoup/', 'http://lxml.de/', 'http://code.google.com/p/html5lib/', 'http://www.crummy.com/software/BeautifulSoup/bs3/documentation.html', 'http://www.nytimes.com/2007/10/25/arts/design/25vide.html', 'https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py', 'http://www.harrowell.org.uk/viktormap.html', 'http://svn.python.org/view/tracker/importer/', 'http://www2.ljworld.com/', 'http://www.b-list.org/weblog/2010/nov/02/news-done-broke/', 'http://esrl.noaa.gov/gsd/fab/', 'http://laps.noaa.gov/topograbber/', 'http://groups.google.com/group/beautifulsoup/', 'https://launchpad.net/beautifulsoup', 'https://code.launchpad.net/beautifulsoup/', 'https://bugs.launchpad.net/beautifulsoup/', 'http://creativecommons.org/licenses/by-sa/2.0/', 'http://creativecommons.org/licenses/by-sa/2.0/', 'http://www.crummy.com/', 'http://www.crummy.com/software/', 'http://www.crummy.com/software/BeautifulSoup/']
    


```python
new_list_for_external_list=[]

for l in link_list:
    if l is not None and l.startswith('http'):
        new_list_for_external_list.append(l)
print(new_list_for_external_list)
```

    ['https://code.launchpad.net/beautifulsoup', 'https://bazaar.launchpad.net/%7Eleonardr/beautifulsoup/bs4/view/head:/CHANGELOG', 'https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup', 'https://tidelift.com/subscription/pkg/pypi-beautifulsoup4?utm_source=pypi-beautifulsoup4&utm_medium=referral&utm_campaign=website', 'https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup', 'https://bugs.launchpad.net/beautifulsoup/', 'http://lxml.de/', 'http://code.google.com/p/html5lib/', 'http://www.crummy.com/software/BeautifulSoup/bs3/documentation.html', 'http://www.nytimes.com/2007/10/25/arts/design/25vide.html', 'https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py', 'http://www.harrowell.org.uk/viktormap.html', 'http://svn.python.org/view/tracker/importer/', 'http://www2.ljworld.com/', 'http://www.b-list.org/weblog/2010/nov/02/news-done-broke/', 'http://esrl.noaa.gov/gsd/fab/', 'http://laps.noaa.gov/topograbber/', 'http://groups.google.com/group/beautifulsoup/', 'https://launchpad.net/beautifulsoup', 'https://code.launchpad.net/beautifulsoup/', 'https://bugs.launchpad.net/beautifulsoup/', 'http://creativecommons.org/licenses/by-sa/2.0/', 'http://creativecommons.org/licenses/by-sa/2.0/', 'http://www.crummy.com/', 'http://www.crummy.com/software/', 'http://www.crummy.com/software/BeautifulSoup/']
    


```python
[l for l in link_list if l is not None and l.startswith('http')]
```




    ['https://code.launchpad.net/beautifulsoup',
     'https://bazaar.launchpad.net/%7Eleonardr/beautifulsoup/bs4/view/head:/CHANGELOG',
     'https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup',
     'https://tidelift.com/subscription/pkg/pypi-beautifulsoup4?utm_source=pypi-beautifulsoup4&utm_medium=referral&utm_campaign=website',
     'https://groups.google.com/forum/?fromgroups#!forum/beautifulsoup',
     'https://bugs.launchpad.net/beautifulsoup/',
     'http://lxml.de/',
     'http://code.google.com/p/html5lib/',
     'http://www.crummy.com/software/BeautifulSoup/bs3/documentation.html',
     'http://www.nytimes.com/2007/10/25/arts/design/25vide.html',
     'https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py',
     'http://www.harrowell.org.uk/viktormap.html',
     'http://svn.python.org/view/tracker/importer/',
     'http://www2.ljworld.com/',
     'http://www.b-list.org/weblog/2010/nov/02/news-done-broke/',
     'http://esrl.noaa.gov/gsd/fab/',
     'http://laps.noaa.gov/topograbber/',
     'http://groups.google.com/group/beautifulsoup/',
     'https://launchpad.net/beautifulsoup',
     'https://code.launchpad.net/beautifulsoup/',
     'https://bugs.launchpad.net/beautifulsoup/',
     'http://creativecommons.org/licenses/by-sa/2.0/',
     'http://creativecommons.org/licenses/by-sa/2.0/',
     'http://www.crummy.com/',
     'http://www.crummy.com/software/',
     'http://www.crummy.com/software/BeautifulSoup/']




```python

# redifining `s` without any line breaks
s =['<html><head><title>Page title</title></head>',
       '<body><p id="firstpara" align="center">This is paragraph <b>one</b>.',
        '<p id="secondpara" align="blah">This is paragraph <b>two</b>.',
        '</html>']
tree = bs4.BeautifulSoup(''.join(s))

## get html root node
root_node = tree.html

## get head from root using contents
head = root_node.contents[0]

## get body from root
body = root_node.contents[1]

## could directly access body
print(tree.contents[0].contents[1].name)
# Directy access body
tree.body

```

    body
    




    <body><p align="center" id="firstpara">This is paragraph <b>one</b>.<p align="blah" id="secondpara">This is paragraph <b>two</b>.</p></p></body>




```python
#Find the p tag 
print(tree.contents[0].contents[1].p)
print(body.contents[0])
```

    <p align="center" id="firstpara">This is paragraph <b>one</b>.<p align="blah" id="secondpara">This is paragraph <b>two</b>.</p></p>
    <p align="center" id="firstpara">This is paragraph <b>one</b>.<p align="blah" id="secondpara">This is paragraph <b>two</b>.</p></p>
    


```python
s = """<!DOCTYPE html><html><head><title>This is a title</title></head><body><h3> Test </h3><p>Hello world!</p></body></html>"""
## get bs4 object
tree=bs4.BeautifulSoup(s)

## use ul as entry point
entry_point = soup.find('ul')

## get hall of fame list from entry point
## skip the first entry 
hall_of_fame_list=entry_point.contents[1:]

tmp=[]
for l in hall_of_fame_list:
    
    tmp.append(l.contents)
print(tmp)
```

    [[<a href="http://www.nytimes.com/2007/10/25/arts/design/25vide.html">"Movable
     Type"</a>, ', a work of digital art on display in the lobby of the New\n York Times building, uses Beautiful Soup to scrape news feeds.\n\n', <li>Reddit uses Beautiful Soup to <a href="https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py">parse
    a page that's been linked to and find a representative image</a>.
    
    <li>Alexander Harrowell uses Beautiful Soup to <a href="http://www.harrowell.org.uk/viktormap.html">track the business
     activities</a> of an arms merchant.
    
    <li>The developers of Python itself used Beautiful Soup to <a href="http://svn.python.org/view/tracker/importer/">migrate the Python
    bug tracker from Sourceforge to Roundup</a>.
    
    <li>The <a href="http://www2.ljworld.com/">Lawrence Journal-World</a>
    uses Beautiful Soup to <a href="http://www.b-list.org/weblog/2010/nov/02/news-done-broke/">gather
    statewide election results</a>.
    
    <li>The <a href="http://esrl.noaa.gov/gsd/fab/">NOAA's Forecast
    Applications Branch</a> uses Beautiful Soup in <a href="http://laps.noaa.gov/topograbber/">TopoGrabber</a>, a script for
    downloading "high resolution USGS datasets."
    
    </li></li></li></li></li>]]
    


```python
test =  ["".join(str(a) for a in sublist) for sublist in tmp]
print('\n'.join(test))

```

    <a href="http://www.nytimes.com/2007/10/25/arts/design/25vide.html">"Movable
     Type"</a>, a work of digital art on display in the lobby of the New
     York Times building, uses Beautiful Soup to scrape news feeds.
    
    <li>Reddit uses Beautiful Soup to <a href="https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py">parse
    a page that's been linked to and find a representative image</a>.
    
    <li>Alexander Harrowell uses Beautiful Soup to <a href="http://www.harrowell.org.uk/viktormap.html">track the business
     activities</a> of an arms merchant.
    
    <li>The developers of Python itself used Beautiful Soup to <a href="http://svn.python.org/view/tracker/importer/">migrate the Python
    bug tracker from Sourceforge to Roundup</a>.
    
    <li>The <a href="http://www2.ljworld.com/">Lawrence Journal-World</a>
    uses Beautiful Soup to <a href="http://www.b-list.org/weblog/2010/nov/02/news-done-broke/">gather
    statewide election results</a>.
    
    <li>The <a href="http://esrl.noaa.gov/gsd/fab/">NOAA's Forecast
    Applications Branch</a> uses Beautiful Soup in <a href="http://laps.noaa.gov/topograbber/">TopoGrabber</a>, a script for
    downloading "high resolution USGS datasets."
    
    </li></li></li></li></li>
    [[<a href="http://www.nytimes.com/2007/10/25/arts/design/25vide.html">"Movable
     Type"</a>, ', a work of digital art on display in the lobby of the New\n York Times building, uses Beautiful Soup to scrape news feeds.\n\n', <li>Reddit uses Beautiful Soup to <a href="https://github.com/reddit/reddit/blob/85f9cff3e2ab9bb8f19b96acd8da4ebacc079f04/r2/r2/lib/media.py">parse
    a page that's been linked to and find a representative image</a>.
    
    <li>Alexander Harrowell uses Beautiful Soup to <a href="http://www.harrowell.org.uk/viktormap.html">track the business
     activities</a> of an arms merchant.
    
    <li>The developers of Python itself used Beautiful Soup to <a href="http://svn.python.org/view/tracker/importer/">migrate the Python
    bug tracker from Sourceforge to Roundup</a>.
    
    <li>The <a href="http://www2.ljworld.com/">Lawrence Journal-World</a>
    uses Beautiful Soup to <a href="http://www.b-list.org/weblog/2010/nov/02/news-done-broke/">gather
    statewide election results</a>.
    
    <li>The <a href="http://esrl.noaa.gov/gsd/fab/">NOAA's Forecast
    Applications Branch</a> uses Beautiful Soup in <a href="http://laps.noaa.gov/topograbber/">TopoGrabber</a>, a script for
    downloading "high resolution USGS datasets."
    
    </li></li></li></li></li>]]
    
