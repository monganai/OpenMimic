# OpenMimic
Imitate an openmetrics/prometheus endpoint for replication 


##  How to use

1 - Install the pip requirments: `pip3 install -r requirements.txt` 

2 - Obtain a snapshot of the endpoint you wish to mimic, and save it in the directory as `desired_output.txt` [See Below]

3 - Run the flask server: `python3 openmimic.py`

4 - `localhost:8888/metrics` will now expose the contents of `desired_output.txt`




## Obtaining a snapshot of an endpoint.

Openmetrics/promethues based endpoints expose metrics in a specific prometheus format:
https://github.com/OpenObservability/OpenMetrics

```
# HELP kong_bandwidth Total bandwidth in bytes consumed per service/route in Kong
# TYPE kong_bandwidth counter
kong_bandwidth{type="egress",service="google"} 1277
...
...
...
kong_bandwidth{type="egress",service="yahoo"} 297
```

To take a snapshot of these metrics, once can `curl` the endpoint where they are actively exposed, and save it as a file.
For use with OpenMimic, this could looks like `curl <ip_of_my_service>:<port>/<route> >> desired_output.txt`
A metric collector (such as any openmetrics based Datadog integration) could then be configured to point at the OpenMimic endpoint for live testing of configurations. 





```
init_config:

instances:
  - openmetrics_endpoint: http://localhost:8888/metrics/
 
```
