# 🏁 亞洲大學進階程式設計期末作業

## 🐍 SayHello Flask 專案

這是一個基於 Flask 的簡單應用範例，展示如何將同一個應用部署到四個平台：

* PythonAnywhere 靜態網站
* PythonAnywhere RESTful API
* AWS Lambda + API Gateway（透過 Zappa）
* AWS Elastic Beanstalk

---

## 📁 專案結構

```
sayhello-flask/
├── sayhello_web/         → Flask 網站
├── sayhello_api/         → Flask RESTful API
├── sayhello_lambda/      → AWS Lambda (Zappa)
├── sayhello_eb/          → Elastic Beanstalk 應用
└── README.md             → 本說明文件
```

---

## 1️⃣ PythonAnywhere 靜態網站

📂 資料夾：`sayhello_web`
📄 [👉 點此查看程式碼](./sayhello_web/sayhello_web.py)

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return '<h1>Hello, this is SayHello Website on PythonAnywhere!</h1>'

if __name__ == '__main__':
    app.run(debug=True)
```

---

## 2️⃣ PythonAnywhere RESTful API

📂 資料夾：`sayhello_api`
📄 [👉 點此查看程式碼](./sayhello_api/sayhello_api.py)
📄 [👉 點此查看 requirements.txt](./sayhello_api/requirements.txt)

```python
from flask import Flask
from flask_restful import Resource, Api

app = Flask(__name__)
api = Api(app)

class Hello(Resource):
    def get(self):
        return {'message': 'Hello from RESTful API on PythonAnywhere'}

api.add_resource(Hello, '/')

if __name__ == '__main__':
    app.run(debug=True)
```

📦 `requirements.txt`

```
flask
flask-restful
```

---

## 3️⃣ AWS Lambda (Zappa)

📂 資料夾：`sayhello_lambda`
📄 [👉 點此查看程式碼](./sayhello_lambda/sayhello_lambda.py)
📄 [👉 點此查看 requirements.txt](./sayhello_lambda/requirements.txt)
📄 [👉 點此查看 zappa\_settings.json](./sayhello_lambda/zappa_settings.json)

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return {'message': 'Hello from AWS Lambda (Zappa)'}

if __name__ == '__main__':
    app.run(debug=True)
```

📦 `requirements.txt`

```
flask
zappa
```

⚙️ `zappa_settings.json`

```json
{
  "dev": {
    "app_function": "sayhello_lambda.app",
    "aws_region": "us-east-1",
    "profile_name": "default",
    "project_name": "sayhello_lambda",
    "runtime": "python3.11",
    "s3_bucket": "your-zappa-s3-bucket"
  }
}
```

---

## 4️⃣ AWS Elastic Beanstalk

📂 資料夾：`sayhello_eb`
📄 [👉 點此查看程式碼](./sayhello_eb/application.py)
📄 [👉 點此查看 requirements.txt](./sayhello_eb/requirements.txt)
📄 [👉 點此查看 python.config](./sayhello_eb/.ebextensions/python.config)

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return 'Hello from AWS Elastic Beanstalk!'

if __name__ == '__main__':
    app.run(debug=True)
```

📦 `requirements.txt`

```
flask
```

📄 `.ebextensions/python.config`

```yaml
option_settings:
  aws:elasticbeanstalk:container:python:
    WSGIPath: application:app
```

---

## 🛠 教學步驟說明

以下是如何將 Flask 應用分別部署到 4 種平台的完整教學流程：

### 1️⃣ PythonAnywhere 靜態網站部署

1. 註冊並登入 [PythonAnywhere](https://www.pythonanywhere.com/)
2. 建立新的 Web App，選擇：**Flask + Python 版本**
3. 上傳你的 `sayhello_web.py` 到 `/home/你的帳號/`
4. 修改 `WSGI` 設定檔，將原本內容改為：

```python
import sys
path = '/home/你的帳號'
if path not in sys.path:
    sys.path.append(path)

from sayhello_web import app as application
```

5. 點選「Reload」，瀏覽器開啟即可看到網頁

---

### 2️⃣ PythonAnywhere RESTful API 部署

1. 與上面步驟相同登入 PythonAnywhere
2. 建立新的 Web App，並上傳 `sayhello_api.py` 和 `requirements.txt`
3. 開啟 Bash Console，安裝必要套件：

```bash
pip install --user -r requirements.txt
```

4. 修改 WSGI 檔為：

```python
import sys
path = '/home/你的帳號'
if path not in sys.path:
    sys.path.append(path)

from sayhello_api import app as application
```

5. 點選 Reload，開啟網址查看 API JSON 結果

---

### 3️⃣ AWS Lambda + API Gateway（Zappa）

1. 確保你有安裝 `AWS CLI` 並已設定好 `aws configure`
2. 安裝 Zappa：

```bash
pip install zappa
```

3. 進入 `sayhello_lambda/` 資料夾，初始化 Zappa：

```bash
zappa init
```

4. 部署到 AWS Lambda：

```bash
zappa deploy dev
```

5. 部署成功後，Zappa 會提供一組網址，即可開啟 API

---

### 4️⃣ AWS Elastic Beanstalk

1. 安裝 EB CLI：[官方教學](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html)
2. 初始化專案：

```bash
eb init -p python-3.11 sayhello-eb
```

3. 建立環境並部署：

```bash
eb create sayhello-env
```

4. 完成後輸出網址，瀏覽器開啟即可看到畫面

---

## ✅ 小結比較表

| 平台                    | 架構           | 適合用途       |
| --------------------- | ------------ | ---------- |
| PythonAnywhere 網站     | 傳統 HTML      | 靜態頁面、學習用   |
| PythonAnywhere API    | RESTful JSON | 資料 API 測試用 |
| AWS Lambda (Zappa)    | Serverless   | 小成本 API    |
| AWS Elastic Beanstalk | WSGI App     | 生產環境應用     |

---

## 👨‍🎓 作者

亞洲大學 資訊工程學系
進階程式設計期末報告
指導老師：謝老師
專案製作人：**\[你的名字]**

📂 資料夾：`sayhello_eb`  
📄 [👉 點此查看程式碼](./sayhello_eb/application.py)  
📄 [👉 點此查看 requirements.txt](./sayhello_eb/requirements.txt)  
📄 [👉 點此查看 python.config](./sayhello_eb/.ebextensions/python.config)  


