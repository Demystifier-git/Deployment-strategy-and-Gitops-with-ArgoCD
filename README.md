  Deployment Strategies & GitOps with Argo CD

This project is a hands-on lab showing how to deploy and manage a containerized application on Kubernetes the production-ready way.
It covers rolling updates, autoscaling, GitOps with Argo CD, and even canary releases — all the strategies real-world teams use to ship software safely and reliably.

  What You’ll Learn

How to perform zero-downtime rolling updates
Add readiness & liveness probes for self-healing apps
Configure resource requests/limits to enable autoscaling
Use HPA (Horizontal Pod Autoscaler) to scale 2–6 replicas under load
Run load tests with Jobs to simulate traffic
Manage deployments with Argo CD GitOps
Try canary releases for safe, gradual rollouts
(Optional) Use Argo CD Image Updater to auto-deploy new images

Setup Guide

# 1. Clone this repository
git clone https://github.com/Demystifier-git/Deployment-strategy-and-Gitops-with-ArgoCD.git
cd Deployment-strategy-and-Gitops-with-ArgoCD

# 2. Switch to main branch (if needed)
git branch -m master main
git push -u origin main
git push origin --delete master

# 3. Deploy the app
kubectl apply -f kubernetes.yamlfiles/
kubectl get pods
kubectl get svc

# 4. Test a rolling update
kubectl set image deployment/myapp-deployment myapp=demystifier/myapp:2.0
kubectl rollout status deployment/myapp-deployment

# 5. Check autoscaling
kubectl get hpa
kubectl get pods -w

# 6. Deploy with Argo CD
kubectl apply -f argo-app-myapp.yaml -n argocd
kubectl get applications -n argocd

  Scaling Test

Run a 10-minute load generator job
kubectl apply -f load-generator-job.yaml
kubectl get pods
kubectl logs <load-pod-name>
Scaling Behavior

Pods scale up automatically under load

Scale down gracefully when traffic reduces

Jobs clean up automatically after finishing ✅

🔄 GitOps Workflow with Argo CD

Commit & push manifest updates to GitHub

Argo CD detects changes → syncs them to the cluster

Kubernetes applies a rolling update automatically

🐦 Canary Release with Kubernetes

A canary release rolls out a new version gradually:

New version (canary) runs alongside the stable one

Only a small % of traffic goes to the canary

If it’s healthy → increase traffic until it becomes stable

If issues appear → rollback quickly with minimal impact

👉 Think of it like sending a canary bird into a coal mine first — if it survives, the rest follow.

📂 Inside the Repo

stable and canary Deployments

Services to route traffic between versions

Ingress / Istio VirtualService for traffic splitting

Sample app to test version routing


👨‍💻 Author
Delight David
DevOps Engineer | Cloud & Kubernetes Enthusiast
