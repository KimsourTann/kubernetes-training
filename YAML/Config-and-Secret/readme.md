kubectl create secret acleda-config generic --from-literal name=acleda -o yaml --dry-run=client > ./configmap.yaml 


kubectl create cm acleda-config --from-literal name=acleda -o yaml --dry-run=client > ./configmap.yaml 


kubectl create cm html-file --from-file ./4-configmaps-and-secrets/index.html -o yaml --dry-run=client > ./html-confimap.yaml