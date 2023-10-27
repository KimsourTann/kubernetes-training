kubectl autoscale deploy microservice --cpu=30 

kubectl create deploy microservice --image nj93/k8s-demo-container:latest --port 8080 -o yaml --dry-run > ./hpa.yaml