# GitHub Actions — CI/CD Pipeline

This project demonstrates a complete CI/CD pipeline built with **GitHub Actions**, based on the [GitHub Actions Zero to Hero](https://www.youtube.com/playlist?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa) series by Abhishek Veeramalla.

---

## 📁 Project Structure

```
github-actions/
├── .github/
│   └── workflows/
│       ├── ci.yml              # CI pipeline with matrix strategy (GitHub-hosted runners)
│       └── self-hosted.yml     # Pipeline using a self-hosted runner (EC2/VM)
├── src/
│   └── addition.py             # Python app with basic math operations
├── tests/
│   └── test_addition.py        # Unit tests using pytest
├── requirements.txt
└── README.md
```

---

## ⚙️ Workflows

### 1. CI Pipeline (`ci.yml`)
- Triggers on `push` to `main`/`develop` and on `pull_request`
- Runs tests in **parallel across Python 3.8, 3.9, and 3.10** using a matrix strategy
- Installs dependencies, runs `pytest` with coverage, and uploads a coverage artifact

### 2. Self-Hosted Runner Pipeline (`self-hosted.yml`)
- Runs on a **self-hosted runner** (e.g., an EC2 instance or local VM)
- Demonstrates how to configure and use your own runner instead of GitHub-hosted machines
- Matrix strategy across Python 3.8 and 3.9

---

## 🔑 Key Concepts Covered

| Concept | Description |
|---|---|
| `on: push / pull_request` | Event-driven workflow triggers |
| `strategy: matrix` | Parallel jobs across multiple Python versions |
| `runs-on: ubuntu-latest` | GitHub-hosted runner |
| `runs-on: self-hosted` | Custom runner on your own infrastructure |
| `actions/checkout@v3` | Checkout source code in the runner |
| `actions/setup-python@v4` | Set up a specific Python version |
| `upload-artifact` | Save test coverage reports as artifacts |
| `pytest --cov` | Run tests with coverage reporting |

---

## 🚀 How to Run Locally

```bash
# Clone the repo
git clone https://github.com/aqib2742k/github-actions.git
cd github-actions

# Install dependencies
pip install -r requirements.txt

# Run tests
pytest tests/ -v
```

---

## 🆚 GitHub Actions vs Jenkins

| Feature | GitHub Actions | Jenkins |
|---|---|---|
| Hosting | GitHub-managed (no server needed) | Self-hosted (you manage the server) |
| Setup | Zero config — lives in `.github/workflows/` | Requires Jenkins installation & plugins |
| Cost | Free for public repos | Free software, but server costs apply |
| Integration | Native GitHub events (push, PR, issues) | Webhook-based, more manual wiring |
| Best for | GitHub-native projects, open source | Enterprise, complex multi-stage pipelines |

---

## 📌 Self-Hosted Runner Setup (EC2)

To register your own runner:

```bash
# On your EC2 instance or VM:
mkdir actions-runner && cd actions-runner
curl -o actions-runner-linux-x64-2.x.x.tar.gz -L https://github.com/actions/runner/releases/download/...
tar xzf ./actions-runner-linux-x64-2.x.x.tar.gz
./config.sh --url https://github.com/YOUR_USERNAME/YOUR_REPO --token YOUR_TOKEN
./run.sh
```

Then in your workflow, set `runs-on: self-hosted`.
