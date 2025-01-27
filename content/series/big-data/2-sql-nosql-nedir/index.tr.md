---
title: "SQL, NoSQL ve Büyük Veri: BASE, ACID ve CAP Teoremi"
date: 2025-01-27T23:28:06+01:00
description: "NoSQL veritabanlarının temelleri, BASE ve ACID arasındaki farklar, CAP Teoremi, büyük veriyle ilişkisi ve NoSQL veritabanı türleri."
tags: ["NoSQL", "ACID", "BASE", "CAP Teoremi", "Büyük Veri"]
categories: ["Veritabanları", "Teknoloji"]
---

NoSQL veritabanları, günümüzün büyük veri ve modern uygulama ihtiyaçlarını karşılamak için geleneksel ilişkisel veritabanlarından farklı bir yaklaşım sunar. Bu yazımızda, **SQL ve NoSQL** veritabanları arasındaki temel farklara, **ACID** ve **BASE** modelleri arasındaki ayrımlara, **CAP Teoremi**'nin büyük veri dünyasındaki önemine ve NoSQL'in sunduğu esnek mimariye odaklanacağız. Ayrıca, farklı NoSQL veritabanı türlerini (doküman, anahtar-değer, sütunlu ve graf veritabanları gibi) örneklerle inceleyeceğiz.[^1][^2][^3][^4][^5]

SQL veritabanları, özellikle veritabanı tutarlılığı ve karmaşık sorgular için güçlü bir yapı sunarken, NoSQL veritabanları daha esnek ve yatay ölçeklenebilir çözümler sunar. Bu yazıda, her iki yaklaşımın avantajlarını ve kullanım alanlarını karşılaştırarak, farklı veri gereksinimlerine nasıl hitap ettiklerini ele alacağız.

---

Böyle daha kapsamlı oldu! Uygun mudur?

## CAP Teoremi Nedir?

CAP Teoremi, Eric Brewer tarafından ortaya atılmış bir teoridir ve dağıtık sistemlerin üç temel özelliği aynı anda sağlayamayacağını ifade eder. Bu özellikler şunlardır:

1. **Consistency (Tutarlılık):** Sistem üzerinde gerçekleştirilen her okuma işlemi, son yazma işleminden sonra güncellenmiş bir veri döndürmelidir. Yani, tüm düğümler aynı veriyi görmelidir.
2. **Availability (Erişilebilirlik):** Her okuma veya yazma isteği, bir hata durumu olmadıkça, bir yanıt almalıdır. Sistem sürekli erişilebilir durumda kalmalıdır.
3. **Partition Tolerance (Bölümleme Toleransı):** Sistem, ağ bölünmeleri veya iletişim kesintileri gibi durumlarda bile çalışmaya devam edebilmelidir.

CAP Teoremi, üç özelliğin aynı anda sağlanamayacağını belirtir. Bu nedenle, NoSQL sistemlerinde genellikle iki özellik arasında bir denge kurulur:

- **AP (Availability ve Partition Tolerance):** Tutarlılıktan ödün verilerek sistem erişilebilirliği ve ağ bölünmesine dayanıklılık önceliklendirilir. Örnek: **Cassandra**, **DynamoDB**.
- **CP (Consistency ve Partition Tolerance):** Erişilebilirlikten ödün verilerek tutarlılık ve ağ bölünmesine dayanıklılık sağlanır. Örnek: **MongoDB**, **HBase**.
- **CA (Consistency ve Availability):** Bölümleme toleransı olmadan tutarlılık ve erişilebilirlik sağlanabilir. Geleneksel tek düğümlü SQL veritabanlarında bu model uygulanabilirken, pratikte dağıtık sistemlerde ağ bölünmeleri kaçınılmaz olduğundan bu yaklaşım sürdürülebilir değildir. Dağıtık SQL çözümleri genellikle tutarlılığı sağlamak için erişilebilirlikten ödün verir (**CP**).

Bu teorem, NoSQL veritabanlarının hangi koşullarda daha verimli olduğunu anlamak için kritik bir yol göstericidir.

---


## BASE ve ACID Nedir?

BASE ve ACID, veritabanı tasarımında farklı yaklaşımları ifade eden iki modeldir. Her iki model de veritabanlarının güvenilirliği, performansı ve ölçeklenebilirliği üzerinde farklı etkiler yaratır.

