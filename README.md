---

# 🚀 Deploy Flask App to Google Cloud Run with GitHub Actions

This repo contains a **Flask app (`app.py`)** with **`requirements.txt`** and **`Dockerfile`**, deployed automatically to **Google Cloud Run** using **GitHub Actions**.

---

## 📂 Project Structure

```
.
├── app.py
├── requirements.txt
├── Dockerfile
└── .github/
    └── workflows/
        └── deploy.yml
```

---

## 🔑 Required GitHub Secrets

Go to your repo → **Settings → Secrets and variables → Actions** → **New repository secret** and add:

| Secret Name  | Value                                                                                           |
| ------------ | ----------------------------------------------------------------------------------------------- |
| `GCP_SA_KEY` | Contents of your GCP service account JSON key (with Cloud Run + Artifact Registry permissions). |

---

## ⚙️ Replace Placeholders in Workflow

In `.github/workflows/deploy.yml`, replace the following:

* **`PROJECT_ID`** → Your Google Cloud project ID (example: `my-gcp-project`)
* **`REGION`** → Deployment region (example: `us-central1`)
* **`REPO_NAME`** → Artifact Registry repository name (example: `my-docker-repo`)
* **`SERVICE_NAME`** → Cloud Run service name (example: `flask-service`)

---

## 📝 Example Configuration

```yaml
IMAGE="us-central1-docker.pkg.dev/my-gcp-project/my-docker-repo/flask-service:latest"

gcloud run deploy flask-service \
  --image $IMAGE \
  --region us-central1 \
  --platform managed \
  --allow-unauthenticated
```

---

## 🚀 Deployment Flow

1. Push to **main** branch
2. GitHub Actions workflow runs:

   * Authenticates with GCP
   * Builds Docker image from `Dockerfile`
   * Pushes image to Artifact Registry
   * Deploys to Cloud Run

---

## 🌐 Access Your Service

After deployment, you’ll get a public URL from Cloud Run. Example:

```
https://flask-service-xyz123-uc.a.run.app
```

