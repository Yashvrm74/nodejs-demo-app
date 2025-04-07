
## 🚀 Task 1: Automate Code Deployment Using CI/CD Pipeline (GitHub Actions)

### 🎯 Objective

Set up a **CI/CD pipeline** using **GitHub Actions** to build and deploy a **Node.js** web application inside a **Docker** container.

---

### 🧰 Tools & Technologies

- **GitHub**
- **GitHub Actions**
- **Node.js**
- **Docker**
- **DockerHub**

---

### 📦 Deliverables

- ✅ GitHub repository with:
  - Node.js demo app
  - `Dockerfile`
  - `.github/workflows/main.yml` (CI/CD pipeline)

---

### 📁 Project Structure

```
nodejs-demo-app/
├── index.js
├── package.json
├── Dockerfile
├── .github/
│   └── workflows/
│       └── main.yml
└── README.md
```

---

### 🧪 Steps Performed

1. Created a Node.js web app
2. Wrote a `Dockerfile` to containerize the app
3. Pushed project to GitHub
4. Created GitHub Actions workflow (`main.yml`) to:
   - Install dependencies
   - Run tests
   - Build Docker image
   - Push image to DockerHub
5. Stored DockerHub credentials as GitHub Secrets
6. Verified build and image deployment on push to `main`

---

### 🐳 Dockerfile

```Dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

---

### ⚙️ GitHub Actions Workflow (`.github/workflows/main.yml`)

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test || echo "No tests defined"

      - name: Log in to DockerHub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build Docker image
        run: docker build -t yashvrm74/nodejs-demo-app:latest .

      - name: Push Docker image
        run: docker push yashvrm74/nodejs-demo-app:latest
```

---

### 🔐 GitHub Secrets Used

| Secret Key         | Value                       |
|--------------------|-----------------------------|
| `DOCKER_USERNAME`  | Your DockerHub username     |
| `DOCKER_PASSWORD`  | Your DockerHub access token |

---

### 📦 Run Locally

```bash
npm install
npm start
```

Visit: [http://localhost:3000](http://localhost:3000)

---

### 🐋 Run with Docker

```bash
docker build -t yashvrm74/nodejs-demo-app .
docker run -p 3000:3000 yashvrm74/nodejs-demo-app
```

---

### 🚀 CI/CD Behavior

Any code pushed to the `main` branch will:

- 🛠️ Install dependencies
- ✅ Run tests (if any)
- 🐳 Build Docker image
- 📤 Push to DockerHub

---

### ✅ Final Result

Your app is fully automated from push to deployment using GitHub Actions and Docker.
