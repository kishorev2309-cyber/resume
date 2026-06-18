# ResumeIQ — AI Resume Analyzer

## Project Structure

```
resume-analyzer/
├── public/
│   └── index.html       ← The entire frontend (single file)
├── server.js            ← Express server
├── package.json
└── README.md
```

---

## How to Deploy on Render (Step-by-Step)

### Step 1 — Push to GitHub

1. Create a new GitHub repository (e.g. `resumeiq`)
2. Upload all project files:
   - `public/index.html`
   - `server.js`
   - `package.json`
   - `README.md`

```bash
git init
git add .
git commit -m "Initial commit - ResumeIQ frontend"
git remote add origin https://github.com/YOUR_USERNAME/resumeiq.git
git push -u origin main
```

---

### Step 2 — Create a Render Account

Go to: https://render.com
Sign up with GitHub (recommended — it makes linking repos easier).

---

### Step 3 — Create a New Web Service

1. Click **"New +"** → **"Web Service"**
2. Connect your GitHub account if not already
3. Select your `resumeiq` repository
4. Click **"Connect"**

---

### Step 4 — Configure the Service

Fill in the settings:

| Setting         | Value                    |
|-----------------|--------------------------|
| Name            | `resumeiq` (or any name) |
| Region          | Choose closest to you    |
| Branch          | `main`                   |
| Runtime         | `Node`                   |
| Build Command   | `npm install`            |
| Start Command   | `npm start`              |

---

### Step 5 — Deploy

1. Click **"Create Web Service"**
2. Render will automatically:
   - Pull your code from GitHub
   - Run `npm install`
   - Start the server with `npm start`
3. Wait ~2 minutes for the build to complete

---

### Step 6 — Your site is live!

Render gives you a free URL like:
```
https://resumeiq.onrender.com
```

Every time you push to GitHub, Render auto-deploys the update.

---

## Notes

- The frontend currently runs in **demo mode** (simulated AI response).
- To connect a real backend, point the `fetch()` call in `index.html` to your FastAPI `/analyze` endpoint.
- Free Render tier may sleep after 15 min of inactivity (first load takes ~30s to wake).

---

## Connecting to Your FastAPI Backend (Optional)

When your FastAPI backend is ready, replace the `DEMO_DATA` block in `index.html` with a real API call:

```javascript
async function startAnalysis() {
  showPage('page-analyzing');
  
  const formData = new FormData();
  formData.append('file', fileInput.files[0]);

  const response = await fetch('https://YOUR_BACKEND_URL/analyze', {
    method: 'POST',
    body: formData
  });

  const data = await response.json();
  showResults(data);
}
```

Your FastAPI `/analyze` endpoint should return:
```json
{
  "predicted_role": "Data Science",
  "resume_score": 66.67,
  "skills_found": ["python", "sql", "machine learning"],
  "skills_missing": ["aws", "docker", "tensorflow"],
  "companies": [
    { "name": "Google", "role": "Data Science", "score": 87 }
  ],
  "accuracy": 99.48
}
```
