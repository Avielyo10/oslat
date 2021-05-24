# oslat

OS latency tool

## Deployment
```bash
pip3 install jinja2-tools --user
jinja render -e duration=1h -e cpu=16 \
  -e profile_name=$(oc get performanceprofile -o jsonpath='{.items[0].metadata.name}') \
  -e cnf_node_selector=worker-cnf \
  -e kubernetes_hostname=$(oc get node -l kubernetes.io/hostname -o name | awk -F '/' '{print $2}') -t ./pod.j2 -o pod.yaml
oc apply -f performanceprofile.yaml
# ... Wait for mcp to complete updating the nodes ...
oc apply -f pod.yaml
```
