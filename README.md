# flow-deploy

kubectl config set-cluster RANCHER_CLUSTER_NAME --server=YOURE_RANCHER_SERVER_URL --insecure-skip-tls-verify=true
kubectl config set-credentials RANCHER_CLUSTER_NAME --token=YOUR_RANCHER_KUBE_CONFIG
kubectl config set-context RANCHER_CLUSTER_NAME --cluster=RANCHER_CLUSTER_NAME --user=RANCHER_USER
kubectl config use-context RANCHER_CLUSTER_NAME

helm repo add redis https://raw.githubusercontent.com/bitnami/charts/archive-full-index/bitnami
helm repo add postgresql https://raw.githubusercontent.com/bitnami/charts/archive-full-index/bitnami
helm dependency build ./helm/contrib-helm-chart
helm upgrade -install redash-demo ./helm/contrib-helm-chart --set image.tag=latest --create-namespace --namespace redash-namespace -f ./helm/vars/redash-warehouse-demo.yaml