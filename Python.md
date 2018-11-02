Python Cheat Sheet

In Python3, ImportError: module 'pip' has no attribute 'main' 
`sudo python3 -m pip install <package name>`

Connect Jupyter-Notebook to native Python3 kernel (Not anaconda python3 kernel)
` vim /Users/{username}/Library/Jupyter/kernels/python3/kernel.json`
```
{
 "argv": [
  "/usr/local/bin/python3",
  "-m",
  "ipykernel",
  "-f",
  "{connection_file}"
 ],
 "display_name": "Python 3",
 "language": "python"
}

```

Create PDF file in Python
```
from reportlab.pdfgen import canvas
from reportlab.lib.pagesizes import letter

width, height = letter
c = canvas.Canvas("Hello.pdf", pagesize=letter)
c.drawString(width/2,height/2,"Hello World!")
c.save()
```

Create multiple page PDF in Python using Reportlab `canvas.showPage()`
```
from reportlab.pdfgen import canvas
from reportlab.lib.pagesizes import letter

width, height = letter
c = canvas.Canvas("Hello.pdf", pagesize=letter)
c.drawString(width/2,height/2,"Page1")
c.showPage()  #Close the current page and start on a new page.
c.drawString(width/2,height/2,"Page2")
c.save()
```

Convert string-tpye json into dictionary-type json in Python
```
import json
f = open("test.json",'r')
data = f.read()
json_data = json.loads(data)
```

Using wand.image to make thumbnail
```
from wand.image import Image
with Image(blob=infile) as img:
    # Convert original picture to 50x50 thumbnail picture
    img.resize(50, 50)
    img.save(filename="test.png")
```

In python3, we can directly assign the variable in string
```
date = "Sunday"
print(f'Today is {date}')
### Today is Sunday
```

Encode/decode the String/byte-like object
```
s = "Hello world!"
encoded = s.encoded("utf-8")
# b"Hello world!"
decoded = encoded.decode("utf-8") 
# "Hello world!"

s = '你好'
encoded = s.encoded("utf-8")
# b'\xe4\xbd\xa0\xe5\xa5\xbd'
decoded = encoded.decode("utf-8") 
# '你好'
```

base64 encoding/decoding
```
import base64
string = 'Hello World!'
# Encode
# string_encoded = base64.b64encode(string)
# TypeError: a bytes-like object is required, not 'str'
# Make sure using bytes-like object as input such as utf-8
string_encoded = base64.b64encode(string.encode('utf-8'))
# b'SGVsbG8gV29ybGQh'

# Decode
string_decoded = base64.b64decode(string_encoded).decode('utf-8')
# 'Hello World!'
```

Image rotation
Issue: The photo upload from iOS app can't store with the correct driection in AWS S3.
Fix: Find EXIF in the picture and do some corresponding rotation. `image.auto_orient()` can easily fix this problem.
```
from wand.image import Image
with Image(blob=infile) as img:
    # Rotate the picture to correct direction
    img.auto_orient()
    img.save(filename="test.png")
```

Print EXIF(Exchangeable image file format) of image using wand.image
```
from wand.image import Image
with Image(blob=infile) as img:
	for key, value in img.metadata.items():
	    if key.startswith('exif:'):
	        print(key, value)
#exif:ColorSpace 1
#exif:ExifImageLength 4096
#exif:ExifImageWidth 2304
#exif:ExifOffset 38
#exif:Orientation 1
```

Deal with 'multipart/form-data' request from user in Lambda built by chalice.
Receive multiple files from http request in Python such as multiple json file, multiple picture.
```
import cgi
from io import BytesIO
from chalice import Chalice

app = Chalice(app_name='test-upload')
app.debug = True

def _get_parts():
    rfile = BytesIO(app.current_request.raw_body)
    content_type = app.current_request.headers['content-type']
    _, parameters = cgi.parse_header(content_type)
    parameters['boundary'] = parameters['boundary'].encode('utf-8')
    parsed = cgi.parse_multipart(rfile, parameters)
    return parsed

@app.route('/upload', methods=['POST'],content_types=['multipart/form-data'])
def upload():
    files = _get_parts()
    return {k: v[0].decode('utf-8') for (k, v) in files.items()}
# {filename1: data1, filename2:data2, ...}
```

`import request` Error when deploy Python app in lambda using chalice, using the following package instead
`from botocore.vendored import requests`


Deploy app in Lambda Chalice Error. `ImportError`: I can't load my own function from my script
1. Find out that the same import code in python2 can't load but in python3 it works
2. Try to chage my native `$python` from python2 > python3
3. Find the file in /usr/local/bin/. Delete the original python alias and make a copy of python3 alias and named it python
4. But it still doesn't work. Because in environment variable setting, there is another python path in /usr/bin which I think is the mac built-in python2 
5. Comments the export = /usr/bin temperately in `~/.bash_profile`
6. `python --version` will show python3.6.0
7. Try to deploy --> still doesn't work, same error
8. Install chalice in python3 environment: `sudo python3 -m pip install chalice`
9. Sucessfully deploy
10. uncomment the export = /usr/bin temperately in `~/.bash_profile`


Receive Weird Bytes from picture via http request in python
The first bytes showing `\xef\xbf\xbd\xef\xbf\xbd\xef\xbf\xbd\xef\xbf\xbd\x00\x10JFIF`
`\xef\xbf\xbd` is replacing unknown character with "? in a square".

```
response = requests.get(url).text
# get werid bytes \xef\xbf\xbd from picture which means the picture is distorted
response = requests.get(url).content
# get \xff\xd8\xff which is representing .jpg file
```