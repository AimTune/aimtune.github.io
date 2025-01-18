---
title: "Büyük Veri: Nedir, Teknolojileri"
date: 2024-01-18T21:14:06+01:00
description: Bu yazımızda, Büyük Veri (Big Data) kavramını, temel bileşenlerini ve teknolojilerini ele alıyoruz. Hadoop, Spark ve NoSQL gibi araçların bu alandaki rolünü açıklayarak, futbol sektörü gibi örneklerle kullanım alanlarına değiniyoruz. 
summary: Bu yazımızda, Büyük Veri (Big Data) kavramını, temel bileşenlerini ve teknolojilerini ele alıyoruz. Hadoop, Spark ve NoSQL gibi araçların bu alandaki rolünü açıklayarak, futbol sektörü gibi örneklerle kullanım alanlarına değiniyoruz. 
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Hamza Ağar
authorEmoji: 🤖
tags:
  - büyük veri
  - hadoop
  - spark
  - NoSQL
  - futbol
categories:
  - big-data-serisi
cascade:
  showSummary: true
---

Selamlar,  

Uzun zamandır üzerine araştırma yapmak istediğim ve geçmişte biraz da olsa öğrenmeye çalıştığım **Büyük Veri** konusuna olan ilgim yeniden canlandı. Bu kez, daha derinlemesine bir şekilde incelemek ve öğrendiklerimi bir yazı serisiyle paylaşmaya karar verdim. Ayrıca fırsatım olursa bu seride bir de futbol verileri üzerinde (veya başka bir veri üzerinde) basit de olsa bir büyük veri çalışması yapmak istiyorum. Bu süreçte de birçok farklı kaynaktan yararlanmaya çalışıyorum. [^1][^2][^3][^4][^5]

Peki o halde başlayalım, nedir bu **Büyük Veri (Big Data)**? Günümüzün dijital dünyasında büyük veri, işletmeler ve organizasyonlar için vazgeçilmez bir kaynak haline gelmiştir. Bu serinin ilk yazısında, büyük verinin ne olduğunu, temel bileşenlerini, **Hadoop**, **Spark** ve **NoSQL** gibi teknolojilerin bu alandaki rollerini ve futbol sektöründe nasıl uygulandıklarını inceleyeceğiz.

> Veriniz yoksa, sadece bir başka fikri olan insansınız.
> — <cite>W. Edwards Deming</cite>

> Veri, yeni petrole benzer.
> — <cite>Clive Humby</cite>

Keyifli okumalar!

## Büyük Veri (Big Data) Nedir?

Büyük veri, geleneksel veri işleme yöntemleriyle yönetilmesi ve analiz edilmesi zor olan, çok büyük hacimde ve çeşitli kaynaklardan gelen veri kümelerini ifade eder. Büyük veri, genellikle **5V** modeliyle açıklanır:

1. **Hacim (Volume):** Oluşturulan veri miktarının büyüklüğünü ifade eder. Örneğin, futbol maçlarında saniyede üretilen konum ve hareket verileri terabaytlarca bilgi oluşturabilir.
2. **Çeşitlilik (Variety):** Verinin farklı format ve türlerde olmasıdır; yapılandırılmış (oyuncu istatistikleri), yarı yapılandırılmış (JSON maç raporları) ve yapılandırılmamış (maç videoları) veri gibi.
3. **Hız (Velocity):** Verinin oluşturulma ve işlenme hızını belirtir. Örneğin, bir futbol maçında sensörlerden gelen veriler anlık olarak analiz edilebilir.
4. **Doğruluk (Veracity):** Verinin doğruluğu ve güvenilirliğidir. Maç istatistiklerinin hatasız ve anlamlı olması için veri kaynaklarının doğruluğu önemlidir.
5. **Değer (Value):** Verinin organizasyonlara sağladığı faydadır. Örneğin, oyuncu performans analizinden elde edilen bilgiler, antrenman programlarının optimize edilmesini sağlar.

