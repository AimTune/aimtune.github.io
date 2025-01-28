+++
title = "Observability ve OpenTelemetry Nedir?"
summary = "Bu sunumda, modern dağıtık sistemlerde gözlemlenebilirlik (observability) kavramını inceleyeceğiz. Yazılım sistemlerinde gözlemlenebilirlik kavramını, log, trace ve metrics gibi temel bileşenleri ve OpenTelemetry gibi endüstri standartlarını ele alarak, sistemlerin performansını nasıl izleyebileceğimizi ve hataları nasıl tespit edebileceğimizi öğreneceğiz."
date = 2025-01-28T23:36:10+01:00
topics = ["Observability", "Monitoring", "Logs", "Tracing", "Metrics", "OpenTelemetry", "APM", "Distributed Systems"]
layout = "list"
outputs = ["Reveal"]
[reveal_hugo]
margin = 0.2
weight=1
+++

{{% section %}}

{{< slide template="darkslide3" >}}

## Observability Nedir?
(Sistem Gözlemlenebilirliği)
<br>

<img src="/images/series/opentelemetry/opentelemetry-logo.png" height="300" style="border: none;background-color: transparent;"/>

---

{{< slide template="darkslide2" >}}

- **Tanım**: Observability, uygulamaların canlı ortamda bile iç durumlarını dışa vuran veriler üreterek izlenebilmesini sağlayan bir yaklaşımdır. Aynı zamanda bir sistemin iç durumunu dış gözlemlerle anlama yeteneğini ifade eder ve dağıtık sistemlerde sistemin performansını izlemek ve hataları tespit etmek için kullanılır.

- **Neden Önemli?**: IDE'de lokal olarak debug yapmak kolay. Ancak canlıda bir sorun yaşandığında sistemi gözlemleyebilmek için bazı verileri aktif olarak toplamamız gerekir.

{{% /section %}}

---

{{% section %}}

{{< slide template="darkslide3" >}}

## Observability'nin 3 Temel Veri Tipi

---

{{< slide template="darkslide4" >}}

1. **Log:**

   -  Sistemde meydana gelen olayların kaydıdır ve detaylı analiz yapma imkanı sunar.

   - Uygulamanın zaman bilgisini (timestamp), mesajı, sınıf/metot bilgilerini ve formatlanmış metinleri içerir.

   - Her yere log atmak sakıncalı olabilir, çünkü sistemde yük oluşturabilir.

---

{{< slide template="darkslide4" >}}

2. **Metrics:**

   - Yükü en hafif olan, sistem performansını gösteren sayısal veriler sağlar. (ör. CPU kullanımı, kuyruktaki istek sayısı, hata sayısı).

   - Uygulamadan veya container/servis mesh gibi katmanlardan toplanabilir.

---

{{< slide template="darkslide4" >}}

3. **Tracing:**

   - İşlemlerin dağıtık sistemlerde nasıl ilerlediğini izler. Özellikle mikroservisler arası isteklerin nasıl geçtiğini takip eder.

   - **Trace Data**: Başlangıçtan bitişine kadar bir operasyonu (transaction) uçtan uca izlemek için oluşturulur (Bu veride hangi işlemle devam etti, işlem ne kadar sürdü gibi veriler vardır.).

   - Geniş çaplı (ör. bir HTTP request’in veritabanı işlemlerine kadar takibi) süreçlerde gereklidir.

   - Her yerde trace tutmak da kaynak tüketimini artırır; ihtiyaca göre konumlandırılmalıdır.

{{% /section %}}

---

{{< slide template="darkslide5" >}}

## Observability'nin Önemi

- **Hata Ayıklama**: Performans ve hataların gerçek zamanlı izlenmesi.

- **Proaktif İzleme**: Sorunları önceden tespit etme ve çözüm üretme.

- **Sistem Kararlılığı**: Daha dayanıklı ve performanslı sistemler için kritik.