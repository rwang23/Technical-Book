##Web Crawl
```python
import urllib2

# Request source file
url = 'http://yue.ifeng.com'
request = urllib2.Request(url)
response = urllib2.urlopen(request)
page = response.read()

# Save Source file

webFile = open('webPage.html', 'wb')
webFile.write(page)
webFile.close()
```
