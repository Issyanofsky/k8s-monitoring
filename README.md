# k8s-monitoring
install Prometheous and Grafana


ingress yaml are bak (not deploying) because i add the setting into a Application running on Argo-cd.

locallog to Grafana:

     kubectl port-forward svc/grafana -n monitoring 3000:3000
     http://localhost:3000

 locallog to Prometheus:

          kubectl port-forward svc/prometheus -n monitoring 9090:9090
          http://localhost:9090


for https:
     certificate.yaml (under grafana). create a Certificate using clusterIssuer (existed in the cluster) 
