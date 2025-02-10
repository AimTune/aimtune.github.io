+++
weight=3
+++


{{% section %}}

{{< slide template="darkslide3" >}}

### Kurulum


![OpenTelemetry Console Packages](/images/series/opentelemetry/opentelemetry-package.png)
Bu paketleri yüklüyoruz.

---

{{< slide template="darkslide3" >}}

### Console Demo

![OpenTelemetry Console Demo](/images/series/opentelemetry/console-demo.png)

---

{{< slide template="darkslide3" >}}

### Console Demo

![OpenTelemetry Console Demo Output](/images/series/opentelemetry/console-demo-output.png)

{{% /section %}}

---

{{< slide template="darkslide3" >}}

## OpenTelemetry'deki Temel Kavramlar

---

{{% section %}}

{{< slide template="darkslide3" >}}

## Resource Nedir ve Nasıl Yapılandırılır?

OpenTelemetry’de **Resource**, hangi servis veya uygulamanın veri ürettiğini tanımlayan ve telemetri (Trace, Metrics, Logs) verilerine bağlam kazandıran meta bilgileri içerir. Bu sayede, ürettiğiniz verilerin **hangi servis** tarafından, **hangi sürümde**, **hangi ortamda** (örn. dev, preprod, prod) veya **hangi instance** (kopya) üzerinden geldiğini anlayabilirsiniz.

---

{{< slide template="darkslide4" >}}

### Resource Üzerinde Tanımlanabilen Bilgiler

1. **Service Name**
   - Uygulama veya servisin adı. (Örneğin: `PaymentService`)

2. **Service Version**
   - Uygulamanın hangi sürümünün çalıştığını belirtir. (Örneğin: `1.0.0`)

---

{{< slide template="darkslide4" >}}

### Resource Üzerinde Tanımlanabilen Bilgiler

3. **Namespace**
   - Bir uygulama veya servis ailesinin/alanının adı olarak düşünebilirsiniz. (Örneğin: `MyCompanyName.PaymentSystem`)

4. **Instance**
   - Servisin belirli bir kopyası. (Örneğin: `payment-service-instance-2`)

---

{{< slide template="darkslide4" >}}

### Resource Üzerinde Tanımlanabilen Bilgiler

5. **Deployment Environment** (örn. `dev`, `preprod`, `prod`)
   - **Static property** olarak veya değişken üzerinden tanımlayabilirsiniz. Böylece telemetri verilerinin **hangi ortamdan** geldiği kolayca anlaşılır.

---

{{< slide template="darkslide3" >}}

### Örnek Resource Tanımı

```csharp{1|2-12|3-6|7-11|14|15}
var tracerProvider = Sdk.CreateTracerProviderBuilder()
    .SetResourceBuilder(
        ResourceBuilder.CreateDefault()
            .AddService(
              serviceName: "PaymentService",
              serviceVersion: "1.0.0")
            .AddAttributes(new Dictionary<string, object>
            {
                ["deployment.environment"] = "dev", // Ortam bilgisi
                ["service.instance.id"] = "instance-001" // Instance
            })
    )
    // Exporter vb. diğer ayarlar
    .AddConsoleExporter()
    .Build();
```
{{% /section %}}

---

{{% section %}}

{{< slide template="darkslide5" >}}

## AgentSource (TraceProvider)

- **Tanım**: Uygulamada **trace verilerinin üretildiği** ana sınıflardır.
- **Amaç**: Trace verilerini oluşturarak, hangi işlemlerin ne kadar sürdüğünü ve hangi bileşenler arasında gerçekleştiğini izlememizi sağlar.

---

{{< slide template="darkslide5" >}}

### AgentSource (TraceProvider)

- **Tasarım**:
  - **Static veya Singleton** şeklinde tasarlanmalıdır, böylece uygulama içinde merkezi ve tutarlı bir yerden yönetilebilir.
  - Benzer şekilde, `namespace` yapısını kullanarak farklı **traceleri** mantıksal olarak ayırabilir veya gruplandırabilirsiniz.

---

{{< slide template="darkslide5" >}}

### AgentSource (TraceProvider)

- **Faydalar**:
  - Uygulamanın belirli kısımlarından veya mikroservislerden üretilen verileri **daha düzenli** takip etme olanağı sunar.
  - Tek noktada konfigüre edildiğinden, **kaynak yönetimi** (örneğin, tek bir Tracer Provider üzerinden farklı bileşenlerin izlenmesi) kolaylaşır.
  - **Şeffaf gözlemlenebilirlik** elde etmeye yardımcı olur, çünkü tüm izleme (tracing) aktiviteleri ortak bir kayıt noktası üzerinden yönetilir.

{{% /section %}}

---

{{% section %}}

