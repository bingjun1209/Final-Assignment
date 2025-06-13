# 亞洲大學進階程式設計期末作業
(1) Flask Website on PythonAnywhere
1. 建立一個flask app:
   # sayhello_web.py
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return '<h1>Hello, this is SayHello on PythonAnywhere!</h1>'
2.上傳 sayhello_web.py 至 PythonAnywhere（可用 Bash 或 Web File Manager）。
3.在「Web」頁面：
  新增一個 Web App。
  選擇 Flask，設定 WSGI 檔案指向你的 Flask app。
  修改 WSGI 檔案加入：
  import sys
path = '/home/yourusername/path_to_project'
if path not in sys.path:
    sys.path.append(path)

from sayhello_web import app as application
(2) Flask RESTful API on PythonAnywhere
1.建立API程式
程式如右--
