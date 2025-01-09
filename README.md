# k8s-monitoring
install Prometheous and Grafana




# locallog to Grafana:
the helm for Grafana is in folder "grafana".

     kubectl port-forward svc/grafana -n monitoring 3000:3000
     http://localhost:3000

setting Prometheus Data Source in Grafana:
     since the loging to Prometheus is open to HTTPS (outside). on adding Prometheus Data source the setting is:
     - URL - set this URL in the URL field http://prometheus-service.monitoring.svc.cluster.local:9090 
     - GET - set HTTP Method set to "GET".

 # locallog to Prometheus:
 the helm for Promrtheus is in folder "prometheus-ol1".

          kubectl port-forward svc/prometheus-service -n monitoring 9090:9090
          http://localhost:9090

     installing Prometheus Operator:
          not done with the yamls (autonatically) i had to run it manualy:

          kubectl create -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/master/bundle.yaml

     for allowing Prometheus to scrap metrics from rhe kubletAPI i added the The flag --authentication-token-webhook=true to the
     kubeadm-flags.env:
          * loged to control plane (ssh).
          * sudo nano /var/lib/kubelet/kubeadm-flags.env
          * add a line: KUBELET_KUBEADM_ARGS="--authentication-token-webhook=true"
          * to reload the setting:
                    sudo systemctl daemon-reload
                    sudo systemctl restart kubelet

          

# for https:
     certificate.yaml (under grafana). create a Certificate using clusterIssuer (existed in the cluster). that's because a secret (with the certificate) 
     cant be read from othe namespace.

check permission of prometheus to scrap:

     kubectl auth can-i list configmaps --as=system:serviceaccount:monitoring:prometheus-sa --namespace=kube-system

varify installation:

     kubectl get crds | grep servicemonitor

# ingress:
     there are ingress roles set to enter to Prometheus and Grafana by HTTPS.
