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

Selamlar,

Son günlerde, Conversation modülü sayesinde ve daha öncesinde geliştirilmiş Workflow modülü sayesinde, çalışmakta olduğum Chatbot ürününe de çokça katkı sağlayacağına inandığım bir araç haline geldi. Bu kaynağı ise Türkçe içerik olmamasından dolayı ve bana da YouTube üzerinde paylaşılan bana ait bir anlatımdan gelen geri dönüşler üzerine yazıyorum.

Bu yazı serimizde, Dapr kavramını, temel bileşenlerini ve teknolojilerini ele alıyor olacağım. Dapr, uzun süredir üzerinde çalıştığım bir araç. Bu araç, Microsoft tarafından geliştirilmeye başlanmış, daha sonradan ise CNCF'ye taşınmış bir araçtır.

## Dapr Nedir?

Dapr (Distributed Application Runtime), mikro hizmet tabanlı dağıtık uygulamaların geliştirilmesini ve işletilmesini basitleştiren, olay odaklı, taşınabilir bir çalışma zamanıdır. Dapr; durum yönetimi (state management), yayın/abonelik (pub/sub), aktörler (actors), sıraya bağlama (bindings), kriptografi ve dağıtılmış izleme gibi temel yapı taşlarını sunarak geliştiricinin yeniden kullanılabilir kod yazmasını sağlar.

Dapr, HTTP veya gRPC üzerinden erişilebilen entegre API'ler aracılığıyla mikro hizmetler arasında servis çağrısı, durum yönetimi, yayın/abonelik, işlem akışları (workflow), aktör modeli ve daha fazlasını sağlar. Çok sayıda programlama dilini destekler ve çoklu altyapı (Kubernetes, sanal makineler, sunucusuz platformlar) üzerinde çalışabilir. Ayrıca Dapr, programlama dilinden bağımsızdır ve herhangi bir programlama dilinde kullanılabilir. Bunu HTTP veya gRPC üzerinden erişilebilen entegre API'ler aracılığıyla sağlar.

## Sidecar Pattern Nedir?

Sidecar deseni, bir mikro hizmetin yanına eklenen küçük, bağımsız bir konteynerin (ya da işlem) ana hizmetin operasyonel görevlerini üstlenmesini sağlayan bir mimari yaklaşımdır. Yanarı konumlandırılan bu yan konteyner (sidecar), loglama, monitoring, configuration management, servis mesh proxy'leri veya güvenlik gibi çapraz kesen (cross-cutting) sorumlulukları gerçekleştirir.

Örneğin, bir web uygulamanız var ve bu uygulamanın loglarını toplamak istiyorsunuz. Bu durumda, web uygulamanızın yanında bir log toplama container'ı çalıştırabilirsiniz. Bu container, web uygulamanızın loglarını toplar ve bunları bir log aggregator'a gönderir. Örneğin bu senaryoyu OTel Collector'a kolaylıkla yazdırabilirsiniz. Bunların yanında, bu araç sayesinde, Redis, Kafka, RabbitMQ gibi sistemlerle dil bağımsız şekilde entegrasyon yapabilirsiniz. Tek yapmanız gereken, bu Dapr'ın açtığı container'daki YAML dosyalarını konfigüre etmek olacaktır.

## Dapr ve Sidecar Pattern İlişkisi

Dapr'ın mimarisi, her mikro hizmet uygulamasının yanına bir Dapr sidecar'ı eklenmesi üzerine kuruludur; böylece Dapr'ın sunduğu tüm "building block" API'leri, ana iş konteynerine dokunmadan kullanılabilir. Dapr sidecar'ı, servis çağrıları, durum yönetimi ve mesajlaşma gibi görevleri kendi içinde yöneterek, uygulamanın üretim ortamında hazırcı çözümlerle donatılmasını sağlar.

Modern bulut ve mikro hizmet tabanlı mimarilerde, çapraz kesen sorumlulukların güvenilir, taşınabilir ve kolay bakım yapılabilir bir biçimde yönetilmesi kritik öneme sahiptir. Dapr ve sidecar pattern birlikte kullanıldığında, geliştiriciler karmaşık altyapı detaylarına takılmadan iş mantığına odaklanabilir, operasyonel görevler ise yan konteynerlerde standardize ve izole biçimde yürütülür. Bu yaklaşım, uygulamaların ölçeklenebilirliğini, dayanıklılığını ve sürdürülebilirliğini artırır.

## Dapr'ın Temel Bileşenleri

### Building Blocks

1. **Service Invocation:** Microservice'ler arasında güvenli ve doğrudan metod çağrıları yapmanızı sağlar. HTTP veya gRPC protokolleri üzerinden çalışır.

2. **Publish & Subscribe:** Microservice'ler arasında güvenli ve ölçeklenebilir mesajlaşma sağlar. Event-driven mimariler için idealdir.

3. **Workflow:** Farklı microservice'ler arasında mantık orkestrasyonu yapmanızı sağlar. Uzun süren iş akışlarını yönetmek için kullanılır.

4. **State Management:** Uzun süreli stateful servisler oluşturmanızı sağlar. Redis, MongoDB gibi farklı state store'lar ile çalışabilir.

5. **Bindings:** Harici sistemlerle (Kafka, Redis, RabbitMQ vb.) entegrasyon yapmanızı sağlar. Input ve output binding'ler olarak ikiye ayrılır.

6. **Actors:** Kod ve veriyi yeniden kullanılabilir actor nesnelerinde kapsüllemenizi sağlar. Stateful microservice'ler için idealdir. Bu araç için ayrıca Actor Model yaklaşımına da değineceğiz.

7. **Secrets Management:** Uygulamanızdan güvenli bir şekilde secret'lara erişmenizi sağlar. Kubernetes Secrets, Azure Key Vault gibi sistemlerle entegre çalışır.

8. **Configuration:** Uygulama konfigürasyonlarını yönetmenizi ve değişikliklerden haberdar olmanızı sağlar.

9. **Distributed Lock:** Uygulamanızdan paylaşılan kaynaklara karşılıklı olarak özel erişim sağlar.

10. **Cryptography:** Anahtarları uygulamanıza açığa çıkarmadan şifreleme gibi işlemleri yapmanızı sağlar.

11. **Jobs:** İşlerin planlanmasını ve orkestrasyonunu yönetmenizi sağlar.

12. **Conversation:** Large Language Models (LLMs) ile prompt'ları kullanmanızı sağlar. Chatbot'lar ve AI destekli uygulamalar için idealdir.

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


### Sonuç

Dapr, mikro hizmet tabanlı uygulamaların geliştirilmesi ve işletilmesi için birçok avantaj sunan bir çalışma zamanıdır. Sidecar pattern'i kullanarak, Dapr'ın sunduğu building block'ları kullanarak, uygulamalarınızı daha basit ve güvenli hale getirebilirsiniz.

Sonraki yazılarımda, Dapr'ın bu building block'larından ilk olarak Service Invocation'ın nasıl çalıştığını, nasıl entegre edildiğini ve nasıl kullanıldığını göreceğiz.

Okuduğunuz için teşşekkürler. Sonraki yazıda görüşürüz :smiling_face_with_smiling_eyes:

## Kaynakça

1. [Dapr Documentation](https://docs.dapr.io/)
2. Practical Microservices with Dapr and .NET - Second Edition, Richard L. Weeks, Packt Publishing, 2022
3. [Dapr'ın GitHub Repository](https://github.com/dapr/dapr)
