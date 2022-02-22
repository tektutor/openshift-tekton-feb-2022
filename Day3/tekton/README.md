# Tekton

## Tekton CI/CD Pipeline
- Tekton is an opensource knative application that helps you create CI/CD 
  pipeline within Kubernetes/OpenShift cluster.
- Tekton supports both Kubernetes and OpenShift

## Installing Tekton within OpenShift Cluster
- From the OpenShift web console, switch to Administrator view and select Operators --> Operators Hub 
  and search for "Red Hat OpenShift Pipelines" and install it.

## Installing Tekton CLI tool
```
sudo dnf copr enable chmouel/tektoncd-cli
sudo dnf install tektoncd-cli
```

## Tekton Jargons
Custom Resources added by Tekton project to your OpenShift Cluster
- Step
   - does one activity
- Task
   - is a list of steps executed either sequentially or parallely
- TaskRun
- Pipeline
- PipelineRun 
