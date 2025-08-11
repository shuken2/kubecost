# Kubecost on EKS

This guide describes how to install Kubecost on an Amazon EKS cluster and expose the Web Console over HTTPS using an AWS Application Load Balancer.

## Prerequisites
- EKS cluster (`>=1.26`) with OIDC and AWS Load Balancer Controller enabled
- Namespace `kubecost`
- ACM certificate for `kubecost.jhun80.click`
- IAM role `kubecost-irsa` with Cost Explorer permissions
- Existing Prometheus at `http://prometheus-server.monitoring.svc:80`
- StorageClass `gp2`

## Installation
```bash
helm upgrade -i kubecost oci://public.ecr.aws/kubecost/cost-analyzer \
  --version 2.8.1 -n kubecost \
  -f deploy/kubecost/kubecost.yaml --create-namespace
```

## Access
The Web Console is exposed at `https://kubecost.jhun80.click` via an ALB. Verify by opening the URL in a browser.

## Operations Checklist
- Ensure workloads are labeled with `team`, `env`, and `owner`
- Review Allocation, Assets and Savings dashboards after deployment
- Generate monthly cost reports and prune unused resources