### Kişisel yorumum

İncelediğim kaynaklarda, **5V modeli**nin özellikle ilk üç boyutu (Hacim, Çeşitlilik ve Hız) üzerinde daha fazla duruluyor. Ancak bana göre, son iki boyut olan **Doğruluk** ve **Değer**, en az ilk üçü kadar önemli.  

Örneğin, elimizde yalnızca bir şirkete ait on yıllık bir veri olduğunu düşünelim. Bu veriler satış ve yatırımları içeriyor olsun. Eğer bu verilerin içinde yalnızca şirket ismi gibi doğrudan anlam ifade etmeyen bilgiler varsa, bunlar bizim için pek bir değer taşımaz; aksine, gereksiz bir hesaplama maliyeti oluşturur. Ancak, bu verilere ek olarak şirketin o yıl içerisindeki **misyonu** ve **hedefleri** gibi bilgiler de kayıt altına alınmışsa, bu veriler satışlar üzerindeki etkileri analiz etmemizi sağlar. Böylece, elde edilen veriler daha anlamlı hale gelir ve çıktılarımız daha verimli olur.

Bu nedenle, verilerimizin yalnızca hacmi ve çeşitliliği değil, aynı zamanda **doğruluğu** ve sunduğu **değer** de büyük veri analizinde kritik öneme sahiptir.

---

## Hadoop Nedir?

**Hadoop**, büyük veri işleme için kullanılan açık kaynaklı bir framework'tür. Apache Vakfı tarafından geliştirilen bu sistem, çok büyük veri kümelerini dağıtık bir ortamda depolamak ve işlemek için tasarlanmıştır [^6]. Hadoop'un temel bileşenleri şunlardır:

- **HDFS (Hadoop Distributed File System):** Büyük veriyi dağıtık bir şekilde saklar.
- **MapReduce:** Büyük veri setlerini işlemeye yönelik bir programlama modeli.
- **YARN (Yet Another Resource Negotiator):** Kaynak yönetimini ve iş planlamasını sağlar.

Hadoop, futbol gibi veri yoğun sektörlerde büyük maç istatistiklerini saklamak ve analiz etmek için kullanılabilir. Bu kavramlara daha sonraki yazılarımızda ayrıntılı değineceğiz.

---

## Spark Nedir?

**Apache Spark**, büyük veri işleme için kullanılan hızlı bir veri analitik motorudur. Hadoop’a benzer şekilde dağıtık veri işlemeye odaklanır ancak Spark, özellikle **hafızada veri işleme (in-memory processing)** yeteneğiyle öne çıkar [^7].

- **Hızlı İşleme:** Spark, veriyi bellekte işlediği için analizlerde 100 kata kadar hız artışı sağlar.
- **Esneklik:** SQL, veri akışı (streaming) ve makine öğrenimi gibi farklı görevleri destekler.
- **Kullanım Alanları:** Gerçek zamanlı veri analizi, futbol maçlarında akış verilerinin anlık değerlendirilmesi gibi.

---

## NoSQL Nedir?

**NoSQL** (Not Only SQL), yapılandırılmamış veya yarı yapılandırılmış verilerin saklanması ve işlenmesi için tasarlanmış bir veritabanı türüdür [^8]. Örnek türler:

- **Doküman Tabanlı Veritabanları:** JSON veya BSON formatında verileri işler. Örneğin, **MongoDB**.
- **Anahtar-Değer Depoları:** Veriler anahtar-değer çiftleri olarak saklanır. Örneğin, **Redis**.
- **Graf Veritabanları:** Oyuncular arasındaki bağlantıları analiz etmek için kullanılabilir. Örneğin, **Neo4j**.

NoSQL, futbol maçlarında üretilen büyük veri setlerini hızlıca sorgulamak ve analiz etmek için ideal bir çözüm sunar.

---

## Futbol Sektöründe Büyük Veri Uygulamaları

