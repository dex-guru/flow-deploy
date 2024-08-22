```bash
# Set up Kubernetes context for Rancher
kubectl config set-cluster RANCHER_CLUSTER_NAME --server=YOUR_RANCHER_SERVER_URL --insecure-skip-tls-verify=true
kubectl config set-credentials RANCHER_CLUSTER_NAME --token=YOUR_RANCHER_KUBE_CONFIG
kubectl config set-context RANCHER_CLUSTER_NAME --cluster=RANCHER_CLUSTER_NAME --user=RANCHER_USER
kubectl config use-context RANCHER_CLUSTER_NAME

# Add Helm repositories for Redis and PostgreSQL
helm repo add redis https://raw.githubusercontent.com/bitnami/charts/archive-full-index/bitnami
helm repo add postgresql https://raw.githubusercontent.com/bitnami/charts/archive-full-index/bitnami

# Build Helm dependencies
helm dependency build ./helm/contrib-helm-chart

# Install or upgrade the Redash demo Helm chart
helm upgrade --install redash-demo ./helm/contrib-helm-chart --set image.tag=latest --create-namespace --namespace redash-namespace -f ./helm/vars/redash-warehouse-demo.yaml
