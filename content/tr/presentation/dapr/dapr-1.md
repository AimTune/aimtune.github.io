---
title: "Dapr (Distributed Application Runtime) - 1"
date: 2024-07-10T19:45:20+09:00
description: "Bu sunumda modern mikroservis mimarileri için güçlü bir sidecar aracı olan Dapr'ı (Distributed Application Runtime) keşfedeceğiz. Sunumda değinilecek Dapr konuları: Service Invocation (Servis Çağırma), State Management (Durum Yönetimi), Secrets Management (Gizli Veri Yönetimi), Configuration (Yapılandırma), Resiliency (Dayanıklılık)."
tags:
  - Dapr
  - Mikroservisler
  - Kubernetes
  - Redis
  - JavaScript
  - Node.js
  - Sidecar Pattern
  - Cross Cutting Concerns
series:
categories:
image: images/slides/dapr/dapr-logo.png
highlightTheme: monokai
revealTheme: night
revealBackgroundColor: ""
revealBackgroundImage: ""
revealBackgroundPosition: ""
revealBackgroundRepeat: ""
revealBackgroundOpacity: ""
revealBackgroundVideo: ""
revealBackgroundVideoLoop: false
revealBackgroundVideoMuted: false
revealBackgroundSize: ""
reveal:
  - main:
      - sub:
          - |
            # Dapr
            (Distributed Application Runtime)

            <img src="/images/slides/dapr/dapr-logo.png" height="300" style="border: none;background-color: transparent;"/>
      - sub:
          - |
            ## Dapr'a Giriş
            Dapr, mikroservis tabanlı uygulamaların geliştirilmesini ve çalıştırılmasını kolaylaştıran, open-source bir sidecar ürünüdür.
  - main:
      - sub:
          - |
            ## Sidecar Pattern Nedir?
            Sidecar Pattern, yardımcı bir bileşenin (sidecar) ana uygulamaya eklenmesiyle (container veya process), uygulamanın iş mantığına müdahale etmeden ortak görevlerin yürütülmesini sağlar. Güvenlik, logging ve dinamik yapılandırma gibi cross cutting concerns'leri yönetmek için idealdir.
      - sub:
          - |
            ## Cross Cutting Concerns Nedir?
            Cross cutting concerns, yazılım sisteminde birçok modül veya katmanda ortak olan ve tekrarlanan fonksiyonel özelliklerdir. Güvenlik, logging, hata yönetimi, performans izleme gibi konular bu kapsamda değerlendirilir. Bunlar, sistemin bakımını ve genişletilebilirliğini artırır.
      - sub:
          - |
            ## Sidecar Pattern'in Avantajları
            - Yardımcı hizmetleri izole eder.
            - Uygulamanın modülerliğini ve yeniden kullanılabilirliğini artırır.
            - Yönetimi ve bakımı kolaylaştırır.
      - sub:
          - |
            ## Örnek Sidecar: Resiliency (Dayanıklılık)
            - Resiliency, bir sistemin hatalardan kurtulma ve hizmet vermeye devam etme yeteneğidir. Sidecar kullanarak bir mikroservise resiliency özellikleri eklemek, özellikle ağ hataları veya diğer geçici sorunlar durumunda hizmet sürekliliğini sağlamak için etkilidir. Bu sidecar, otomatik yeniden deneme (retry), devre kesici (circuit breaker) ve zaman aşımı (timeout) gibi dayanıklılık desenlerini uygular.
            - Bizler de sidecar'larda örneği uygulamamıza gelen trafiği sadece sidecar üstünden alabiliriz ve gelen istekleri sidecar içerisinde resiliency görevi görecek kodlardan geçiririz ve uygulamamızın ayakta olmadığı durumda resiliency policy'lerine göre tekrar istek atma veya istek durdurma sürecine geçer.
  - main:
      - sub:
          - |
            ## Dapr'ın Amacı ve Faydaları
            - Uygulama mantığını değiştirmeden dağıtılmış sistemlerin yaygın ihtiyaçlarını karşılamak için çeşitli yapı taşları (building blocks) ve birçok farklı özellik sunar.
            - HTTP ve gRPC protokolleri üzerinden çalışarak çoklu programlama dilleriyle uyumluluk sunar.
            - Kolay programlayabilmek için birçok farklı dilde SDK'ları vardır.

  - fragment:
      - sub:
          - |
            ## Dapr'ın Temel Bileşenleri
      - sub:
          - |
            #### Service Invocation*
      - sub:
          - |
            #### State Management*
      - sub:
          - |
            #### Secrets Management*
      - sub:
          - |
            #### Configuration*
      - sub:
          - |
            #### Pub/Sub Messaging
      - sub:
          - |
            #### Bindings
      - sub:
          - |
            #### Distributed lock
      - sub:
          - |
            #### Cryptography
      - sub:
          - |
            #### Actors
      - sub:
          - |
            #### Workflow

  - fragment:
      - sub:
          - |
            ## Dapr'ın Diğer Özellikleri

      - sub:
          - |
            ### Resiliency*
      - sub:
          - |
            Hata toleransı sağlamak için zaman aşımı, yeniden deneme, devre kesici ve geri çekilme gibi politikalar tanımlamayı ve uygulamayı destekler.

      - sub:
          - |
            ### Observability
      - sub:
          - |
            Open Telemetry ve Zipkin gibi protokollerle izleme verilerini toplar ve birçok gözlemlenebilirlik aracıyla entegrasyon sağlar.

      - sub:
          - |
            ### Security
      - sub:
          - |
            Varsayılan olarak etkin güvenlik özellikleri sunar, API'lar, servisler ve bileşenler için uygulamaya özel politikalar ayarlama imkanı sağlar. İletişim mTLS ile otomatik olarak şifrelenir.

  - fragment:
      - sub:
          - |
            # Service Invocation
      - sub:
          - |
            #### Mikroservisler arası iletişim sağlar.
      - sub:
          - |
            #### HTTP veya gRPC ile çalışır.
      - sub:
          - |
            #### Servis keşfi ve yük dengeleme özellikleri içerir.
      - sub:
          - |
            #### Servislerde araya girdiği için security, resiliency, observability gibi yapıları da bu istekler çalıştığı anda uygulayabilir.

  - fragment:
      - sub:
          - |
            # State Management
      - sub:
          - |
            #### Uygulamalarda durum (state) kalıcılığı sağlar.
      - sub:
          - |
            #### Key/value tabanlı durum depolamada görev alır.
      - sub:
          - |
            #### Farklı ürünler ile entegre edilebilir (Redis, MongoDB, SQLs*, In-Memory, etcd, vb...).
      - sub:
          - |
            ![State Store Example](/images/slides/dapr/statestore.png)

  - main:
      - sub:
          - |
            ## Secrets Management
            - Güvenli bilgi yönetimini sağlar.
            - API üzerinden bu gizli bilgileri alabilmeyi kolaylaştırır. Örneğin  DB
            - Çeşitli ürünler ile uyumludur.

  - main:
      - sub:
          - |
            ## Geliştirici Deneyimi
            Uygulama geliştiricileri, Dapr'ın sağladığı API'leri kullanarak mikroservislerini daha hızlı ve güvenilir bir şekilde oluşturabilir ve yönetebilir.
---
