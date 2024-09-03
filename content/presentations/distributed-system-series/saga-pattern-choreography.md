+++
title = "Saga Bölüm 1"
summary = "Bu sunumda modern mikroservis mimarileri için güçlü bir iş akışı yönetimi deseni olan Saga'yı keşfedeceğiz. Sunumda değinilecek Saga konuları: Choreography (Koreografi), Orchestration (Orkestrasyon), Compensation (Telafi İşlemleri), Error Handling (Hata Yönetimi), Transaction Management (İşlem Yönetimi)."
date = 2024-09-03T22:53:10+03:00
topics = ["Saga Pattern", "Mikroservisler", "Kubernetes", "Event-Driven Architecture", "Fault Tolerance", "Choreography", "Orchestration"]
layout = "list"
outputs = ["Reveal"]
[reveal_hugo]
theme = "night"
margin = 0.2
+++

{{% section %}}

## Saga Pattern
<br>
(Bağımsız ve Hata Toleranslı İş Akışı Yönetimi) 
<br>
<img src="/images/slides/saga/saga-cover.webp" height="300" style="border: none;background-color: transparent;"/>

##### Photo by [Microservices Architecture Pattern - SAGA](https://www.c-sharpcorner.com/article/microservices-architecture-pattern-saga/)
---

{{< slide template="hamzadark1" >}}

## Saga Pattern'e Giriş
Saga, mikroservis tabanlı uygulamalarda uzun süreli ve birden fazla adımdan oluşan işlemleri yönetmek için kullanılan bir iş akışı yönetim desenidir.

{{% /section %}}


---

{{% section %}}

## Saga'nın Amacı ve Faydaları


- Saga, dağıtık sistemlerde uzun süreli işlemleri güvenli bir şekilde yönetmek için kullanılır.
- İşlemleri adımlara bölerek hata durumunda her bir adımın telafi edilmesini sağlar.
- Sistemin genel dayanıklılığını artırır ve hata yönetimini daha yapılandırılmış bir şekilde ele alır.

---

{{< slide template="hamzadark1" >}}

## Saga Pattern'in Temel Bileşenleri

- **Choreography**
- **Orchestration**
- **Compensation**
- **Error Handling**

{{% note %}}
Error Handling (Hata Yönetimi)
Hata yönetimi, Saga Choreography'de her adımın hata durumunda telafi işlemlerini tetiklemesiyle gerçekleştirilir. Merkezi bir kontrol olmadığı için servisler kendi hatalarını olay tabanlı bir yaklaşımla yönetir ve durumu geri alır.
{{% /note %}}

---

{{< slide template="hamzadark2" >}}

## Saga Pattern'in Temel Bileşenleri
- **Event-Driven Communication**
- **Service Independence**
- **Real-Time Updates**
- **Distributed Transactions**

{{% note %}}
Event-Driven Communication (Olay Tabanlı İletişim)
Servisler arasında asenkron iletişim, olay tabanlı bir yapı ile sağlanır. Her servis, bir işlemi tamamladığında bir olay yayınlar ve bu olay, diğer servisler tarafından dinlenerek işlemlerin tetiklenmesini sağlar.

Service Independence (Servis Bağımsızlığı)
Choreography, her servisin kendi iş mantığını bağımsız olarak yönetmesini sağlar. Bu yapı, servislerin birbirinden izole olmasını ve kendi başlarına çalışabilmelerini mümkün kılar, böylece sistemin esnekliği artar.

Real-Time Updates (Gerçek Zamanlı Güncellemeler)
Olay tabanlı iletişim sayesinde servisler gerçek zamanlı olarak birbirleriyle etkileşime geçer. Bu sayede, sistemdeki güncellemeler anında diğer servisleri tetikler ve hızlı tepki süreleri sağlar.

Distributed Transactions (Dağıtık İşlemler)
Dağıtık işlemler, Saga Pattern ile adımlara bölünerek yönetilir. Her bir işlem adımı bağımsızdır ve hata durumunda telafi edici işlemlerle güvenilir bir şekilde geri alınabilir, bu da sistemin bütünlüğünü korur.
{{% /note %}}
{{% /section %}}

