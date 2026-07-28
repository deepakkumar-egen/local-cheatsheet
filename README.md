# 🚀 Platform Engineering Workstation & Multi-Cloud Guide

Welcome to the **Platform Engineering Workstation** repository! This repository serves as a complete setup guide, configuration matrix, operational cheat sheet, and environment verification suite for building, managing, and automating cloud-native infrastructure.

---

## 📌 Tooling Inventory

- **Public Cloud CLIs:** AWS CLI v2, Google Cloud SDK (`gcloud`), Azure CLI (`az`)
- **Containerization & Orchestration:** Docker Desktop, `kubectl`, Helm, `kind` (Kubernetes in Docker)
- **Infrastructure as Code (IaC):** HashiCorp Terraform & TFLint
- **Observability & Terminal UI:** `k9s` TUI, `kubectx` / `kubens`, `stern` multi-pod log tailer
- **Runtime Environments:** Python 3.12, Node.js (LTS), Go (Golang)
- **Data & Automation Utilities:** `jq`, `yq`, Git Bash, PowerShell 7

---

## ⚡ Quick Start: SSH Setup & Initial Configuration

Run these commands in **Git Bash** to set up your SSH keys and link your workstation to GitHub:

```bash
# Generate SSH key pair, activate agent, add key, and test GitHub connectivity
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
echo "=== Copy the SSH Public Key below and add it to GitHub Settings -> SSH Keys ==="
cat ~/.ssh/id_ed25519.pub
ssh -T git@github.com
```

# Workstation Validation Suite
## Execute these consolidated script blocks to perform an end-to-end health audit of your workstation's PATHs, tools, cloud endpoints, and container runtimes.

### 1. Automated Terminal PATH Audit
#### Git Bash Environment Check
```bash
tools=("git" "docker" "kubectl" "helm" "terraform" "aws" "gcloud" "az" "kubectx" "stern" "kind" "k9s" "jq" "yq" "python" "go" "node")

echo "=== Git Bash Platform Environment Audit ==="
for tool in "${tools[@]}"; do
    if command -v "$tool" &> /dev/null; then
        echo -e " \033[0;32m[✓]\033[0m $tool -> $(which "$tool")"
    else
        echo -e " \033[0;31m[x]\033[0m $tool NOT found"
    fi
done
```

#### PowerShell System PATH Check
```powershell
$tools = @("git", "docker", "kubectl", "helm", "terraform", "aws", "gcloud", "az", "kubectx", "stern", "kind", "k9s", "jq", "yq", "python", "go", "node")

Write-Host "=== PowerShell Environment Audit ===" -ForegroundColor Cyan
foreach ($t in $tools) {
    $found = Get-Command $t -ErrorAction SilentlyContinue
    if ($found) {
        Write-Host " [✓] $t -> $($found.Source)" -ForegroundColor Green
    } else {
        Write-Host " [X] $t NOT found in PATH" -ForegroundColor Red
    }
}
```

### 2. Runtime, Binary & Cloud Smoke-Test

#### Run this single consolidated bash block in Git Bash to verify binary versions, test public cloud endpoint responsiveness, and perform a local Kubernetes cluster smoke-test:

```bash
# --- A. Check Runtime & Tool Binary Versions ---
echo "=== Runtime & Binary Versions ==="
python --version
go version
node -v
terraform --version
docker --version
kubectl version --client --output=yaml | grep gitVersion
helm version --short
jq --version
yq --version

# --- B. Test Public Cloud Endpoints ---
echo "=== Public Cloud Identity Checks ==="
aws sts get-caller-identity || echo "[!] AWS CLI not configured yet."
gcloud info --format="value(config.account)" || echo "[!] GCP CLI not authenticated yet."
az account show --query name -o tsv || echo "[!] Azure CLI not logged in yet."

# --- C. Local Kubernetes Smoke-Test ---
echo "=== Local Kubernetes (Kind) Test ==="
kind create cluster --name dev-cluster
kubectl get nodes
kubectl cluster-info
kind delete cluster --name dev-cluster
```

## Full Command Reference

For the complete cheat sheet covering Git, Kubernetes, Helm, Terraform, cloud CLIs, Docker, and more, see [PLATFORM_ENGINEERING_COMMANDS.md](PLATFORM_ENGINEERING_COMMANDS.md).

## License & Usage

This repository is maintained for local workstation initialization, platform engineering onboarding, and operational reference. Feel free to adapt and distribute across your organization.