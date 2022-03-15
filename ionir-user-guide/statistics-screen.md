# Statistics Screen

Performance data is available at a cluster, namespace, and volume level. Ionir performance monitoring uses Prometheus and Grafana and provides an easy view of the storage performance in the environment.

* Prometheus ([https://prometheus.io/](https://prometheus.io)) is an open-source system monitoring and alerting toolkit that is used to collect Ionir’s performance statistics.
* Grafana ([https://grafana.com/](https://grafana.com)) is an open-source software for time series analytics used to visualize the performance statistics collected By Prometheus.

## Cluster Statistics

To view the cluster performance, click the **Statistics** tab. The window displays three graphs that show the IOPS, Throughput, and Latency of the cluster in the past fifteen (15) minutes.

![](<../.gitbook/assets/Screen Shot 2022-03-15 at 17.52.51.png>)

## Volume Statistics

●      To view the performance of a specific volume, select the namespace and the volume you would like to monitor.

●      To view the performance of another volume in the same namespace, select the volume name from the volumes’ dropdown menu.

●      To view the performance of a volume at another namespace, click the “Cluster” button and select the desired namespace and volume.

●      To go back to the cluster performance view, click the “Cluster” button.

## Performance Monitoring Using Grafana

To view historical performance information or to create customized graphs, use native Grafana. Ionir provides two dashboards in Grafana, one at the cluster level and one at the volume level, that are used in the Ionir Cloud Manage UI.

Both dashboards are available in Grafana and can be accessed either by login to Grafana, or by clicking the “Open in Grafana” button in the performance tab.

Clicking the button while monitoring performance at the cluster level will open the “Ionir - Cluster Performance” dashboard in Grafana.

![](<../.gitbook/assets/Screen Shot 2022-03-15 at 17.53.49.png>)
