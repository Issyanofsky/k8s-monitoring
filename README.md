# k8s-monitoring
install Prometheous and Grafana




# locallog to Grafana:

     kubectl port-forward svc/grafana -n monitoring 3000:3000
     http://localhost:3000

 # locallog to Prometheus:

          kubectl port-forward svc/prometheus-service -n monitoring 9090:9090
          http://localhost:9090

     installing Prometheus Operator:
          not done with the yamls (autonatically) i had to run it manualy:

          helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
          helm repo update

          helm install prometheus-operator prometheus-community/kube-prometheus-stack


# for https:
     certificate.yaml (under grafana). create a Certificate using clusterIssuer (existed in the cluster). that's because a secret (with the certificate) 
     cant be read from othe namespace.

check permission of prometheus to scrap:

     kubectl auth can-i list configmaps --as=system:serviceaccount:monitoring:prometheus-sa --namespace=kube-system

varify installation:

     kubectl get crds | grep servicemonitor

# ingress:
     there are ingress roles set to enter to Prometheus and Grafana by HTTPS.