---

{{% section %}}

{{< slide template="hamzadark1" >}}

## Choreography vs Orchestration
***Choreography*** ve ***Orchestration***, Saga Pattern'in iki ana uygulama yöntemidir. Bu sunumda özellikle ***Choreography*** üzerine odaklanacağız.

---

{{< slide template="hamzadark1" >}}

## Choreography ve Orchestration Farkları
- **Choreography**: Servisler olaylar aracılığıyla birbirleriyle konuşur, merkezi bir kontrol yoktur.
- **Orchestration**: Merkezi bir kontrol birimi (orchestrator) tüm süreci yönetir ve kontrol eder.

{{% /section %}}

---

{{% section %}}


## Choreography Yapısının Özellikleri

- **Olay Tabanlı İletişim**: Servisler arasında asenkron olaylar yoluyla iletişim kurulur, bu da sistemin daha hızlı tepki vermesini sağlar.
- **Servislerin Bağımsızlığı**: Her servis kendi sorumluluğunda olan işi yapar ve diğer servislerden bağımsız çalışır. Bu, sistemin esnekliğini ve ölçeklenebilirliğini artırır.

---

{{< slide template="hamzadark1" >}} 

## Choreography Yapısının Özellikleri

- **Dağıtık Mimari için Uygunluk**: Choreography, dağıtık sistemlerde merkezi bir yönetim olmadan iş akışlarını etkin bir şekilde yönetir. Servisler kendi işlemlerini yönetirken olay tabanlı bir akışla ilerler.

{{% /section %}}

---

{{% section %}}

{{< slide template="hamzadark2" >}}

## Choreography'nin Avantajları
- Merkezi kontrol birimi yoktur; servisler bağımsızdır.
- Olay tabanlı iletişim, hızlı ve gerçek zamanlı güncellemeler sağlar.
- Sistemin esnekliği ve ölçeklenebilirliği yüksektir.

---

{{< slide template="hamzadark2" >}}

## Choreography'nin Dezavantajları ve Zorlukları
- Hata yönetimi karmaşıktır ve telafi işlemleri zor olabilir.
- Olayların izlenmesi ve yönetimi zordur (event storming).
- Servisler arasında beklenmeyen bağımlılıklar oluşabilir.
{{% /section %}}

---

{{% section %}}

{{< slide template="hamzadark1" >}}

### Compensation İşlemleri (Compensable Transactions)

- Başarısız adımları geri alarak sistemin önceki durumuna dönmesini sağlar.
- Telafi edici işlemler her adım için ayrı tanımlanır ve hata durumunda tetiklenir.
- Servisler bağımsız çalışırken kendi telafi işlemlerini yönetir.

---

{{< slide template="hamzadark1" >}}

### Hata Yönetimi

- Hatalar olaylar aracılığıyla yönetilir ve her adımda telafi işlemleri tetiklenir.
- Olay tabanlı hata yönetimi, olayların doğru izlenmesini ve uygun yanıt verilmesini gerektirir.
- Özellikle karmaşık hata senaryoları için dikkatli bir planlama ve güçlü telafi işlemleri gereklidir.
{{% /section %}}

---

{{< slide template="hamzadark2" >}}

# Demo

---

{{< slide template="hamzadark2" >}}
{{% slide notes="You found the notes!" %}}
{{% note %}}

- You found the **speaker notes**!
  {{% /note %}}

## Dinlediğiniz için teşekkürler

Kaynaklar: [A'dan Z'ye Mikroservis Mimarisi Eğitimi - 1. Etap](https://www.youtube.com/playlist?list=PLQVXoXFVVtp0sUDTpTiwerseU1nClYjEC) - [ChatGPT](https://chatgpt.com/)

Örnekler Reposu: [aimtune/distributed-systems-design-patterns-examples](https://github.com/AimTune/distributed-systems-design-patterns-examples/tree/main/saga-choreography)
