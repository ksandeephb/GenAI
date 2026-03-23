
# 🚀 Streamlit App Deployment on Azure Web App (No Docker)

## 📌 Overview

This guide explains how to deploy and run a **basic Streamlit application** on **Azure Web App (Linux, code-based deployment)** without using Docker.

This setup is ideal for:

* MVPs
* Internal tools
* Quick demos

---

## 🧰 Prerequisites

* Azure Subscription
* Azure Web App created with:

  * OS: **Linux**
  * Runtime: **Python 3.10 or 3.11**
* Basic knowledge of deployment (ZIP / VS Code)

---

## 📁 Project Structure

Ensure your files are at the **root level**:

```
app.py
requirements.txt
```

❌ Do NOT place files inside a folder
❌ Do NOT zip the parent folder

---

## 📝 Create a Minimal Streamlit App

### `app.py`

```python
import streamlit as st

st.title("Streamlit test on Azure 🚀")
```

### `requirements.txt`

```txt
streamlit
```

---

## 🚀 Deployment Methods

### ✅ Option 1: ZIP Deploy (Recommended)

1. Select `app.py` and `requirements.txt`
2. Create a ZIP file:

   ```
   app.zip
   ```
3. Go to Azure Portal → **Web App**
4. Navigate to **Deployment Center → ZIP Deploy**
5. Upload `app.zip`

---

### ✅ Option 2: VS Code Deployment

* Right-click project folder → **Deploy to Web App**

---

## ⚙️ Azure Configuration

### 🔹 1. Add Environment Variable

Go to:
**Web App → Configuration → Environment variables**

Add:

| Name                           | Value |
| ------------------------------ | ----- |
| SCM_DO_BUILD_DURING_DEPLOYMENT | true  |

👉 This ensures Azure installs dependencies from `requirements.txt`

Click **Save** and **Restart**

---

### 🔹 2. Set Startup Command

Go to:
**Configuration → General settings**

Set:

```bash
python -m streamlit run app.py --server.port 8000 --server.address 0.0.0.0
```

⚠️ Important:

* Use `python -m streamlit` (NOT `streamlit run`)
* Use port **8000** (required by Azure)
* Use `0.0.0.0` for external access

Click **Save**

---

## 🔁 Redeploy the App

After setting the environment variable:

* Redeploy your app (ZIP / VS Code / GitHub)

⚠️ Azure installs dependencies **only during deployment**, not restart

---

## ✅ Verify Deployment

### 🔹 Check Logs

Go to:
**Web App → Log Stream**

Expected logs:

```
Collecting streamlit
Installing collected packages: streamlit
Running on http://0.0.0.0:8000
```

---

### 🔹 Open the App

```
https://<your-app-name>.azurewebsites.net
```

You should see:

```
Streamlit test on Azure 🚀
```

---

## 🛠️ Troubleshooting

### ❌ Error: `streamlit: not found`

✔️ Fix:

```bash
python -m streamlit run app.py ...
```

---

### ❌ Error: Container did not start (230s timeout)

✔️ Check:

* Startup command
* Port = 8000
* Dependencies installed

---

### ❌ Dependencies not installed

✔️ Ensure:

* `requirements.txt` is at root
* `SCM_DO_BUILD_DURING_DEPLOYMENT = true`
* Redeploy app

---

### ❌ Files not found

Check using Kudu:

```
/home/site/wwwroot
```

---

## 🔍 Debug with Kudu

1. Go to **Advanced Tools (Kudu)**
2. Open **Debug Console → Bash**
3. Run:

```bash
ls /home/site/wwwroot
```

---

## 🔐 Security Notes

* Safe for testing and MVP use
* Azure handles HTTPS (port 443)
* Port 8000 is internal only
* Optional:

  * Add IP restrictions
  * Stop app after testing

---

## 🧠 How It Works

```
User → HTTPS (443)
      ↓
Azure Web App (Reverse Proxy)
      ↓
Streamlit App (Port 8000 internally)
```

---

## ✅ Final Checklist

* [ ] Linux Web App
* [ ] Python 3.10+
* [ ] `app.py` at root
* [ ] `requirements.txt` at root
* [ ] Startup command set correctly
* [ ] Port = 8000
* [ ] Environment variable added
* [ ] App redeployed

---

## 🚀 Next Steps

* Add bot catalog UI (`bots.json`)
* Add search and filters
* Add authentication (optional)
* Move to container-based deployment for production

---

## 📌 Conclusion

You can successfully run a Streamlit app on Azure Web App without Docker by:

* Setting the correct startup command
* Ensuring dependencies are installed
* Using Azure-compatible configuration

This approach is best for **quick deployments and testing**, with flexibility to scale later.
