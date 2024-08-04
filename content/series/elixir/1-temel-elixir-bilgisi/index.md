---
title: 1 - Elixir nedir? Nasıl Kurulur ve Kullanılır
date: 2024-07-30T23:42:06+03:00
description: Bu yazımızda Elixir dilinin temellerine, kurulumuna ve temel kullanımına değineceğiz.
summary: Bu yazımızda Elixir dilinin temellerine, kurulumuna ve temel kullanımına değineceğiz.
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Hamza Ağar
authorEmoji: 🤖
tags:
  - elixir
  - erlang
categories:
  - elixir-serisi
cascade:
  showEdit: false
  showSummary: true
---

## Elixir Nedir?

Elixir, fonksiyonel, eş zamanlı (concurrent) ve dağıtık programlama (distributed programming) için tasarlanmış, dinamik ve güçlü bir programlama dilidir. Elixir, özellikle yüksek performanslı, ölçeklenebilir (scalable) ve hata toleranslı (fault tolerance) sistemler geliştirmek için idealdir.[^1] [^2]

Elixir, Erlang sanal makinesi (BEAM) üzerinde çalışır ve bu sayede güçlü concurrency (eşzamanlılık) özelliklerine sahiptir. Erlang (Ericsson Language), 1980'lerde Ericsson tarafından telekomünikasyon sistemleri için geliştirildi ve BEAM sanal makinesi, bu yüksek talepli sistemlerin gereksinimlerini karşılamak için optimize edildi.

## Erlang ve Elixir HelloWorld Örnekleri

### Erlang
{{< highlight erlang >}}
-module(helloworld).
-export([say_hello/0]).

say_hello() ->
    io:format("Hello, World!~n").
{{< /highlight >}}

### Elixir
{{< highlight elixir >}}
defmodule HelloWorld do
  def say_hello do
    IO.puts("Hello, World!")
  end
end

HelloWorld.say_hello()
{{< /highlight >}}

{{< alert >}}
**Not**: Elixir, aslında HelloWorld örneğinde olduğu gibi daha uzun değil, aksine daha kısa yazılabiliyor ve okunabilirlik konusunda da daha iyi.
{{< /alert >}}


## Temel Özellikler

- **Fonksiyonel Programlama**: Elixir, fonksiyonel programlamayı destekler ve immutable (değişemeyen) veri yapıları ile çalışır. Bu, daha güvenli ve öngörülebilir kod yazmanızı sağlar. Örneğin aşağıda map, filter gibi fonksiyonlar zincir şeklinde birbirini pipe(|) işareti ile çağırıyolar ve her biri çıktısını bir sonraki fonksiyona girdi olarak veriyor:

{{< highlight elixir >}}
defmodule MyList do
  def process_list(list) do
    list
    |> Enum.map(&(&1 + 1))
    |> Enum.filter(&rem(&1, 2) == 0)
    |> Enum.map(&(&1 * &1))
    |> Enum.sum()
  end
end


# Kullanım
list = [1, 2, 3, 4, 5]
result = MyList.process_list(list)
IO.puts("Sonuç: #{result}")
{{< /highlight >}}

