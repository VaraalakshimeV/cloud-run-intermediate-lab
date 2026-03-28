# Cloud Run Intermediate Lab - GitHub Events Explorer

## Overview
A containerized Flask application deployed on Google Cloud Run that interacts with **Google Cloud Storage** and **BigQuery**. The app explores GitHub event data from the `githubarchive` public dataset.

## Endpoints

| Endpoint | Description |
|----------|-------------|
| `/` | Welcome message with available endpoints |
| `/upload` | Uploads a sample report file to Cloud Storage |
| `/query` | Returns top 10 GitHub event types (Jan 1, 2024) |
| `/summary` | Returns event summary with unique user counts |

## Tech Stack
- **Python 3.10** with Flask
- **Google Cloud Run** (serverless deployment)
- **Google Cloud Storage** (file upload)
- **Google BigQuery** (public dataset queries)
- **Docker** (containerization)

## Project Structure
```
cloud-run-intermediate-app/
├── app.py              # Flask application
├── requirements.txt    # Python dependencies
├── Dockerfile          # Container configuration
└── README.md
```

## Setup & Deployment

### Prerequisites
- Google Cloud account with billing enabled
- Google Cloud SDK installed
- Docker installed

### 1. Enable GCP APIs
- Cloud Run API
- Cloud Storage API
- BigQuery API

### 2. Create GCP Resources
- Cloud Storage Bucket
- Service Account with **Storage Admin** and **BigQuery User** roles

### 3. Build & Push Docker Image
```bash
docker build -t gcr.io/YOUR_PROJECT_ID/cloud-run-intermediate-app .
gcloud auth configure-docker
docker push gcr.io/YOUR_PROJECT_ID/cloud-run-intermediate-app
```

### 4. Deploy to Cloud Run
```bash
gcloud run deploy cloud-run-intermediate-service \
  --image gcr.io/YOUR_PROJECT_ID/cloud-run-intermediate-app \
  --region us-central1 \
  --platform managed \
  --allow-unauthenticated \
  --update-env-vars BUCKET_NAME=YOUR_BUCKET_NAME \
  --service-account YOUR_SERVICE_ACCOUNT_EMAIL
```

### 5. Test Endpoints
```bash
curl https://YOUR_SERVICE_URL/
curl https://YOUR_SERVICE_URL/upload
curl https://YOUR_SERVICE_URL/query
curl https://YOUR_SERVICE_URL/summary
```

## Clean Up
```bash
gcloud run services delete cloud-run-intermediate-service --region us-central1
gsutil rm -r gs://YOUR_BUCKET_NAME
gcloud container images delete gcr.io/YOUR_PROJECT_ID/cloud-run-intermediate-app --force-delete-tags
gcloud iam service-accounts delete YOUR_SERVICE_ACCOUNT_EMAIL
<img width="1903" height="683" alt="image" src="https://github.com/user-attachments/assets/029976be-d685-4866-8247-94446531f983" />
<img width="1919" height="911" alt="image" src="https://github.com/user-attachments/assets/291d9215-f11a-4466-8ba1-e84cdbc05d11" />
<img width="1919" height="769" alt="image" src="https://github.com/user-attachments/assets/fe1fbc00-a028-42d8-be29-67b118e293da" />
<img width="1919" height="780" alt="image" src="https://github.com/user-attachments/assets/b4f57ab6-9dcb-4824-a701-b5b344ae7c55" />

```

## Author
Varaalakshime Vigneswara Pandiarajan  
MS Data Analytics Engineering, Northeastern University
