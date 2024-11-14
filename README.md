README


After the creation of the VM on Openstack with the good configurations, I resize the VM with growpart and resize2fs (because not automatically done).


- In the first step we have to create a kubernetes cluster to deploy a single-node cluster with the command "kind create cluster".

Then I deploy Nginx service thanks to yaml files that will configure the deployment by applying files with command "kubectl apply -f". Nginx service has to be exposed on port 80 inside the cluster and port 30080 outside the cluster. I configure that inside nginx-config/deployment/service.yaml files.


- Then I configure prometheus exporter on port 9113 and the IP of nginx thanks via prometheus-deployment.yaml file and prometheus-service.yaml file.

- After that I install helm and create a space named monitoring and I depploy prometheus using helm. To do that I install prometheus in the monitoring space and port-forward prometheus on port 9090.

- Then I create a ssh bridge between the two VM (openstack one and the one in which we work) on port 12345.

- After that I configure firefox proxy on manual and in the SOCKS5 protocol add localhost for adress part and port 12345 to use the bridge created before.

- Before connecting to prometheus via "localhost:9090" on firefox I modify values.yaml file that configure prometheus to add nginx service to it. After that I can connect to prometheus and see nginx in the targets.

- Finally, I install grafana same way I install prometheus with helm in the monitoring space and port-forward grafana on port 3000. So I can connect to grafana when I write "localhost:3000" on firefox via username and password I can get thanks to kubernetes. Then I configure grafana by adding prometheus data source to it (json file), configure the dashboard and try DoS attack to see how the server behave. 



