# File System Upload App v1

This is the first version of the file system upload/download/delete application.

Features:
- Upload files
- View uploaded files
- Download files
- Delete files
- Backend API endpoints for file management
- Docker-ready container
- Jenkins pipeline for CI/CD
- Kubernetes deployment manifest

## Local run

```bash
npm install
npm start
```

Open:
- http://localhost:3000

## Docker

```bash
docker build -t file-system-upload-v1:v1 .
docker run -p 3000:3000 file-system-upload-v1:v1
```

## Jenkins

Use the included `Jenkinsfile` in a Jenkins pipeline job.

## Kubernetes

```bash
kubectl apply -f k8s/deployment.yaml
```

Then access via localhost using the NodePort:
- http://localhost:30080

## API

- `POST /api/upload` Upload a file
- `GET /api/files` List files
- `GET /api/files/:filename` Download a file
- `DELETE /api/files/:filename` Delete a file
