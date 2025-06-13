# 亞洲大學進階程式設計期末作業
# 🌍 SayHello Flask 

這是一個基於 Flask 的簡單應用範例，展示如何將同一個應用部署到四種平台：
- PythonAnywhere 靜態網站
- PythonAnywhere RESTful API
- AWS Lambda + API Gateway（透過 Zappa）
- AWS Elastic Beanstalk

---

## 📁 專案結構
sayhello-flask/
├── sayhello_web/ → Flask 網站
├── sayhello_api/ → Flask RESTful API
├── sayhello_lambda/ → AWS Lambda (Zappa)
├── sayhello_eb/ → Elastic Beanstalk 應用
└── README.md → 本說明文件

---

## 1️⃣ Flask Website on PythonAnywhere

這是一個傳統 HTML 輸出頁面，部署到 PythonAnywhere。

📄 [查看程式碼](./sayhello_web/sayhello_web.py)

### 步驟摘要：

1. 登入 [PythonAnywhere](https://www.pythonanywhere.com/)
2. 上傳 `sayhello_web.py`
3. 設定 Web App，修改 `WSGI` 檔案：
   ```python
   from sayhello_web import app as application
2️⃣ RESTful API on PythonAnywhere
使用 flask-restful 建立一個簡單的 API，返回 JSON 格式。

📄 查看程式碼
📦 需求檔
3️⃣ Flask API on AWS Lambda (Zappa)
這個範例展示如何將 Flask API 部署為 AWS Lambda 函數，搭配 API Gateway。

📄 查看程式碼
📦 需求檔
⚙️ Zappa 設定
4️⃣ Flask App on AWS Elastic Beanstalk
這是一個部署到 AWS Elastic Beanstalk 的 Flask App，適合長期營運。

📄 查看程式碼
📦 需求檔

可選設定：
🛠 .ebextensions 設定
📚 小結
| 平台                    | 架構           | 適合用途       |
| --------------------- | ------------ | ---------- |
| PythonAnywhere 網站     | 傳統 HTML      | 靜態頁面、學習用   |
| PythonAnywhere API    | RESTful JSON | 資料 API 測試用 |
| AWS Lambda (Zappa)    | Serverless   | 小成本 API    |
| AWS Elastic Beanstalk | WSGI App     | 生產環境應用     |
