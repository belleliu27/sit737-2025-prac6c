# SIT737 - Task 6.2C: Interacting with Kubernetes

## 🧩 Overview

This task extends Task 6.1P by interacting with the Kubernetes deployment via the CLI and updating the Node.js application in the cluster.

---

## 🔧 Tools Used

- Node.js
- Docker & Docker Hub
- Minikube (Kubernetes)
- kubectl CLI
- Visual Studio Code

---

## ✅ Part I: Interacting with the Cluster

### 1. Get Running Pods & Services

```bash
kubectl get pods
kubectl get services
```

### 2. Port Forward and Access App

```bash
kubectl port-forward service/node-app-service 3000:3000
```

Then go to: [http://localhost:3000](http://localhost:3000)

You should see:
```
Hello from Dockerized App!
```

---

## 🔄 Part II: Updating the Application

### 1. Modify the App

Update `index.js`:

```js
res.send("Updated version: Hello from Kubernetes!");
```

### 2. Build & Push New Image

```bash
docker build -t hellomyjune/sit737-2025-prac6c/node-app:v2 .
docker tag hellomyjune/sit737-2025-prac6c/node-app:v2 hellomyjune/sit737-2025-prac6c:v2
docker push hellomyjune/sit737-2025-prac6c:v2
```

### 3. Update `deployment.yaml`

```yaml
image: hellomyjune/sit737-2025-prac6c:v2
```

### 4. Apply Deployment

```bash
kubectl apply -f deployment.yaml
```

### 5. Confirm New Version

```bash
kubectl get pods
kubectl port-forward service/node-app-service 3000:3000
```

Visit again and check for:
```
Updated version: Hello from Kubernetes!
```

---

## 🗂 Project Files

- `index.js`: Node.js app with update message
- `Dockerfile`: Same setup
- `deployment.yaml`: Now uses `:v2`
- `service.yaml`: Exposes app on port 3000

---

## 🔗 GitHub Repo

[https://github.com/belleliu27/sit737-2025-prac6c](https://github.com/belleliu27/sit737-2025-prac6c)

---

## 👨‍💻 Author 

**Zhaojun Liu**  
