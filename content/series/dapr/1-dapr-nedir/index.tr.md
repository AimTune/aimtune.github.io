---
title: "Dapr Nedir?"
date: 2025-04-18T21:14:06+01:00
description: Bu yazımızda, Dapr kavramını, temel bileşenlerini ve teknolojilerini ele alıyoruz.
summary: Bu yazımızda, Dapr kavramını, temel bileşenlerini ve teknolojilerini ele alıyoruz.
hideToc: false
enableToc: true
enableTocContent: true
author: Hamza Ağar
authorEmoji: 🤖
tags:
  - dapr
  - sidecar
  - microservices
  - distributed applications
categories:
  - dapr-serisi
cascade:
  showSummary: true
---

{{< lead >}}
Dapr (Distributed Application Runtime), mikro hizmet tabanlı dağıtık uygulamaların geliştirilmesini ve işletilmesini basitleştiren, olay odaklı, taşınabilir bir çalışma zamanıdır.
{{< /lead >}}

{{< alert "circle-info" >}}
Bu yazı serimizde, Dapr kavramını, temel bileşenlerini ve teknolojilerini ele alıyor olacağım. Dapr, uzun süredir üzerinde çalıştığım bir araç. Bu araç, Microsoft tarafından geliştirilmeye başlanmış, daha sonradan ise CNCF'ye taşınmış bir araçtır.
{{< /alert >}}

Selamlar,

Son günlerde, Conversation modülü sayesinde ve daha öncesinde geliştirilmiş Workflow modülü sayesinde, çalışmakta olduğum Chatbot ürününe de çokça katkı sağlayacağına inandığım bir araç haline geldi. Bu kaynağı ise Türkçe içerik olmamasından dolayı ve bana da YouTube üzerinde paylaşılan bana ait bir anlatımdan gelen geri dönüşler üzerine yazıyorum.

## Dapr Nedir?

Dapr; durum yönetimi (state management), yayın/abonelik (pub/sub), aktörler (actors), sıraya bağlama (bindings), kriptografi ve dağıtılmış izleme gibi temel yapı taşlarını sunarak geliştiricinin yeniden kullanılabilir kod yazmasını sağlar.

{{< alert "circle-info" >}}
Dapr, HTTP veya gRPC üzerinden erişilebilen entegre API'ler aracılığıyla mikro hizmetler arasında servis çağrısı, durum yönetimi, yayın/abonelik, işlem akışları (workflow), aktör modeli ve daha fazlasını sağlar. Çok sayıda programlama dilini destekler ve çoklu altyapı (Kubernetes, sanal makineler, sunucusuz platformlar) üzerinde çalışabilir.
{{< /alert >}}

Dapr, HTTP veya gRPC üzerinden erişilebilen entegre API'ler aracılığıyla mikro hizmetler arasında servis çağrısı, durum yönetimi, yayın/abonelik, işlem akışları (workflow), aktör modeli ve daha fazlasını sağlar. Çok sayıda programlama dilini destekler ve çoklu altyapı (Kubernetes, sanal makineler, sunucusuz platformlar) üzerinde çalışabilir. Ayrıca Dapr, programlama dilinden bağımsızdır ve herhangi bir programlama dilinde kullanılabilir. Bunu HTTP veya gRPC üzerinden erişilebilen entegre API'ler aracılığıyla sağlar.

## Sidecar Pattern Nedir?

Sidecar deseni, bir mikro hizmetin yanına eklenen küçük, bağımsız bir konteynerin (ya da işlem) ana hizmetin operasyonel görevlerini üstlenmesini sağlayan bir mimari yaklaşımdır. Yanarı konumlandırılan bu yan konteyner (sidecar), loglama, monitoring, configuration management, servis mesh proxy'leri veya güvenlik gibi çapraz kesen (cross-cutting) sorumlulukları gerçekleştirir.

Örneğin, bir web uygulamanız var ve bu uygulamanın loglarını toplamak istiyorsunuz. Bu durumda, web uygulamanızın yanında bir log toplama container'ı çalıştırabilirsiniz. Bu container, web uygulamanızın loglarını toplar ve bunları bir log aggregator'a gönderir. Örneğin bu senaryoyu OTel Collector'a kolaylıkla yazdırabilirsiniz. Bunların yanında, bu araç sayesinde, Redis, Kafka, RabbitMQ gibi sistemlerle dil bağımsız şekilde entegrasyon yapabilirsiniz. Tek yapmanız gereken, bu Dapr'ın açtığı container'daki YAML dosyalarını konfigüre etmek olacaktır.

## Dapr ve Sidecar Pattern İlişkisi

Dapr'ın mimarisi, her mikro hizmet uygulamasının yanına bir Dapr sidecar'ı eklenmesi üzerine kuruludur; böylece Dapr'ın sunduğu tüm "building block" API'leri, ana iş konteynerine dokunmadan kullanılabilir. Dapr sidecar'ı, servis çağrıları, durum yönetimi ve mesajlaşma gibi görevleri kendi içinde yöneterek, uygulamanın üretim ortamında hazırcı çözümlerle donatılmasını sağlar.

