+++
weight=4
+++


{{< slide template="hamzadark1" >}}

## Jaeger ve Elastic APM Kurulumu

Aşağıda, hem **Jaeger** hem de **Elastic APM** için temel kurulum örneklerini bulabilirsiniz. Bu örnekler, hızlı bir şekilde lokal ortamda çalıştırmak veya test amaçlı yapılandırmak içindir. Üretim ortamına uygun daha detaylı kurulumlar için resmi dokümanları inceleyebilirsiniz.

---

### 1. Jaeger Kurulumu

**Docker Compose** ile Jaeger’i hızlıca çalıştırmak için örnek bir `docker-compose.yml` dosyası:

```yaml{3-14|4|5-6|7-14|8|9|10|11|12|13|14}
version: '3'
services:
  jaeger:
    image: jaegertracing/all-in-one:1.21
    environment:
      - COLLECTOR_ZIPKIN_HOST_PORT=:9411  # Zipkin HTTP endpoint'i için kullanılan port ayarı (9411).
    ports:
      - "16686:16686"  # Jaeger web arayüzü
      - "4317:4317"    # OTLP Collector (gRPC)
      - "4318:4318"    # OTLP Collector (HTTP)
      - "14250:14250"  # Collector (model.proto)
      - "14268:14268"  # Collector (jaeger.thrift)
      - "14269:14269"  # Collector (SPM)
      - "9411:9411"    # Collector (Zipkin)
```

---

### 2. Elastic APM Stack Kurulumu

```yaml{|3-10|4|5|9-10|12-21|13|15-17|16|18-19|23-35|24|26-35|27|29|32-33|33}
version: '3'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.9.0
    container_name: elasticsearch
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
    ports:
      - "9200:9200"

  kibana:
    image: docker.elastic.co/kibana/kibana:8.9.0
    container_name: kibana
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
      - xpack.security.enabled=false
    ports:
      - "5601:5601"
    depends_on:
      - elasticsearch

  apm-server:
    image: docker.elastic.co/apm/apm-server:8.9.0
    container_name: apm-server
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
      - output.elasticsearch.enabled=true
      - output.elasticsearch.hosts=["elasticsearch:9200"]
      - apm-server.secret_token=some_secret_token
      - xpack.security.enabled=false
    ports:
      - "8200:8200"
    depends_on:
      - elasticsearch
```