Büyük veri, futbol sektöründe geniş bir uygulama alanı bulmuştur:

- **Oyuncu Performans Analizi:** Sensörler ve kameralarla toplanan veriler, oyuncuların hızını, dayanıklılığını ve taktik uyumunu ölçer.
- **Taktiksel Analiz:** Rakip takımların oyun düzenleri, büyük veri analitiği ile incelenir ve taktik geliştirilir.
- **Taraftar Deneyimi:** Taraftarların sosyal medya etkileşimleri analiz edilerek kişiselleştirilmiş kampanyalar oluşturulur.
- **Maç İstatistikleri:** Gerçek zamanlı analizlerle maç boyunca taktiksel değişikliklere olanak tanır.

Örneğin, Spark ve NoSQL veritabanları, bir futbol maçında saniyede üretilen milyonlarca veri noktasını işleyerek antrenörlere gerçek zamanlı raporlar sunabilir.

---

Büyük Veri (Big Data) alanında uzmanlaşmış profesyonellere olan talep, günümüz iş dünyasında hızla artmaktadır. Veri analistleri, veri mühendisleri ve veri bilimcileri gibi uzmanlar, şirketlerin stratejik kararlar almasına, operasyonel verimliliklerini artırmasına ve müşteri deneyimlerini iyileştirmesine yardımcı olmaktadır. Özellikle teknoloji, finans, sağlık ve perakende sektörlerinde büyük veri uzmanlarına olan ihtiyaç belirgin bir şekilde artmaktadır.

Türkiye'de de büyük veri alanında uzmanlaşmış profesyonellere yönelik iş ilanları bulunmaktadır. Örneğin, Veri Analiz Uzmanı pozisyonları, farklı sektörlerde faaliyet gösteren firmalar tarafından sıkça aranmaktadır.

Büyük Veri uzmanları, veri analitiği, makine öğrenimi ve yapay zeka gibi alanlarda derinlemesine bilgi ve deneyime sahip olmalıdır. Bu uzmanlık, onlara yüksek maaşlar ve hızlı kariyer ilerlemesi gibi avantajlar sunmaktadır.

Futbol kulüpleri de büyük veri mühendislerine ihtiyaç duymaktadır. Örneğin, Manchester United ve Liverpool gibi dev futbol kulüpleri, veri mühendisliği alanında uzmanlaşmış profesyoneller aramaktadır. Bu tür pozisyonlar, spor endüstrisinde veri biliminin önemini ve büyüklüğünü göstermektedir. [^9]

![Manchester United Job Post](/images/series/big-data/manu-job-post.png "LinkedIn'de Daha Önceden Paylaşılmış Bir İş İlanı")

[^1]: [Udemy - Yeni Başlayanlar için Big Data: NoSQL & Spark & Hadoop](https://www.udemy.com/course/big-data-hadoop-spark-nosql-egitimi)
[^2]: [Udemy - Sıfırdan Her Yönüyle Big Data ( Büyük Veri ) Eğitimi](https://www.udemy.com/course/sifirdan-her-yonuyle-bigdata)
[^3]: [Udemy - (50 Saat) Python A-Z™: Veri Bilimi ve Machine Learning](https://www.udemy.com/course/python-egitimi)
[^4]: [Udemy - Software Architecture & Technology of Large-Scale Systems](https://www.udemy.com/course/developer-to-architect)
[^5]: [ChatGPT](https://chatgpt.com)
[^6]: Apache Software Foundation. *Apache Hadoop Documentation*. [https://hadoop.apache.org](https://hadoop.apache.org)  
[^7]: Apache Software Foundation. *Apache Spark Documentation*. [https://spark.apache.org](https://spark.apache.org)  
[^8]: MongoDB, Inc. *MongoDB Official Website*. [https://www.mongodb.com](https://www.mongodb.com)  
[^9]: Lead Data Scientist [Liverpool Careers](https://careers.liverpoolfc.com/members/modules/job/detail.php?record=826)