Modern bulut ve mikro hizmet tabanlı mimarilerde, çapraz kesen sorumlulukların güvenilir, taşınabilir ve kolay bakım yapılabilir bir biçimde yönetilmesi kritik öneme sahiptir. Dapr ve sidecar pattern birlikte kullanıldığında, geliştiriciler karmaşık altyapı detaylarına takılmadan iş mantığına odaklanabilir, operasyonel görevler ise yan konteynerlerde standardize ve izole biçimde yürütülür. Bu yaklaşım, uygulamaların ölçeklenebilirliğini, dayanıklılığını ve sürdürülebilirliğini artırır.

## Dapr'ın Temel Bileşenleri

{{< figure
    src="/images/series/dapr/dapr-building-blocks.png"
    alt="Dapr Building Blocks"
    caption="Dapr'ın Temel Yapı Taşları (<a href='https://docs.dapr.io/concepts/building-blocks-concept/'>Dapr Building Blocks</a>)"
    >}}

### Building Blocks

{{< alert "circle-info" >}}
Her bir building block, Dapr'ın sidecar'ı üzerinden erişilebilen HTTP/gRPC API'leri sunar. Bu API'ler sayesinde, dil ve platform bağımsız olarak mikroservis mimarinizi geliştirebilirsiniz.
{{< /alert >}}

#### 1. Service Invocation
Mikroservisler arası iletişimin temel yapı taşı. HTTP veya gRPC protokolleri üzerinden güvenli ve doğrudan metod çağrıları yapmanızı sağlar.

{{< alert "code" >}}
**Endpoint:** `/v1.0/invoke`
- Yerleşik servis keşfi (service discovery)
- Otomatik yük dengeleme
- Yerleşik dağıtık izleme
{{< /alert >}}

#### 2. Publish & Subscribe
Event-driven mimariler için ideal mesajlaşma modeli. Mikroservisler arasında güvenli ve ölçeklenebilir mesajlaşma sağlar.

{{< alert "code" >}}
**Endpoints:** `/v1.0/publish`, `/v1.0/subscribe`
- Gevşek bağlı (loosely coupled) iletişim
- At-least-once teslimat garantisi
- Çoklu mesaj broker desteği
{{< /alert >}}

#### 3. Workflow
Farklı mikroservisler arasında mantık orkestrasyonu yapmanızı sağlar. Uzun süren iş akışlarını yönetmek için kullanılır.

{{< alert "code" >}}
**Endpoint:** `/v1.0/workflow`
- Durum yönetimi ve hata toleransı
- Diğer building block'larla entegrasyon
- Retry ve error handling
{{< /alert >}}

#### 4. State Management
Uzun süreli stateful servisler oluşturmanızı sağlar. Redis, MongoDB gibi farklı state store'lar ile çalışabilir.

{{< alert "code" >}}
**Endpoint:** `/v1.0/state`
- Key/Value tabanlı state yönetimi
- Concurrency ve consistency kontrolleri
- State encryption desteği
{{< /alert >}}

#### 5. Bindings
Harici sistemlerle entegrasyon için çift yönlü bağlantı sağlar. 70'den fazla hazır binding komponenti mevcuttur.

{{< alert "code" >}}
**Endpoint:** `/v1.0/bindings`
- Input ve output binding'ler
- Trigger-based işlemler
- Özel binding geliştirme imkanı
{{< /alert >}}

#### 6. Actors
Virtual Actor pattern implementasyonu. Stateful mikroservisler için idealdir.

{{< alert "code" >}}
**Endpoint:** `/v1.0/actors`
- Tek iş parçacıklı execution modeli
- Timer ve reminder desteği
- Reentrancy kontrolü
{{< /alert >}}

#### 7. Secrets Management
Hassas verilerin güvenli yönetimi için kullanılır. Kubernetes Secrets, Azure Key Vault gibi sistemlerle entegre çalışır.

{{< alert "code" >}}
**Endpoint:** `/v1.0/secrets`
- Çoklu secret store desteği
- Secret scoping ve access control
- Güvenli secret rotasyonu
{{< /alert >}}

#### 8. Configuration
Uygulama konfigürasyonlarını yönetmenizi ve değişikliklerden haberdar olmanızı sağlar.

{{< alert "code" >}}
**Endpoint:** `/v1.0/configuration`
- Real-time config güncellemeleri
- Config subscription modeli
- Versiyonlama desteği
{{< /alert >}}

#### 9. Distributed Lock
Paylaşılan kaynaklara güvenli erişim için kullanılır.

{{< alert "code" >}}
**Endpoint:** `/v1.0-alpha1/lock`
- Mutual exclusion garantisi
- Deadlock prevention
- Lock timeout mekanizması
{{< /alert >}}

