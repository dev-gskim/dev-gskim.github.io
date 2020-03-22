# Flask Simple

## 

### install flask

```text
$ python -m pip install Flask==1.1.1
```

### python write app.py

```text
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run(host="0.0.0.0")
```

### start flask

```text
$ python app.py
```

