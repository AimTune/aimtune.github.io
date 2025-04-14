+++
title = "Agentlar, Tools ve n8n"
summary = "Agentlar, Tools ve n8n hakkında temel bilgiler ve kullanım senaryoları"
date = 2025-04-16T22:53:10+03:00
topics = ["AI", "Otomasyon", "n8n", "Agent", "Tools", "MCP"]
layout = "list"
outputs = ["Reveal"]
[reveal_hugo]
theme = "night"
transition = "slide"

#theme = "night"
#margin = 0.2
+++

# Agent'lar ve n8n

---

{{% section %}}

# Agents ve Tools

- Modern sistemlerde entegrasyon ihtiyacı
- Süreç otomasyonu ve veri aktarımı
- Yapay zeka destekli karar alma

---

## Agent Nedir?
- Bağımsız, çevresini algılayabilen yazılım modülleri
- Belirli hedefe yönelik hareket eder
- Otonom karar verebilir
- Duruma göre hareket edebilir
- Öğrenme yeteneği (bazıları için)

---

## Tool Nedir?
- Agentların kullandığı yardımcı araçlar
- Agentların yeteneklerini genişletir
- Belirli bir görevi yerine getiren araçlar
- Statik çalışır, kendi başına düşünmez
- Input → Output şeklinde çalışır
- Karar vermez, sadece iş yapar

---

## Agent vs Tool
| Özellik | Agent | Tool |
|---------|-------|------|
| Bağımsızlık | Otonom | Kontrol edilmeli |
| Amaç | Hedefe ulaşmak için karar alır | Tek görevi yapar |
| Davranış | Çevreye göre değişir | Sabit |
| Zeka | AI destekli | AI yok |

{{% /section %}}

---

{{% section %}}

## n8n
- Açık kaynak workflow otomasyon aracı
- Kod yazmadan sistemler arası entegrasyon
- Low-code / no-code altyapı
- 300+ hazır node
- API entegrasyonları
- Webhook, cron, event tetikleyiciler

{{% /section %}}

---

{{% section %}}

## Agent + n8n
- n8n yapısal iş akışı sağlar
- Agentlar karar verme yeteneği sağlar
- Birlikte kullanım senaryosu:
  - Müşteri isteği → n8n webhook
  - Agent değerlendirmesi
  - n8n eylem

---

## Örnek Senaryo
E-ticaret müşteri destek otomasyonu:
- n8n: Sipariş verisini alır, trigger tetikler
- Agent: Veriye göre müşteri segmenti belirler
- Şikayet ise, ilgili departmana yönlendirir
- Sonuç: Otomatik, hızlı, hatasız süreç

{{% /section %}}

---

{{% section %}}

## MCP Protokolü
- Model Context Protocol
- LLM'lerin bağlam yönetimi için açık kaynak standart protokol
- LLM'lerin veri ve araçlarla entegrasyonunu standartlaştırır (Claude Desktop, IDE'ler)

---

### Swagger Benzerliği

![Swagger UI](/images/general/swagger.png)

---

## Temel Bileşenler
- Resources: Veri ve içerik sağlama
- Prompts: Prompt şablonları
- Tools: İşlem yapabilme
- Sampling: Tamamlamalar talep etme
- Transports: İletişim mekanizmaları

{{% /section %}}

---

## MCP + n8n
- n8n üzerinden MCP sunucularına bağlantı
- LLM entegrasyonlarının otomatizasyonu
- Veri kaynaklarına güvenli erişim
- Prompt iş akışlarının otomatikleştirilmesi
- Araç entegrasyonlarının yönetimi

---

# Demo

---

{{% section %}}

## Dinlediğiniz için teşekkürler

Kaynaklar: [MCP Protocol](https://modelcontextprotocol.io/introduction)

{{% /section %}}