#### 10. Cryptography
Güvenli kriptografik işlemler için kullanılır.

{{< alert "code" >}}
**Endpoint:** `/v1.0-alpha1/crypto`
- Key yönetimi
- Encryption/Decryption işlemleri
- HSM entegrasyonu
{{< /alert >}}

#### 11. Jobs
İş planlama ve orkestrasyon için kullanılır.

{{< alert "code" >}}
**Endpoint:** `/v1.0-alpha1/jobs`
- Zamanlanmış görevler
- Batch processing
- ETL iş akışları
{{< /alert >}}

#### 12. Conversation
LLM entegrasyonları için modern arayüz sağlar.

{{< alert "code" >}}
**Endpoint:** `/v1.0-alpha1/conversation`
- Prompt yönetimi ve caching
- PII maskeleme
- Çoklu LLM desteği
{{< /alert >}}

### Components

1. **State Stores:** Redis, MongoDB, Azure CosmosDB gibi veri saklama sistemleri
2. **Message Brokers:** Redis, RabbitMQ, Azure Service Bus gibi mesajlaşma sistemleri
3. **Name Resolution:** Service discovery için kullanılır
4. **Secret Stores:** Kubernetes Secrets, Azure Key Vault gibi hassas veri saklama sistemleri

## Dapr'ın Operasyonel Özellikleri

### Observability (Gözlemlenebilirlik)
Dapr, bileşenler ve ağ servisleri arasındaki mesaj çağrılarını görüntülemenizi ve ölçmenizi sağlar. OpenTelemetry, Jaeger, Zipkin gibi araçlarla entegre çalışır.

### Hosting Options (Barındırma Seçenekleri)
Dapr'ı farklı ortamlara deploy etme seçenekleri sunar:
- Self-Hosted (Docker, Podman)
- Kubernetes (AKS, GKE, EKS)
- Serverless (Azure Container Apps)

### Configuration Management (Yapılandırma Yönetimi)
Dapr konfigürasyonlarını yönetme ve deployment'ları kontrol etme imkanı sağlar. YAML dosyaları üzerinden kolay konfigürasyon yapılabilir.

### Component Management (Bileşen Yönetimi)
Dapr bileşenlerini uygulamanızda yönetme imkanı sunar. State stores, pub/sub brokers, secret stores gibi bileşenler kolayca yönetilebilir.

### Security (Güvenlik)
Dapr deployment'larını güvenli hale getirmek için en iyi uygulamalar ve talimatlar sunar:
- mTLS sertifikaları
- OAuth yetkilendirme
- API token authentication

### Resiliency (Dayanıklılık)
Hata kurtarma politikaları ile Dapr'ın hata durumlarını yönetme imkanı sağlar:
- Retry politikaları
- Timeout yapılandırmaları
- Circuit breaker pattern

### Support & Versioning (Destek ve Sürümleme)
Dapr için mevcut destek ve sürümleme seçenekleri sunar. CNCF projesi olarak aktif geliştirme ve destek süreci devam etmektedir.

### Performance & Scalability (Performans ve Ölçeklenebilirlik)
Dapr building block'ları için benchmark'lar ve yönergeler sunar. Service invocation ve Actors activation performans metrikleri mevcuttur.

### Debugging & Troubleshooting (Hata Ayıklama)
Dapr ile ilgili sorunları teşhis etmek ve çözmek için araçlar ve teknikler sunar:
- Log yönetimi
- API logları
- Debugging araçları

{{< alert "lightbulb" >}}
**İpucu:** Dapr'ın sunduğu building block'ları kullanarak, uygulamalarınızı daha basit ve güvenli hale getirebilirsiniz.
{{< /alert >}}

### Sonuç

Dapr, mikro hizmet tabanlı uygulamaların geliştirilmesi ve işletilmesi için birçok avantaj sunan bir çalışma zamanıdır. Sidecar pattern'i kullanarak, Dapr'ın sunduğu building block'ları kullanarak, uygulamalarınızı daha basit ve güvenli hale getirebilirsiniz.

{{< alert "bookmark" >}}
Sonraki yazılarımda, Dapr'ın bu building block'larından ilk olarak Service Invocation'ın nasıl çalıştığını, nasıl entegre edildiğini ve nasıl kullanıldığını göreceğiz.
{{< /alert >}}

Okuduğunuz için teşşekkürler. Sonraki yazıda görüşürüz :smiling_face_with_smiling_eyes:

## Kaynakça

1. [Dapr Documentation](https://docs.dapr.io/)
2. [Practical Microservices with Dapr and .NET - Second Edition, Richard L. Weeks, Packt Publishing, 2022](https://www.amazon.com/Practical-Microservices-Dapr-NET-cloud-native/dp/1803248122)
3. [Dapr'ın GitHub Repository](https://github.com/dapr/dapr)