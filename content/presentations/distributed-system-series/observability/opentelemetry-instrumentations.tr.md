+++
weight=5
+++

{{% section %}}

## Instrumentations Nedir?

**Instrumentations**, bir uygulamanın belirli bölümlerini (ör. ASP.NET Core, HttpClient, Entity Framework, Redis, RabbitMQ) otomatik olarak **izlenebilir** hâle getiren bileşenler veya kütüphanelerdir. Bu sayede, uygulamanızın farklı katmanlarında (ör. web istekleri, veri tabanı işlemleri, mesaj kuyruğu vb.) gerçekleşen olaylar ve performans metrikleri **otomatik** olarak toplanır ve kaydedilir.

---

- **Neden Gerekli?**
  - Uygulamanın kritik noktalarını (API çağrıları, veritabanı sorguları, mesaj kuyruğu işlemleri vb.) tek tek manuel kodlamadan izlemeye olanak tanır.
  - Performans sorunlarını veya hataları hızlı bir şekilde tespit edip kök neden analizi (root cause analysis) yapmak kolaylaşır.

---

- **Nasıl Çalışır?**
  - Geliştiriciler, ilgili **instrumentation** paketini projeye ekler (NuGet).
  - Uygulamaya, konfigürasyonla hangi bileşenlerin izleneceği belirtilir (AddAspNetCoreInstrumentation, AddHttpClientInstrumentation, vb.).
  - Toplanan veriler, tercihe göre Jaeger, Zipkin, Elastic APM gibi dış araçlara veya konsola gönderilir (export edilir).

---

> **Özetle**: Instrumentations, uygulamanızdaki karmaşık işlemleri **elle uğraşmadan** otomatik olarak ölçümleyerek daha kolay gözlemleme (observability) sağlar.

{{% /section %}}

---

![OpenTelemetry Console Packages](/images/series/opentelemetry/opentelemetry-instrumentations-package.png)
Öncelikle bu paketleri yüklüyoruz.

---

## Instrumentations

Aşağıda .NET projelerinde sıkça kullanılan **instrumentation** (izleme/ölçüm) seçeneklerini özetliyoruz. Bu bileşenler, OpenTelemetry veya benzeri kütüphaneler aracılığıyla uygulamanın önemli noktalarını (HTTP istekleri, veritabanı işlemleri, mesaj kuyruğu işlemleri vb.) otomatik veya yarı otomatik bir şekilde izlenebilir hâle getirir.

---

{{% section %}}

### 1. ASP.NET Core Instrumentation

- **Amaç**: ASP.NET Core uygulamanızın **HTTP istek**lerinin süresini, yanıt kodlarını ve performansını otomatik olarak ölçmek.
- **Neler Ölçülür?**
  - Giden/gelen HTTP istekleri
  - İstek başlama ve bitiş zamanı
  - Yanıt durum kodu (ör. 200, 404, 500)
  - İstek başlıkları ve yol (endpoint) bilgileri

---

### 1. ASP.NET Core Instrumentation

- **Fayda**:
  - Uygulamanıza ek **middleware** eklemeden, out-of-the-box izleme alabilirsiniz.
  - Hangi endpoint’lerin ne kadar sıklıkla ve hangi sürelerde çalıştığını görebilirsiniz.

{{% /section %}}

---

{{% section %}}

### 2. HttpClient Instrumentation

- **Amaç**: Uygulamanız içindeki **HttpClient** çağrılarını izlemek ve performans sorunlarını tespit etmek.
- **Neler Ölçülür?**
  - Yapılan **dış istek** (URL), metot (GET, POST vb.)
  - Başlangıç ve bitiş zamanı
  - Yanıt kodu ve süresi (latency)

---

### 2. HttpClient Instrumentation

- **Fayda**:
  - Mikroservisler veya harici API’lere yapılan çağrıları kolayca takip edersiniz.
  - Yanıt süresi uzun mu, hatalar hangi oranda gerçekleşiyor vb. sorulara yanıt bulabilirsiniz.

{{% /section %}}

---

{{% section %}}

### 3. Entity Framework Instrumentation

- **Amaç**: Entity Framework (EF Core) ile yapılan **veritabanı** işlemlerini (sorgu, ekleme, güncelleme) otomatik olarak izlemek.
- **Neler Ölçülür?**
  - Oluşturulan sorgular (SQL)
  - Her sorgunun çalışma süresi (latency)
  - Hata durumu (ör. time-out, bağlantı hatası)

---

### 3. Entity Framework Instrumentation

- **Fayda**:
  - Veritabanı katmanındaki **performans darboğazlarını** (örneğin uzun süren sorgular) kolayca tespit edebilirsiniz.
  - **Tracing** üzerinden hangi üst işlem (HTTP istek, background job vb.) sırasında bu sorguların tetiklendiğini görebilirsiniz.

{{% /section %}}

---

{{% section %}}

### 4. Redis Instrumentation

- **Amaç**: Redis kullanımıyla ilgili **performans ve hata** gözlemlemek (GET, SET, Publish/Subscribe vb.).
- **Neler Ölçülür?**
  - Redis komutları (örn. `GET`, `SET`, `MGET`, `PUBLISH`)
  - Komutun başlangıç ve bitiş zamanı
  - Hata durumları (ör. bağlantı hataları, time-out)

---

### 4. Redis Instrumentation

- **Fayda**:
  - Redis çağrılarının ne kadar sık yapıldığını ve ne kadar sürdüğünü tespit edebilirsiniz.
  - Uygulamanın nakit (cache) katmanında olup bitenleri **tek bir trace** altında izlemek mümkündür.

{{% /section %}}

---

{{% section %}}

### 5. MassTransit Library Instrumentation

- **Amaç**: **RabbitMQ** üzerinden mesajların kuyruklanması ve işlenmesi sürecini izlemek.
- **MassTransit Kütüphanesi**: .NET dünyasında RabbitMQ gibi mesajlaşma altyapılarına dair kolaylaştırıcı bir çerçeve (framework) sunar.

---

### 5. MassTransit Library Instrumentation

- **Neler Ölçülür?**
  - Kuyruğa gönderilen mesajlar (Publish/Send)
  - Tüketici (Consumer) tarafından alınan mesajların işleme süresi
  - Hata durumları (ör. ileti zaman aşımı, işleyici (handler) hatası)

---

### 5. MassTransit Library Instrumentation

- **Fayda**:
  - Dağıtık bir mimaride, mesajların **uçtan uca** (publish -> queue -> consumer) hangi aşamalardan geçtiğini görebilir, hangi aşamada gecikme ya da hata oluştuğunu tespit edebilirsiniz.
  - **MassTransit** ile entegre bir şekilde izleme sağlayarak, iş akışını (workflow) uçtan uca izleyebilirsiniz.

{{% /section %}}

---

> **Özetle**, bu instrumentations sayesinde uygulamanın önemli katmanları (web istekleri, veritabanı, mesaj kuyruğu vb.) hakkında ayrıntılı **telemetri verileri** elde edebilir, **hata ayıklama** ve **performans analizi** süreçlerinizi kolaylaştırabilirsiniz.

---