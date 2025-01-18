+++
title = "Dapr Bölüm 1"
summary = "Bu sunumda modern mikroservis mimarileri için güçlü bir sidecar aracı olan **Dapr**'ı (Distributed Application Runtime) keşfedeceğiz. Sunumda değinilecek Dapr konuları: **Service Invocation** (Servis Çağırma), **State Management** (Durum Yönetimi), Secrets Management (Gizli Veri Yönetimi), **Configuration** (Yapılandırma), **Resiliency** (Dayanıklılık)."
date = 2024-07-28T22:53:10+03:00
topics = ["Dapr", "Mikroservisler", "Kubernetes", "Redis", "JavaScript", "Node.js", "Sidecar Pattern", "Cross Cutting Concerns"]
layout = "list"
outputs = ["Reveal"]
[reveal_hugo]
theme = "night"
margin = 0.2

+++

{{% section %}}
{{< slide template="hamzadark1" >}}

# Dapr

(Distributed Application Runtime)
<br />
<img src="/images/slides/dapr/dapr-logo.png" height="300" style="border: none;background-color: transparent;"/>

---

{{< slide template="hamzadark2" >}}

## Dapr'a Giriş

Dapr, mikroservis tabanlı uygulamaların geliştirilmesini ve çalıştırılmasını kolaylaştıran, open-source bir sidecar ürünüdür.

{{% /section %}}

---

{{% section %}}
{{< slide template="hamzadark1" >}}

## Sidecar Pattern Nedir?

Sidecar Pattern, yardımcı bir bileşenin (sidecar) ana uygulamaya eklenmesiyle (container veya process), uygulamanın iş mantığına müdahale etmeden ortak görevlerin yürütülmesini sağlar. Güvenlik, logging ve dinamik yapılandırma gibi cross cutting concerns'leri yönetmek için idealdir.

---

{{< slide template="hamzadark2" >}}

### Cross Cutting Concerns Nedir?

Cross cutting concerns, yazılım sisteminde birçok modül veya katmanda ortak olan ve tekrarlanan fonksiyonel özelliklerdir. Güvenlik, logging, hata yönetimi, performans izleme gibi konular bu kapsamda değerlendirilir. Bunlar, sistemin bakımını ve genişletilebilirliğini artırır.

---

{{< slide template="hamzadark3" >}}

### Sidecar Pattern'in Avantajları

- Yardımcı hizmetleri izole eder.
- Uygulamanın modülerliğini ve yeniden kullanılabilirliğini artırır.
- Yönetimi ve bakımı kolaylaştırır.

---

{{< slide template="hamzadark2" >}}

### Örnek Sidecar: Resiliency (Dayanıklılık)

- Resiliency, bir sistemin hatalardan kurtulma ve hizmet vermeye devam etme yeteneğidir. Sidecar kullanarak bir mikroservise resiliency özellikleri
  eklemek, özellikle ağ hataları veya diğer geçici sorunlar durumunda hizmet sürekliliğini sağlamak için etkilidir. Bu sidecar, otomatik yeniden deneme
  (retry), devre kesici (circuit breaker) ve zaman aşımı (timeout) gibi dayanıklılık desenlerini uygular.

---

{{< slide template="hamzadark2" >}}

### Örnek Sidecar: Resiliency (Dayanıklılık)

- Bizler de sidecar'larda örneği uygulamamıza gelen trafiği sadece sidecar üstünden alabiliriz ve gelen istekleri sidecar içerisinde resiliency görevi
  görecek kodlardan geçiririz ve uygulamamızın ayakta olmadığı durumda resiliency policy'lerine göre tekrar istek atma veya istek durdurma sürecine geçer.

{{% /section %}}

---

{{< slide template="hamzadark1" >}}

## Dapr'ın Amacı ve Faydaları

{{% fragment %}}

- Uygulama mantığını değiştirmeden dağıtılmış sistemlerin yaygın ihtiyaçlarını karşılamak için çeşitli yapı taşları (building blocks) ve birçok farklı özellik sunar.{{% /fragment %}}
  {{% fragment %}}
- HTTP ve gRPC protokolleri üzerinden çalışarak çoklu programlama dilleriyle uyumluluk sunar.
  {{% /fragment %}}
  {{% fragment %}}
- Kolay programlayabilmek için birçok farklı dilde SDK'ları vardır.
  {{% /fragment %}}

---

{{< slide template="hamzadark2" >}}

### Dapr'ın Temel Bileşenleri

{{% fragment %}}

##### Service Invocation\*

{{% /fragment %}}
{{% fragment %}}

##### State Management\*

{{% /fragment %}}
{{% fragment %}}

##### Secrets Management\*

{{% /fragment %}}
{{% fragment %}}

##### Configuration\*

{{% /fragment %}}

---

{{< slide template="hamzadark2" >}}

### Dapr'ın Temel Bileşenleri

{{% fragment %}}