- **Eş Zamanlı (Concurrent) ve Dağıtık Sistemler**: Elixir, aynı anda birçok işlemi (process) verimli bir şekilde yürütebilir ve dağıtık sistemlerde mükemmel performans sergiler. Erlang VM (BEAM) üzerine inşa edildiği için bu özellikleri doğal olarak sunar.
- **Erlang VM (BEAM)**: Elixir, Erlang sanal makinesi (BEAM) üzerinde çalışır ve bu sayede Erlang’ın sağlam ve hata toleransı özelliklerinden yararlanır. BEAM, hafif süreçleri (process) ve mesaj geçişini (message passing) destekleyen bir yapı sunar. Bu süreçler, işletim sistemi iş parçacıklarından çok daha hafif olup, binlerce hatta milyonlarca sürecin aynı anda çalıştırılmasını mümkün kılar. Erlang Scheduler, bu hafif süreçleri etkin bir şekilde yönetir ve her bir CPU çekirdeği için bir scheduler thread çalıştırır. Scheduler, süreçlerin adil bir şekilde çalıştırılmasını sağlar ve yüksek verimli bir yük dengeleme mekanizması sunar. Bu özellikler sayesinde, Elixir ile yazılan uygulamalar yüksek eşzamanlılık ve düşük gecikme süreleriyle mükemmel performans sergiler.
![BEAM Processes](beam.png "Photo by [How to build fault-tolerant software systems](https://blog.mi.hdm-stuttgart.de/index.php/2019/10/13/how-to-build-fault-tolerant-software-systems/)")
- **Üretkenlik ve Bakım Kolaylığı**: Modern dil özellikleri ve zengin standart kütüphaneleri ile Elixir, geliştiricilerin üretkenliğini artırır ve kodun bakımını kolaylaştırır.
- **Hata Toleransı**: Elixir, hata yönetimi konusunda güçlüdür ve sistemlerin kesintisiz çalışmasını sağlamak için **“let it crash”**[^3] felsefesini benimser bu da sistemlerin hata durumlarında hızlı bir şekilde toparlanmasını sağlar. [^4]
[^3]: [Let It Crash](https://wiki.c2.com/?LetItCrash)
[^4]: [Erlang “Let it Crash” Approach to Building Reliable Services](https://medium.com/@vamsimokari/erlang-let-it-crash-philosophy-53486d2a6da)
- **Ölçeklenebilirlik (Scalability)**: Elixir, yüksek ölçeklenebilirlik sunar ve aynı anda milyonlarca işlemi yönetebilir.
- **Güvenilirlik (Reliability)**: Elixir, sağlam yapısı ve hata toleransı ile güvenilir sistemler geliştirmeyi sağlar.
- **Dağıtık Sistemler (Distribution)**: Elixir, dağıtık sistemlerde mükemmel performans sergiler ve kolayca ölçeklendirilebilir.
- **Hızlı Yanıt Verme (Responsiveness)**: Elixir, kullanıcılarınıza anında yanıt verebilen hızlı ve verimli sistemler oluşturmanıza imkan tanır.
- **Canlı Güncellemeler (Live Update)**: Elixir, uygulamalarınızı kesinti olmadan güncelleyebilmenizi (deployment) sağlar.
- **Yüksek Erişilebilirlik (High Availability)**: Elixir, yüksek erişilebilirlik gerektiren uygulamalarda mükemmel performans sunar.
- **OTP ve GenServer**: Elixir, yüksek performanslı, dağıtık ve hata toleranslı uygulamalar geliştirmek için kullanılan OTP (Open Telecom Platform) adlı bir kütüphane ve araç seti ile birlikte gelir. OTP'nin temel yapı taşlarından biri olan GenServer, süreçlerin yaşam döngüsünü ve mesajlaşmasını yönetir. GenServer, belirli işlevleri gerçekleştirmek ve durum bilgisi tutmak için kullanılır, bu da karmaşık iş mantıklarının kolayca yönetilmesini sağlar.
- **Hex Paket Yöneticisi ve Mix**: Hex, Elixir ve Erlang projeleri için kullanılan bir paket yöneticisidir. Hex, bağımlılıkları yönetmeyi, paylaşmayı ve Elixir kütüphanelerini kolayca yüklemeyi sağlar. Mix ise Elixir projelerini oluşturmak, derlemek, test etmek ve yönetmek için kullanılan güçlü bir araçtır. Mix, bağımlılık yönetimi, uygulama yapılandırması ve görev otomasyonu gibi işlevleri sağlar.
- **Makrolar**: Makrolar, Elixir'de kodunuzu derleme zamanında dönüştürmenizi ve genişletmenizi sağlayan güçlü araçlardır. Makrolar, kodunuzu daha dinamik ve esnek hale getirmenizi sağlar. Elixir'de makrolar <mark>defmacro</mark> anahtar kelimesi ile tanımlanır. Örneğin aşağıdaki örnekte[^5] Ecto kütüphanesiyle .NET'teki LINQ yapısına benzer bir sorgulama makrolar sayesinde yapılabilmiş.

{{< highlight elixir >}}
# Imports only from/2 of Ecto.Query
import Ecto.Query, only: [from: 2]

# Create a query
query = from u in "users",
          where: u.age > 18,
          select: u.name

# Send the query to the repository
Repo.all(query)
{{< /highlight >}}

[^5]: [Ecto.Query](https://hexdocs.pm/ecto/Ecto.Query.html)

## Kullanım Alanları

Erlang, özellikle telekomünikasyon sektöründe yüksek erişilebilirlik ve güvenilirlik gerektiren sistemlerde uzun yıllardır kullanılmaktadır. Ericsson, WhatsApp, Facebook ve RabbitMQ gibi büyük şirketler, yüksek performanslı ve dağıtık sistemlerini yönetmek için Erlang kullanmaktadır.[^6] Ayrıca Elixir'i de PEPSICO, Discord, Change.org, Heroku gibi firmalar kullanmaktadır.[^7] Elixir de Erlang temelli olduğundan çeşitli alanlarda kullanılabilir.
[^6]: [Who uses Erlang for product development?](https://www.erlang.org/faq/introduction#:~:text=1.5%C2%A0%20Who%20uses%20Erlang%20for%20product%20development%3F)
[^7]: [Companies using Elixir in production](https://elixir-lang.org/cases.html)

Örneğin:

- **Web Geliştirme**: Phoenix framework ile birlikte kullanılarak yüksek performanslı web uygulamaları geliştirilebilir.
- **Dağıtık Sistemler**: Yüksek erişilebilirlik ve düşük gecikme süreleri gerektiren sistemlerde idealdir.
- **Gerçek Zamanlı Uygulamalar**: Anlık mesajlaşma, oyun sunucuları ve IoT uygulamaları gibi gerçek zamanlı sistemlerde kullanılır.

Elixir, Erlang'ın güçlü yönlerini modern bir sözdizimi ve geliştirme deneyimi ile birleştirerek geliştiricilere sunar. Bu nedenle, Elixir telekomünikasyon, finans, sağlık ve e-ticaret gibi sektörlerde yüksek ölçeklenebilirlik ve düşük gecikme süreleri gerektiren uygulamalar için ideal bir seçimdir.

## Elixir Kurulum Rehberi

Elixir programlama dilini bilgisayarınıza kurmak için aşağıdaki adımları takip edebilirsiniz. İşletim sisteminize göre farklı kurulum yöntemleri mevcuttur.

### MacOS Üzerine Elixir Kurulumu

1. **Homebrew Paket Yöneticisini Kurun** (Eğer Homebrew yüklü değilse):

{{< highlight bash >}}
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
{{< /highlight >}}


2. **Elixir'i Homebrew ile Kurun**:

{{< highlight bash >}}
brew install elixir
{{< /highlight >}}

### Ubuntu/Linux Üzerine Elixir Kurulumu

1. **Paket Yöneticisini Güncelleyin**:

{{< highlight bash >}}
sudo apt-get update
{{< /highlight >}}

2. **Elixir'i Kurun**:

{{< highlight bash >}}
sudo apt-get install erlang elixir
{{< /highlight >}}

### Windows Üzerine Elixir Kurulumu

1. **Erlang/OTP'yi İndirin ve Kurun**:

   - [Erlang/OTP İndir](https://erlang.org/downloads)

2. **Elixir'i İndirin ve Kurun**:

   - [Elixir İndir](https://elixir-lang.org/install.html#windows)

{{< alert >}}
**Not**: Ayrıca Windows'ta Elixir'i winget, choco gibi paket yöneticileriyle de kolay bir şekilde kurabilirsiniz.
{{< /alert >}}

### Kurulum Sonrası Kontroller

Elixir'in doğru bir şekilde kurulduğunu doğrulamak için terminal veya komut istemcisinde `elixir -v` komutunu çalıştırabilirsiniz. Bu komut Elixir'in kurulu olduğunu ve sürüm numarasını gösterecektir.

{{< highlight bash >}}
elixir -v
{{< /highlight >}}

Çıktısı:

```
Erlang/OTP 24 [erts-12.2.1] [source] [64-bit] [smp:20:20] [ds:20:20:10] [async-threads:1] [jit]

Elixir 1.12.2 (compiled with Erlang/OTP 24)
```

Şimdi kurulumu başarılı bir şekilde yaptığımıza göre interaktif terminalini tanıyalım ve temel bilgileri öğrenmeye başlayalım.

## IEx Nedir ve Nasıl Kullanılır?

IEx (Interactive Elixir), Elixir kodlarını interaktif olarak çalıştırabileceğiniz bir kabuktur(shell). IEx, Elixir dilini öğrenmek ve hızlı bir şekilde kod denemeleri yapmak için ideal bir araçtır.

### IEx'in Temel Özellikleri

- **Interaktif Çalışma Ortamı**: Elixir kodlarını doğrudan yazıp çalıştırabilirsiniz.
- **Anında Geri Bildirim**: Yazdığınız kodun çıktısını hemen görebilirsiniz.
- **Gelişmiş Yardım Sistemi**: Elixir modülleri ve fonksiyonları hakkında anında yardım alabilirsiniz.
- **Gelişmiş Debugging ve Profiling**: Kodunuzu adım adım çalıştırabilir ve performans analizleri yapabilirsiniz.

### IEx Nasıl Kullanılır?

#### IEx'i Başlatma

IEx’i başlatmak için terminal veya komut istemcisinde `iex` komutunu yazmanız yeterlidir:

{{< highlight bash >}}
iex
{{< /highlight >}}

Sizi şöyle bir ekran karşılayacaktır:

```
Erlang/OTP 24 [erts-12.2.1] [source] [64-bit] [smp:20:20] [ds:20:20:10] [async-threads:1] [jit]

Interactive Elixir (1.12.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```

#### Örneğin bir toplama işlemi yapalım ve sonucunu alalım.

{{< highlight elixir >}}
Erlang/OTP 24 [erts-12.2.1] [source] [64-bit] [smp:20:20] [ds:20:20:10] [async-threads:1] [jit]

Interactive Elixir (1.12.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> 1+1
2
iex(2)>
{{< /highlight >}}

#### Yardım Alma

IEx, Elixir modülleri ve fonksiyonları hakkında yardım almanızı sağlar. Yardım almak için h komutunu kullanabilirsiniz. Örneğin IO.puts fonksiyonu hakkında bilgi alalım:

{{< highlight elixir >}}
iex(2)> h IO.puts

                        def puts(device \\ :stdio, item)

  @spec puts(device(), chardata() | String.Chars.t()) :: :ok

Writes item to the given device, similar to write/2, but adds a newline at the
end.

By default, the device is the standard output. It returns :ok if it succeeds.

## Examples

    IO.puts("Hello World!")
    #=> Hello World!

    IO.puts(:stderr, "error")
    #=> error

iex(3)>
{{< /highlight >}}


#### IEx'den Çıkma

IEx kabuğundan çıkmak için aşağıdaki yöntemleri kullanabilirsiniz:

- **<kbd>CTRL</kbd>+<kbd>C</kbd> Tuş Kombinasyonu:** İki kez <kbd>CTRL</kbd>+<kbd>C</kbd> tuş kombinasyonunu uygulayın.

- **System.halt/0 Fonksiyonu**: System.halt() fonksiyonunu çalıştırın.

{{< highlight elixir >}}
iex> System.halt()
{{< /highlight >}}

{{< alert >}}
**Not**: **'/0'** bu fonksiyonun parametresiz halini kullanabileceğimizi göstermektedir. Parametre sayısına göre slash işaretinin yanındaki sayı değişebilir.
{{< /alert >}}

Daha fazla özelliğe farklı bölümlerde ayrıca değineceğiz şimdilik temeller için bunları bilmek yeterli olacaktır.

[^1]: [Elixir in Action Second Edition](https://www.manning.com/books/elixir-in-action-second-edition) by [Saša Jurić](https://www.linkedin.com/in/sasajuric)
[^2]: [ChatGPT](https://chatgpt.com/)