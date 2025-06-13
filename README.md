# 🏁 亞洲大學進階程式設計期末作業  
## 🐍 SayHello Flask

這是一個基於 Flask 的簡單應用範例，展示如何將同一個應用部署到四個平台：

- PythonAnywhere 靜態網站  
- PythonAnywhere RESTful API  
- AWS Lambda + API Gateway（透過 Zappa）  
- AWS Elastic Beanstalk  

---

## 📁 專案結構
## 2️⃣ PythonAnywhere RESTful API  
📂 資料夾：`sayhello_api`  
📄 [👉 點此查看程式碼](./sayhello_api/sayhello_api.py)  
📄 [👉 點此查看 requirements.txt](./sayhello_api/requirements.txt)  

---

## 3️⃣ AWS Lambda (Zappa)  
📂 資料夾：`sayhello_lambda`  
📄 [👉 點此查看程式碼](./sayhello_lambda/sayhello_lambda.py)  
📄 [👉 點此查看 requirements.txt](./sayhello_lambda/requirements.txt)  
📄 [👉 點此查看 zappa_settings.json](./sayhello_lambda/zappa_settings.json)  

---

## 4️⃣ AWS Elastic Beanstalk  
📂 資料夾：`sayhello_eb`  
📄 [👉 點此查看程式碼](./sayhello_eb/application.py)  
📄 [👉 點此查看 requirements.txt](./sayhello_eb/requirements.txt)  
📄 [👉 點此查看 python.config](./sayhello_eb/.ebextensions/python.config)  