{{< slide template="darkslide4" >}}

## Activity (Span)

- Uygulamadaki her bir operasyon, bir **span** (örneğin: HTTP isteği, veritabanı çağrısı, dosya yazma) şeklinde temsil edilir.
- Bu span’lerin bir araya gelmesiyle bir **trace** (işlem bütünlüğü) oluşur.

---

{{< slide template="darkslide4" >}}

#### Span İçeriği

- **Start-end time**: Span’in başlama ve bitiş zamanı
- **Success-failure**: İşlemin başarılı mı yoksa hatalı mı sonuçlandığı
- **Span kind**: Span’in rolü (client, server, consumer, producer, internal)
- **Attributes/Tags**: Operasyona dair ek bilgiler (örn. kullanıcı kimliği, sürüm bilgisi vb.)
- **Events**: Span sürecindeki belirli olaylar veya kontrol noktaları (checkpoints)

---

{{< slide template="darkslide4" >}}

### Span ve Trace Arasındaki İlişki

- **Span**: Tek bir operasyonu temsil eder.
- **Trace**: Birden fazla span’in birleşerek oluşturduğu, uçtan uca bütün bir işlemi ifade eder.

---

{{< slide template="darkslide4" >}}

#### Activity (Span) Kind

- **Internal**: Uygulama içindeki dahili bir işlemi ifade eder.
- **Server**: İstekleri sunucu tarafında karşılayan veya işleyen taraftır.
- **Client**: Dış bir kaynağa veya hizmete istek gönderen taraftır.
- **Producer**: Mesaj veya veri üreterek bir kuyruğa, topic’e veya başka bir yere yayımlayan taraftır.
- **Consumer**: Yayınlanmış mesajları veya event’leri alan ve işleyen taraftır.

{{% /section %}}

---

{{< slide template="darkslide5" >}}

## Event

- **Event**, bir span’in (Activity) içerisindeki belirli bir olayı veya noktayı temsil eder.
- **Log benzeri** bir yapısı olsa da **in-memory** tutulduğu için (doğrudan bellekte saklanır), çok sık kullanılması **yüksek maliyet** doğurabilir.
- Örneğin, “Bu dosyayı oluşturdum, boyutu 50 KB” şeklindeki bir bilgiyi **Event** olarak ekleyebilirsiniz.

---

{{< slide template="darkslide4" >}}

## Activity(Span) Status

Bir span’in durumunu belirlemek için üç temel **Status** tipi vardır:

- **Ok**
- **Error**
- **Unset**

Başarısız bir işlem (ör. istisna, hata kodu) oluştuğunda span durumunu **Error** olarak ayarlayabilirsiniz.

---

{{< slide template="darkslide4" >}}

## Tag (Attributes)

- Span’e ek bilgi (metadata) eklemek için kullanılır.
- **Örnek:** Sipariş ID, kullanıcı ID, işlem türü gibi bilgileri, span ile ilişkilendirerek daha ayrıntılı takip edebiliriz.
- İleride analiz yaparken veya sorun giderirken, bu etiketler sayesinde hangi işlemin hangi kullanıcı veya siparişle ilgili olduğunu hızlıca bulabilirsiniz.

---

{{< slide template="darkslide3" >}}

### Correlations (In-Process)

- Bir uygulama içindeki veya farklı servisler arasındaki **span**’lerin birbirine bağlı olduğu durumu ifade eder.
- İstek, bir servis/uygulamadan diğerine aktarıldığında, **traceId** paylaşılır ve böylece bütün **istek zinciri** aynı iz (trace) altında toplanır.
- Bu sayede **APM** (Application Performance Monitoring) araçlarında tek bir iz (trace) içerisinde, çoklu servis ve işlem adımlarını **uçtan uca** takip edebilirsiniz.

---

{{% section %}}

{{< slide template="darkslide2" >}}

## Activity.Current

- **Tanım**: .NET uygulamalarında **halihazırda etkin (aktif) olan `Activity` nesnesine** (span) erişim sağlar.
- **Kullanım**: Aşağıdaki örnek, `Activity.Current` üzerinden mevcut işlem (span) bilgisini elde etmeye yarar. Örneğin, etiket eklemek veya durum güncellemesi yapmak istediğinizde `Activity.Current?.SetTag("key", "value")` şeklinde çağrı yapabilirsiniz.

---

{{< slide template="darkslide2" >}}

### Activity.Current

- **Örnek Senaryo**:
  1. **Bir HTTP isteği** geldiğinde, yeni bir `Activity` başlatılır (veya otomatik başlatılır).
  2. Bu süreçte, **`Activity.Current`** o anki isteği temsil eden span’i gösterir.
  3. Ek etiketler, event’ler veya hata durumlarıyla ilgili kayıtlar bu aktif `Activity` üzerinden yapılır.