### ACID

ACID ilkeleri, ilişkisel veritabanlarının sağlam ve güvenilir bir şekilde çalışmasını sağlayan temel kurallardır:

- **Atomicity (Atomiklik):** Bir işlem ya tamamen gerçekleştirilir ya da hiç gerçekleştirilmez. İşlemin bir parçası başarısız olursa, işlem geri alınır ve veritabanı önceki durumuna döner.
- **Consistency (Tutarlılık):** Her işlem, veritabanını bir tutarlı durumdan diğerine taşır. Bu, işlem sonrası veritabanının tanımlanmış kurallara uygun bir duruma geçmesini sağlar.
- **Isolation (İzolasyon):** Aynı anda birden fazla işlem yürütüldüğünde, işlemler birbirinden etkilenmez.
- **Durability (Kalıcılık):** İşlem tamamlandığında, sonuçlar sistemde kalıcı olarak saklanır ve bir sistem hatası durumunda bile veri kaybı yaşanmaz.

### BASE

BASE yaklaşımı, NoSQL veritabanlarının daha esnek ve ölçeklenebilir bir şekilde çalışmasını sağlar:

- **Basically Available (Temelde Erişilebilir):** Sistem her zaman bir yanıt döndürür, ancak bu yanıt her zaman güncel olmayabilir.
- **Soft State (Geçici Durum):** Veriler, işlem süresince tutarlı olmayabilir ve sistemin durumu zamanla değişebilir.
- **Eventually Consistent (Sonunda Tutarlı):** Sistem, belirli bir süre içinde tutarlı bir duruma ulaşır. Verilerin anlık tutarlılığı yerine sonunda tutarlılık sağlanır.

BASE modeli, özellikle büyük ölçekli, dağıtık ve dinamik veri gereksinimlerinde tercih edilir. Örneğin, bir sosyal medya platformunda kullanıcının gönderilerini anlık olarak görmemesi büyük bir sorun teşkil etmez, ancak uzun vadede bu verilerin tutarlı hale gelmesi gerekir.

---

### ACID Prensiplerine Bir Örnek: Banka Hesapları
Ahmet, aynı banka hesabına bağlı iki farklı banka kartına sahiptir. Bir gün acil nakit ihtiyacı olur ve hem kendisi hem de kardeşi, farklı ATM'lerden aynı anda para çekmeye karar verir. Ahmet, ilk ATM'den **500 TL**, kardeşi ise ikinci ATM'den **400 TL** çekmeye çalışır.

Eğer veritabanı ACID prensiplerine uygun çalışmasaydı, bu işlemler birbiriyle uyumsuz şekilde yürütülürdü. Örneğin, hesapta yalnızca **700 TL** varsa ve her iki işlem aynı anda gerçekleşirse, veritabanı bu çekimlerden yalnızca birini kaydeder veya hatalı bir bakiye gösterirdi. Ahmet’in **500 TL** çektiği işlem kaydedilmiş gibi görünürken, kardeşinin çektiği **400 TL** işlem de gerçekleşmiş olabilir ve toplamda **900 TL** çekilmesine rağmen hesapta hala **200 TL** varmış gibi görünebilirdi. Bu, banka sisteminin tutarsızlık yaşamasına ve müşterilerin yanlış bilgiye ulaşmasına neden olurdu.

{{< alert >}}
ACID prensipleri sayesinde bu durumun önüne geçilir. Veritabanı işlemleri bir bütün olarak ele alır ve bir işlem tamamlanmadan diğerine izin vermez. Böylece, hesap bakiyesi her zaman doğru ve tutarlı bir şekilde yansıtılır. Bu prensip, özellikle finansal işlemler gibi kritik süreçlerde büyük önem taşır.
{{< /alert >}}

### BASE Prensiplerine Bir Örnek: Sosyal Medya
Öte yandan, BASE prensipleri farklı bir yaklaşımı benimser ve genellikle sosyal medya platformlarında karşımıza çıkar. Örneğin, bir ünlü Instagram’da bir paylaşım yaptığında, gönderinin altında beğeni sayısının tam olarak **1.101.000** ya da sadece **1.1 milyon** olarak görünmesi pek önemli değildir.

