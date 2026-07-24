# 🛠️ Platform Engineering Complete Terminal Cheat Sheet

A comprehensive reference matrix for Git Workflows, Kubernetes Operations, Infrastructure as Code, Public Cloud CLIs, Containerization, and Runtime Environments.

---

## 📌 Table of Contents
- [1. Git Version Control & SSH Setup](#1-git-version-control--ssh-setup)
- [2. Kubernetes CLI (`kubectl`)](#2-kubernetes-cli-kubectl)
- [3. Kubernetes Context & Observability (`kubectx`, `k9s`, `stern`)](#3-kubernetes-context--observability-kubectx-k9s-stern)
- [4. Helm Package Manager](#4-helm-package-manager)
- [5. Local Kubernetes Clusters (`kind`)](#5-local-kubernetes-clusters-kind)
- [6. Infrastructure as Code (`terraform`)](#6-infrastructure-as-code-terraform)
- [7. Amazon Web Services (`aws`)](#7-amazon-web-services-aws)
- [8. Google Cloud Platform (`gcloud`)](#8-google-cloud-platform-gcloud)
- [9. Microsoft Azure (`az`)](#9-microsoft-azure-az)
- [10. Container Engine (`docker`)](#10-container-engine-docker)
- [11. Data Processing Utilities (`jq` & `yq`)](#11-data-processing-utilities-jq--yq)
- [12. Programming Runtimes (Python & Node.js)](#12-programming-runtimes-python--nodejs)

---

## 1. Git Version Control & SSH Setup

### SSH Key Configuration
| Task | Command |
| :--- | :--- |
| **Generate SSH Key** | `ssh-keygen -t ed25519 -C "your_email@example.com"` |
| **Start Agent & Add Key** | `eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519` |
| **Copy Public Key** | `cat ~/.ssh/id_ed25519.pub` |
| **Test GitHub SSH** | `ssh -T git@github.com` |

### Core Git Operations
| Task | Command |
| :--- | :--- |
| **Initialize New Repo** | `git init -b main` |
| **Link Remote SSH Repo** | `git remote add origin git@github.com:USERNAME/REPO.git` |
| **Clone Repository** | `git clone git@github.com:USERNAME/REPO.git` |
| **Create Feature Branch** | `git checkout -b feature/my-feature` |
| **Stage & Commit Changes** | `git add . && git commit -m "feat: description"` |
| **Push Branch to Remote** | `git push -u origin feature/my-feature` |
| **Rebase Main Changes** | `git pull origin main --rebase` |
| **Check Log History** | `git log --oneline --graph -n 10` |

---

## 2. Kubernetes CLI (`kubectl`)

| Task | Command |
| :--- | :--- |
| **Check Cluster Connection** | `kubectl cluster-info` |
| **List All Namespaces** | `kubectl get ns` |
| **List Pods (All Namespaces)**| `kubectl get pods -A` |
| **List Pods with IPs & Nodes**| `kubectl get pods -n <namespace> -o wide` |
| **Describe Pod Events** | `kubectl describe pod <pod-name> -n <namespace>` |
| **Stream Live Pod Logs** | `kubectl logs -f <pod-name> -n <namespace>` |
| **Port Forwarding** | `kubectl port-forward pod/<pod-name> 8080:80 -n <namespace>` |
| **Execute Shell in Pod** | `kubectl exec -it <pod-name> -n <namespace> -- /bin/sh` |
| **Apply Manifest File** | `kubectl apply -f manifest.yaml` |
| **Delete Resource** | `kubectl delete -f manifest.yaml` |

---

## 3. Kubernetes Context & Observability (`kubectx`, `k9s`, `stern`)

| Tool | Task | Command |
| :--- | :--- | :--- |
| **`kubectx`** | List All K8s Contexts | `kubectx` |
| **`kubectx`** | Switch Active Context | `kubectx <cluster-name>` |
| **`k9s`** | Launch Interactive Terminal UI | `k9s` |
| **`k9s`** | Launch K9s in Specific Namespace | `k9s -n <namespace>` |
| **`stern`** | Stream Logs for Matching Pods | `stern <pod-prefix> -n <namespace>` |
| **`stern`** | Tail All Pod Logs (Last 15m) | `stern .* --since 15m` |

---

## 4. Helm Package Manager

| Task | Command |
| :--- | :--- |
| **Add Chart Repository** | `helm repo add <repo-name> <repo-url>` |
| **Update Chart Repositories** | `helm repo update` |
| **Search Chart Registry** | `helm search repo <keyword>` |
| **List Installed Releases** | `helm list -A` |
| **Install Chart** | `helm install <release> <repo>/<chart> -n <ns> --create-namespace` |
| **Idempotent Apply/Upgrade** | `helm upgrade --install <release> <chart> -f values.yaml -n <ns>` |
| **Rollback Release** | `helm rollback <release> <revision-number> -n <ns>` |
| **Uninstall Release** | `helm uninstall <release> -n <ns>` |

---

## 5. Local Kubernetes Clusters (`kind`)

| Task | Command |
| :--- | :--- |
| **Create Local K8s Cluster** | `kind create cluster --name dev-cluster` |
| **List Running Kind Clusters**| `kind get clusters` |
| **Direct `kubectl` to Kind** | `kubectl cluster-info --context kind-dev-cluster` |
| **Destroy Local Cluster** | `kind delete cluster --name dev-cluster` |

---

## 6. Infrastructure as Code (`terraform`)

| Task | Command |
| :--- | :--- |
| **Initialize Workspace** | `terraform init` |
| **Format Code Recursively** | `terraform fmt -recursive` |
| **Validate Code Logic** | `terraform validate` |
| **Generate Execution Plan** | `terraform plan -out=tfplan.binary` |
| **Apply Planned State** | `terraform apply tfplan.binary` |
| **Destroy Infrastructure** | `terraform destroy` |
| **List Tracked Resources** | `terraform state list` |
| **Display Current State** | `terraform show` |
| **View Output Variables** | `terraform output` |

---

## 7. Amazon Web Services (`aws`)

| Task | Command |
| :--- | :--- |
| **Verify AWS Credentials** | `aws sts get-caller-identity` |
| **Configure Interactive SSO**| `aws configure sso` |
| **List S3 Buckets** | `aws s3 ls` |
| **Update EKS `kubectl` Config**| `aws eks update-kubeconfig --region <region> --name <cluster-name>` |
| **Describe EC2 Instances** | `aws ec2 describe-instances` |

---

## 8. Google Cloud Platform (`gcloud`)

| Task | Command |
| :--- | :--- |
| **Browser Login** | `gcloud auth login` |
| **Set Active Project** | `gcloud config set project <project-id>` |
| **Update GKE `kubectl` Config**| `gcloud container clusters get-credentials <cluster> --region <region>` |
| **List Active Instances** | `gcloud compute instances list` |

---

## 9. Microsoft Azure (`az`)

| Task | Command |
| :--- | :--- |
| **Browser Login** | `az login` |
| **List Subscriptions** | `az account list --output table` |
| **Set Active Subscription** | `az account set --subscription <sub-id>` |
| **Update AKS `kubectl` Config**| `az aks get-credentials --resource-group <rg> --name <cluster-name>` |

---

## 10. Container Engine (`docker`)

| Task | Command |
| :--- | :--- |
| **List Running Containers** | `docker ps` |
| **List All Containers** | `docker ps -a` |
| **List Cached Local Images** | `docker images` |
| **Build Docker Image** | `docker build -t <image-name>:<tag> .` |
| **Run Container (Detached)** | `docker run -d -p 8080:80 --name web <image-name>` |
| **Open Shell in Container** | `docker exec -it <container-id> /bin/sh` |
| **Clean Unused Docker Assets**| `docker system prune -a --volumes` |

---

## 11. Data Processing Utilities (`jq` & `yq`)

| Tool | Task | Command |
| :--- | :--- | :--- |
| **`jq`** | Extract Single Key | `kubectl get pod <pod> -o json \| jq '.status.phase'` |
| **`jq`** | Map Array to Plain List | `kubectl get pods -o json \| jq '.items[].metadata.name'` |
| **`jq`** | Filter AWS Instance IDs | `aws ec2 describe-instances \| jq '.Reservations[].Instances[].InstanceId'` |
| **`yq`** | Extract Image from Deployment | `yq eval '.spec.template.spec.containers[0].image' deployment.yaml` |

---

## 12. Programming Runtimes (Python & Node.js)

### Python Virtual Environment
| Task | Command |
| :--- | :--- |
| **Create Virtual Environment**| `python -m venv .venv` |
| **Activate Environment (Git Bash)** | `source .venv/Scripts/activate` |
| **Install Requirements** | `pip install -r requirements.txt` |
| **Deactivate Environment** | `deactivate` |

### Node.js & Package Managers
| Task | Command |
| :--- | :--- |
| **Check Runtime Versions** | `node -v && npm -v` |
| **Install Project Dependencies**| `npm install` |
| **Enable Corepack & Check Yarn**| `corepack enable && yarn --version` |