**Önemli Not**: `Activity.Current`, her zaman aktif bir işlem (span) olmayabilir. Bu nedenle, kod yazarken `null` durumlarını dikkate almak gereklidir.

{{% /section %}}

---

{{% section %}}

{{< slide template="darkslide2" >}}

## ActivityListener

- **Tanım**: .NET uygulamalarında, oluşturulan veya bitirilen `Activity` (yani Span) nesnelerini **dinlemek** (listen) ve yönetmek için kullanılan bir mekanizmadır.
- **Amaç**: Uygulamada hangi `Activity`’lerin (işlemlerin) **izlenmesi**, **örneğin** hangilerinin kaydedilmesi veya kaydedilmemesi gerektiğine karar vermenizi sağlar.

---

{{< slide template="darkslide2" >}}

## ActivityListener

- **Nasıl Çalışır**:
  1. **ActivityListener** nesnesi oluşturulur.
  2. İlgili geribildirim (callback) yöntemleri tanımlanır, örneğin:
     - `ShouldListenTo` (hangi `ActivitySource`’ları dinlemek istediğimizi belirtir)
     - `Sample` (hangi `Activity`’lerin başlatılıp başlatılmayacağına karar verir)
     - `ActivityStarted`/`ActivityStopped` (bir `Activity` başladığında veya bittiğinde çalışacak event metodları)
  3. Bu listener, **ActivitySource** nesnesine veya genel `ActivitySource.AddActivityListener(activityListener)` gibi bir API üzerinden eklenir.

---

{{< slide template="darkslide3" >}}

#### Örnek Kullanım

```csharp{1|2|8-36|10-15|17-23|25-29|31-35|38-39}
using System;
using System.Diagnostics;

public class ActivityListenerExample
{
    public static void SetupListener()
    {
        var listener = new ActivityListener
        {
            // Hangi ActivitySource'ları dinleyeceğimize karar veriyoruz.
            ShouldListenTo = (activitySource) =>
            {
                // Örneğin, "MyCompany.MyApp" adındaki ActivitySource’lara izin ver
                return activitySource.Name.Contains("MyCompany.MyApp");
            },

            // Activity oluşturulmadan önce “örnekleme” kararı veriyoruz (ör. kaydetsin mi kaydetmesin mi).
            Sample = (ref ActivityCreationOptions<ActivityContext> options) =>
            {
                // Belli bir mantığa göre (ör. rastgele yüzdelik, environment bilgisi vb.) karar verebilirsiniz.
                // Örnekte tüm Activity'leri kaydediyoruz:
                return ActivitySamplingResult.AllDataAndRecorded;
            },

            // Activity başladığında çalışacak callback
            ActivityStarted = activity =>
            {
                Console.WriteLine($"Activity Started: {activity.DisplayName}");
            },

            // Activity bittiğinde çalışacak callback
            ActivityStopped = activity =>
            {
                Console.WriteLine($"Activity Stopped: {activity.DisplayName}");
            }
        };

        // Listener'ı default ActivitySource'a ekliyoruz.
        ActivitySource.AddActivityListener(listener);
    }
}
```

---

{{< slide template="darkslide3" >}}

### Bu Örnekte

- **ShouldListenTo**: Hangi **ActivitySource**’ları dinlemek istediğimizi belirtiyoruz.
- **Sample**: Hangi **Activity**’lerin gerçekten oluşturulacağını veya kaydedileceğini kontrol edebiliyoruz.
- **ActivityStarted** ve **ActivityStopped**: Oluşturulan **Activity**’lerin başlangıç ve bitiş anlarında özel işlem yapabiliyoruz (örnek olarak konsola yazma).

---

{{< slide template="darkslide3" >}}

### Neden Önemli?

- **Filtreleme**: Çok fazla **Activity** oluşturulduğunda, dinlemek istediklerimizi kısıtlayarak sistem yükünü azaltabilirsiniz.
- **Merkezi Yönetim**: Tracing mantığını uygulamanın çeşitli yerlerine serpmek yerine, tek bir noktadan (**ActivityListener**) yönetebilirsiniz.

---

{{< slide template="darkslide3" >}}

### Neden Önemli?

- **Esneklik**: Gerçek zamanlı olarak hangi span’lerin kaydedilmesi gerektiğini değiştirerek (örneğin, hata modunda tüm tracing’i aktif hale getirerek) sistem davranışını dinamik olarak ayarlayabilirsiniz.
- **İnce Ayar**: Özel mantıklar (ör. belirli bir kullanıcıya veya siparişe ait **Activity**’leri kaydetme) tanımlayarak ince düzeyde kontrol sağlayabilirsiniz.

{{% /section %}}