Kullanıcılar için önemli olan, bu gönderinin milyonlarca kişi tarafından beğenildiğinin anlaşılmasıdır; beğeni sayısının kesinliği anlık olarak kritik değildir. Bu yüzden, BASE prensiplerini izleyen sistemler, beğeni sayısını zamanla günceller ve süreç sonunda tutarlı bir hale getirir. Bu sayede sistem, yüksek ölçeklenebilirliği koruyarak kullanıcı deneyimini hızlı bir şekilde sunar.

{{< alert >}}
Bu iki senaryo, ACID ve BASE arasında yapılan temel tercihlerin, farklı kullanım alanları için neden önemli olduğunu anlamamızı sağlar. Kimi zaman kesinlik ve güvenilirlik (ACID), kimi zaman da ölçeklenebilirlik ve esneklik (BASE) ön planda olmalıdır.
{{< /alert >}}

---

### Doğru Veritabanı Seçiminin Önemi: Gerçek Bir Olay

Bu hikaye, adını paylaşmak istemediğim eski bir yazılımcı arkadaşımın deneyimlerinden geliyor. Bu arkadaşım, iyi bir müşteri kitlesi olan bir e-ticaret sitesi için **MongoDB** kullanarak bir otomasyon sistemi geliştirdi. Ancak sistem, bir dönem yoğun trafik aldığında, **BASE** modelinin "Eventually Consistent" özelliği nedeniyle veritabanına hatalı veriler yazdı. Bunun sonucunda firma, stokta olmayan ürünleri satmaya devam etti ve farkında olmadan binlerce lira zarara uğradı.

Bu olay, veritabanı seçimi ve yapılandırmasının yalnızca bir teknoloji kararı olmadığını, aynı zamanda iş süreçlerini doğrudan etkileyen kritik bir tercih olduğunu gösteriyor. Özellikle tutarlılığın öncelikli olduğu sistemlerde, ihtiyaç analizi ve doğru yapılandırma hayati önem taşır.

---

## NoSQL Veritabanlarının Gelişimi ve Büyük Veriyle İlişkisi

NoSQL veritabanlarının popülerliği, özellikle büyük veri ve dağıtık sistemlerin ortaya çıkmasıyla birlikte hızla artmıştır. Geleneksel ilişkisel veritabanları (SQL), yüksek hacimli, hızlı büyüyen ve çeşitli veri türlerini işlemek için yeterince esnek değildir. NoSQL veritabanları bu boşluğu doldurur ve aşağıdaki avantajları sağlar:

1. **Yatay Ölçeklenebilirlik:** Veritabanı sistemi, donanım kapasitesini artırmak yerine yeni düğümler eklenerek kolayca genişletilebilir.
2. **Dinamik Şema:** Yapılandırılmamış veya yarı yapılandırılmış verilerle çalışmak için daha uygundur.
3. **Performans:** Hızlı sorgulama ve düşük gecikme süreleri sunar.
4. **Çeşitlilik:** Farklı kullanım senaryolarına uygun çeşitli NoSQL türleri bulunmaktadır.
5. **Büyük Veri Çözümleri ile Entegrasyon:** NoSQL sistemleri, genellikle büyük veri işleme için kullanılan **Apache Hadoop** gibi platformlarla kolayca entegre olabilir. Hadoop’un HDFS (Hadoop Dağıtık Dosya Sistemi) ve MapReduce teknolojileri, büyük veri kümelerinin işlenmesinde önemli bir rol oynar.

Büyük veri, verinin hacmi, çeşitliliği ve hızı (3V: Volume, Variety, Velocity) ile karakterize edilir. Bu tür verilerle başa çıkmak için NoSQL veritabanları ve Hadoop gibi büyük veri teknolojileri daha iyi bir çözüm sunar.

---

## NoSQL Veritabanı Türleri ve Kullanım Alanları

### 1. **Doküman Veritabanları**
- **Özellikleri:** Veriler JSON, BSON veya XML formatında saklanır. Belge odaklı yapı, esnek veri modellemesi sağlar.
- **Kullanım Alanları:** İçerik yönetim sistemleri, kataloglar.
- **Örnekler:** MongoDB, Couchbase.

### 2. **Anahtar-Değer Veritabanları**
- **Özellikleri:** Veriler, anahtar-değer çiftleri olarak saklanır. Basit ama hızlı bir erişim modeli sunar.
- **Kullanım Alanları:** Önbellekleme, oturum yönetimi.
- **Örnekler:** Redis, DynamoDB.

