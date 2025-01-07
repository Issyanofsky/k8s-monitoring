# k8s-monitoring
install Prometheous and Grafana




locallog to Grafana:

     kubectl port-forward svc/grafana -n monitoring 3000:3000
     http://localhost:3000

 locallog to Prometheus:

          kubectl port-forward svc/prometheus-service -n monitoring 9090:9090
          http://localhost:9090


for https:
     certificate.yaml (under grafana). create a Certificate using clusterIssuer (existed in the cluster). that's because a secret (with the certificate) 
     cant be read from othe namespace.

install Prometheus Operator (CRDs):

     kubectl apply -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/main/bundle.yaml


varify installation:

     kubectl get crds | grep servicemonitor

ingress:
     there are ingress roles set to enter to Prometheus and Grafana by HTTPS.
