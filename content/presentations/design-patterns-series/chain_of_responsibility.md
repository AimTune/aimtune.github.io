
+++
title = "Chain of Responsibility"
summary = "Bu sunumda, Chain of Responsibility tasarım deseni ile isteklerin nasıl işleyiciler arasında dolaştırılarak işlendiğini inceleyeceğiz."
date = 2024-10-07T22:53:10+03:00
topics = ["Design Patterns", "Chain of Responsibility", "Software Design", "Handlers", "OOP"]
layout = "list"
outputs = ["Reveal"]
[reveal_hugo]
theme = "night"
margin = 0.2
+++

{{% section %}}

## Chain of Responsibility Nedir?
<br>
<img src="/images/slides/design-patterns/chain-of-responsibility.png" height="300" style="border: none;background-color: transparent;"/>

##### Photo by [Refactoring Guru](https://refactoring.guru/design-patterns/chain-of-responsibility)
---

{{< slide template="hamzadark1" >}}

## Chain of Responsibility'nin Tanımı
Chain of Responsibility, bir isteğin, bir zincir şeklinde düzenlenmiş işleyiciler arasında dolaştırılarak işlenmesini sağlar. Her işleyici isteği işleyebilir veya bir sonraki işleyiciye iletebilir.

{{% /section %}}

---

{{% section %}}

## Chain of Responsibility'nin Temel Bileşenleri
- **Handler (İşleyici)**: İsteği işleyen veya bir sonraki işleyiciye gönderen temel bileşen.
- **Concrete Handler**: İsteği belirli kriterlere göre işleyen işleyici sınıfları.
- **Client**: İsteği gönderen bileşen.

---

{{< slide template="hamzadark1" >}}

## Chain of Responsibility Nasıl Çalışır?
1. **İstek Gönderme**: Müşteri isteği bir işleyiciye iletir.
2. **İşleme Kontrolü**: İşleyici isteği işleyip işlemeyeceğine karar verir.
3. **Zincirleme İşleyiciler**: İşleyici isteği işleyemiyorsa bir sonraki işleyiciye iletir.
4. **Sonuç**: İstek işlenir veya tüm zincir dolaşır.

{{% /section %}}

---

{{% section %}}

## Chain of Responsibility Örnek Kod (C#)

{{< highlight csharp >}}
public abstract class Handler
{
    protected Handler next;

    public void SetNext(Handler nextHandler)
    {
        this.next = nextHandler;
    }

    public abstract void HandleRequest(string request);
}
{{< /highlight >}}

---

{{< highlight csharp >}}
public class ConcreteHandlerA : Handler
{
    public override void HandleRequest(string request)
    {
        if (request == "A")
        {
            Console.WriteLine("Handler A is processing the request.");
        }
        else if (next != null)
        {
            next.HandleRequest(request);
        }
    }
}
{{< /highlight >}}

---

{{< highlight csharp >}}
public class ConcreteHandlerB : Handler
{
    public override void HandleRequest(string request)
    {
        if (request == "B")
        {
            Console.WriteLine("Handler B is processing the request.");
        }
        else if (next != null)
        {
            next.HandleRequest(request);
        }
    }
}
{{< /highlight >}}

---

{{< highlight csharp >}}
// Kullanım:
var handlerA = new ConcreteHandlerA();
var handlerB = new ConcreteHandlerB();
handlerA.SetNext(handlerB);

handlerA.HandleRequest("B");
{{< /highlight >}}
{{% /section %}}

---

{{% section %}}

## Chain of Responsibility'nin Avantajları
- **Gevşek Bağlılık**: İsteği gönderen, hangi işleyicinin sorumlu olduğunu bilmek zorunda değildir.
- **Genişletilebilirlik**: Yeni işleyiciler eklenebilir ve zincir kolayca yapılandırılabilir.
- **Sorumluluk Dağılımı**: Yük birden fazla işleyici arasında dağıtılabilir.

---

{{< slide template="hamzadark2" >}}

## Chain of Responsibility'nin Dezavantajları
- **Zincir Karmaşıklığı**: Uzun zincirlerde isteğin işlenme süresi uzayabilir.
- **İşlenmeyen İstekler**: Hiçbir işleyici isteği işleyemezse, sorun çözülmemiş olabilir.

{{% /section %}}

---

{{% section %}}

## Chain of Responsibility Kullanım Alanları
- **Alışveriş Siteleri İş Kuralları**: Alışveriş sitelerinde sepet gibi iş kollarında iş kuralları çok fazla olabilir. Bunu daha okunabilir ve bakımı kolay hale getirmek için bu desen kullanılabilir.
- **Destek Hizmetleri**: Müşteri şikayetlerinin kademeli olarak çözülmesi.
- **İzin Sistemleri**: Bir izin talebinin farklı seviyelerde işlenmesi.
- **Oyun Geliştirme**: Oyunlarda olayların farklı karakterler veya mekanlar tarafından işlenmesi.

---

{{< slide template="hamzadark1" >}}

## Sonuç
- Chain of Responsibility, esnek ve genişletilebilir bir çözüm sunar.
- İş akışı kolayca yönetilebilir, ancak zincirin iyi yapılandırılması gerekir.

{{% /section %}}

---

{{< slide template="hamzadark2" >}}

# Demo

<img src="/images/slides/design-patterns/ted-scherbatsky.gif" height="300" style="border: none;background-color: transparent;"/>

---
{{% section %}}

## Dinlediğiniz için teşekkürler

Kaynaklar: [Refactoring Guru](https://refactoring.guru/design-patterns/chain-of-responsibility)

Örnekler Reposu: [aimtune/design-patterns-examples](https://github.com/AimTune/design-patterns-examples)

{{% /section %}}