### 3. **Graf Veritabanları**
- **Özellikleri:** Düğümler ve kenarlarla, veriler arasındaki ilişkileri modellemek için idealdir.
- **Kullanım Alanları:** Sosyal ağlar, öneri sistemleri.
- **Örnekler:** Neo4j.

### 4. **Arama ve Analitik Veritabanları**
- **Özellikleri:** Veriler, tam metin arama, analiz ve filtreleme için optimize edilir. Elasticsearch, dağıtık bir altyapıda ölçeklenebilir sorgular sunar. JSON formatında veri saklar ve hızlı arama için ters indeksleme kullanır.
- **Kullanım Alanları:** Log analitiği, metin analitiği, öneri sistemleri, büyük veri ile gerçek zamanlı analiz.
- **Örnekler:** Elasticsearch, Apache Solr.

### 5. **Geniş Sütunlu Veritabanları**
- **Özellikleri:** Veriler sütun bazlı olarak organize edilir. Büyük veri analitiği için optimize edilmiştir.
- **Kullanım Alanları:** IoT verileri, log analitiği, büyük veri analitiği.
- **Örnekler:** Apache Cassandra, HBase (Hadoop ile birlikte çalışır).

HBase, **Apache Hadoop** ekosisteminin bir parçası olup, büyük ölçekli veri kümelerini işlemeye olanak sağlar. HDFS ile birlikte çalışarak verilerin dağıtık bir şekilde saklanmasını ve sorgulanmasını sağlar. Özellikle büyük veri analitiği ve gerçek zamanlı uygulamalar için ideal bir çözüm sunar.

### 6. **Zaman Serisi Veritabanları**
- **Özellikleri:** Zaman damgasıyla ilişkili veriler için özelleşmiştir.
- **Kullanım Alanları:** Sensör verileri, IoT.
- **Örnekler:** InfluxDB, TimescaleDB.

---

## Geleneksel SQL ve NoSQL Sistemlerinin Karşılaştırılması

| **Özellik**           | **SQL**                                      | **NoSQL**                                |
|-----------------------|---------------------------------------------|-----------------------------------------|
| **Veri Yapısı**       | Sabit şemalı ve ilişkisel.                  | Esnek şemalı ve ilişkisel olmayan.      |
| **Ölçeklenebilirlik** | Dikey ölçeklenebilir (daha güçlü sunucular). | Yatay ölçeklenebilir (daha fazla düğüm). |
| **Performans**        | Karmaşık sorgular için optimize edilmiştir. | Büyük veri ve düşük gecikme için uygundur. |
| **Kullanım Alanları** | Finansal işlemler, geleneksel iş uygulamaları. | Büyük veri, IoT, sosyal medya uygulamaları. |

---

## Sonuç
NoSQL veritabanları, modern uygulamaların gereksinimlerini karşılamak adına esneklik ve ölçeklenebilirlik sunar. Büyük veri işleme, IoT ve gerçek zamanlı uygulamalar gibi alanlarda sağladığı avantajlar ise bu teknolojiyi öne çıkarır. Ancak bir veritabanı seçmeden önce, BASE ve ACID modelleri arasındaki farkları anlamak ve uygulamanın ihtiyaçlarını doğru şekilde analiz etmek kritik öneme sahiptir.

Bu yazıda, NoSQL sistemlerinin temel kavramlarına odaklandık. Gelecek yazılarımızda ise **Apache Hadoop**, **Spark**, ve **Kafka** gibi veri akışının yoğun olduğu sistemlerde izlenmesi gereken yolları detaylıca ele alacağız. Bir sonraki yazıda görüşmek üzere! :smiling_face_with_smiling_eyes:

[^1]: [What’s the Difference Between an ACID and a BASE Database?](https://aws.amazon.com/compare/the-difference-between-acid-and-base-database/)
[^2]: [ACID Model vs BASE Model For Database](https://www.geeksforgeeks.org/acid-model-vs-base-model-for-database/)
[^3]: [Udemy - Software Architecture & Technology of Large-Scale Systems](https://www.udemy.com/course/developer-to-architect)
[^4]: [ChatGPT](https://chatgpt.com)