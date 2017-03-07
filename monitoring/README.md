Monitoring
==========

Example
-------

Prometheus + Grafana 的 `docker-compose.yml`

```yml
prometheus:
  image: prom/prometheus
  ports:
    - 9090:9090
grafana:
  image: grafana/grafana:3.1.0
  ports:
    - 3000:3000
  links:
    - prometheus:prometheus
```

Tools
-----

* [Grafana][]
* [Kibana][]
* [Logstash][]
* [Prometheus][]

[Grafana]: http://grafana.org/
[Kibana]: https://www.elastic.co/products/kibana
[Logstash]: https://www.elastic.co/products/logstash
[Prometheus]: https://prometheus.io/
