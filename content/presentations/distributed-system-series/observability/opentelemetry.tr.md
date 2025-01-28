+++
weight=2
+++

{{% section %}}

{{< slide template="darkslide3" >}}

### OpenTelemetry Nedir?

- **Open** açık kaynak olmasını, **Tele** uzaktan yapabilmesini ve **Metry** (**Metron**) ölçümü temsil eder. Bir gözlemlenebilirlik (observability) framework’üdür

- **Log**, **trace** ve **metrics** verilerini **platform bağımsız**, **standart** bir formatta üreterek istenilen hedefe aktarabilmeyi sağlar.

- Her dilin kütüphanesi farklı veri formatları oluşturabilirken, **OpenTelemetry** bu verileri **tek bir standarda** oturtur.

---

{{< slide template="darkslide3" >}}

### OpenTelemetry Nedir?

- **CNCF** (Cloud Native Computing Foundation) tarafından desteklenir ve **APM** araçlarından bağımsız çalışır.

- **OTLP** protokolü sayesinde endüstri standartlarında veri toplayabilir.

- **Jaeger** ve **Zipkin** gibi araçlarla uyumlu çalışarak kapsamlı bir gözlemlenebilirlik çözümü sunar.

{{% /section %}}

---

{{% section %}}

{{< slide template="darkslide4" >}}

### APM (Application Performance Monitoring) Araçları

- **Jaeger ve Zipkin**: Özellikle **tracing** için kullanılan açık kaynaklı platformlardır. OpenTelemetry'le uyumludurlar.

- **Jaeger**: Cassandra ve Elasticsearch gibi veri depolarını destekler.

- **Zipkin**: Tracing tarafında yine popüler açık kaynak bir çözümdür.

- Özellikle bu iki araç log verisi istemezler; daha çok **trace** odaklı çalışırlar.
---

{{< slide template="darkslide3" >}}

### APM (Application Performance Monitoring) Araçları

- **Elastic APM**: Elastic tarafından geliştirilen bir Application Performance Monitoring çözümüdür. Uygulamaların performansını, hatalarını ve işlemler arasındaki gecikmeleri izleyebilmek için distribute tracing, log analizi ve metrik toplama özelliklerini bir arada sunar.

---

{{< slide template="darkslide5" >}}

### APM (Application Performance Monitoring) Araçları

- **New Relic**: SaaS tabanlı bir Application Performance Monitoring platformudur. Anlık performans metrikleri, hata takibi ve gelişmiş analiz araçları sunarak uygulamanızın uçtan uca izlenmesini sağlar. Kod seviyesinde detaylı tracing, kullanılabilirlik ölçümleri, gecikme analizleri gibi özelliklerle performans sorunlarını hızlıca tespit etmeye yardımcı olur.

---

{{< slide template="darkslide5" >}}

### APM (Application Performance Monitoring) Araçları

- **Application Insights**: Microsoft Azure ekosisteminin bir parçası olan Application Insights, canlı uygulamaların performans ve kullanım verilerini izlemek için kullanılan bir APM hizmetidir. Kullanıcı davranışlarını, istek performansını ve hataları gerçek zamanlı olarak takip etmeyi sağlar. Ayrıca, Azure’un diğer hizmetleriyle entegre çalışarak merkezi izleme, uyarı mekanizmaları ve veri analizi imkanları sunar.

---

{{< slide template="darkslide3" >}}

### APM (Application Performance Monitoring) Araçları

- Bu tüm araçlarg genellikle önce gelen veri paketlerini kaydeder, sonrasında da **indexleyerek** sorgulanabilir ve görselleştirilebilir hale getirir.

{{% /section %}}


---

{{% section %}}

{{< slide template="darkslide3" >}}

## Trace Data Nedir?

- **Tracing**, logların daha özelleşmiş bir formudur ve uygulamada meydana gelen olayları **daha detaylı** biçimde gösterir.
- Bu sayede performansla ilgili problemleri, hangi adımda gecikme yaşandığını ve işlemlerin genel gidişatını inceleyebilirsiniz.
- .NET 5 öncesindeki projelerde, **System.Diagnostic.DiagnosticSource** paketine ihtiyaç duyulur.

---

{{< slide template="darkslide2" >}}

### Trace Data İçeriği

Bir **trace**, uygulamanın farklı katmanları veya bileşenleri arasındaki etkileşimleri ayrıntılı bir şekilde gösterir. Örneğin:

- **HTTP Request**: İsteğin gönderilme ve alınma süresi.
- **HTTP Response**: Dönen cevabın içeriği ve genel yanıt süresi.

---

{{< slide template="darkslide2" >}}

### Trace Data İçeriği

- **Veritabanı İşlemleri (DB)**: Komutların (query, insert, update vb.) ne kadar sürdüğü ve hangi tabloların etkilendiği.
- **Başka Bir API'ye Çağrı (Another API)**: Harici servis veya mikroservis iletişimi.
- **Metot Çağrıları (Method)**: Metot içerisinde gerçekleşen adımlar, parametreler ve süre bilgisi.
- **Queue İşlemleri (Queue)**: Sıralarda bekleyen mesajlar, gönderim ve tüketim süreleri.

---

{{< slide template="darkslide2" >}}

### Trace Data İçeriği

Bu veriler, tek bir zincir (trace) üzerinde segmentler (span) şeklinde toplanır ve böylelikle **uçtan uca** bir görünürlük elde etmenizi sağlar.

{{% /section %}}