##### Pub/Sub Messaging

{{% /fragment %}}
{{% fragment %}}

##### Bindings

{{% /fragment %}}
{{% fragment %}}

##### Distributed lock

{{% /fragment %}}
{{% fragment %}}

##### Cryptography

{{% /fragment %}}
{{% fragment %}}

##### Actors

{{% /fragment %}}
{{% fragment %}}

##### Workflow

{{% /fragment %}}

---

{{< slide template="hamzadark2" >}}
{{% section %}}

## Dapr'ın Diğer Özellikleri

<br>

### Resiliency\*

Hata toleransı sağlamak için zaman aşımı, yeniden deneme, devre kesici ve geri çekilme gibi politikalar tanımlamayı ve uygulamayı destekler.

---

## Dapr'ın Diğer Özellikleri

<br>

### Observability

Open Telemetry ve Zipkin gibi protokollerle izleme verilerini toplar ve birçok gözlemlenebilirlik aracıyla entegrasyon sağlar.

---

## Dapr'ın Diğer Özellikleri

<br>

### Security

Varsayılan olarak etkin güvenlik özellikleri sunar, API'lar, servisler ve bileşenler için uygulamaya özel politikalar ayarlama imkanı sağlar. İletişim mTLS ile otomatik olarak şifrelenir.

{{% /section %}}

---

{{< slide template="hamzadark1" >}}

## Service Invocation

{{% fragment %}}Mikroservisler arası iletişim sağlar.{{% /fragment %}}
{{% fragment %}}HTTP veya gRPC ile çalışır.{{% /fragment %}}
{{% fragment %}}Servis keşfi ve yük dengeleme özellikleri içerir.{{% /fragment %}}
{{% fragment %}}Servislerdeki iletişimde araya girdiği için security, resiliency, observability gibi yapıları da bu istekler çalıştığı anda uygulayabilir.{{% /fragment %}}

---

{{< slide template="hamzadark1" >}}
{{% section %}}

## State Management

{{% fragment %}}Uygulamalarda durum (state) kalıcılığı sağlar. {{% /fragment %}}

{{% fragment %}}Key/value tabanlı durum depolamada görev alır. {{% /fragment %}}

{{% fragment %}}Farklı ürünler ile entegre edilebilir (Redis, MongoDB, SQLs\*, In-Memory, etcd, vb...). {{% /fragment %}}

---

## State Management

![State Store Example](/images/slides/dapr/statestore.png)
{{% note %}}

```yaml{}
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: statestore
```

{{< highlight yaml >}}

apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
name: statestore

{{< /highlight >}}
{{% /note %}}
{{% /section %}}

---

{{< slide template="hamzadark1" >}}
{{% section %}}

## Secrets Management

{{% fragment %}}Güvenlik açısından hassas bilgilerin korunmasını sağlar.{{% /fragment %}}
{{% fragment %}}Şifreler, API anahtarları, güvenlik sertifikaları gibi gizli bilgilerin yönetimini içerir.{{% /fragment %}}
{{% fragment %}}Erişim kontrolü ve şifreleme kullanılarak güvenli bir şekilde saklanır ve erişilir.{{% /fragment %}}
{{% fragment %}}Farklı ürünler ile entegre edilebilir (Azure Key Vault, AWS Secrets Manager, HashiCorp Vault, vb.).{{% /fragment %}}

---

## Secrets Management

![Secrets Management Example](/images/slides/dapr/secretstore.png)

{{% note %}}

```yaml{}
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: statestore
```

{{< highlight yaml >}}

apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
name: statestore

{{< /highlight >}}
{{% /note %}}
{{% /section %}}

---

{{< slide template="hamzadark1" transition="zoom" transition-speed="fast" class="side-by-side" >}}

{{% section %}}

## Configuration Management

{{% fragment %}}Uygulamanın çalışma şeklini belirleyen ayarların yönetimini sağlar.{{% /fragment %}}
{{% fragment %}}Uygulama ayarları, çevresel değişkenler ve yapılandırma dosyalarını içerir.{{% /fragment %}}
{{% fragment %}}Uygulama yeniden başlatılmadan veya kod değiştirilmeden kolayca güncellenebilir.{{% /fragment %}}
{{% fragment %}}Farklı ürünler ile entegre edilebilir (Redis, Consul, Kubernetes ConfigMaps, Azure App Configuration vb.).{{% /fragment %}}

---

## Configuration Management

![Configuration Management Example](/images/slides/dapr/configstore.png)
{{% note %}}

```yaml{}
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: statestore
```

{{< highlight yaml >}}

apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
name: statestore

{{< /highlight >}}
{{% /note %}}
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

Kaynaklar: [dapr.io](https://dapr.io/) - [ChatGPT](https://chatgpt.com/)

Örnekler Reposu: [aimtune/dapr-examples](https://github.com/AimTune/dapr-examples)
