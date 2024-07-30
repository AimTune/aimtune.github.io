---
title: 1 - Elixir nedir? Nasıl Kurulur ve Kullanılır
date: 2024-07-30T23:42:06+03:00
description: Bu yazımızda Elixir dilinin temellerine, kurulumuna ve temel kullanımına değineceğiz.
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
series:
  - Elixir
image: images/posts/elixir.png
---

# Elixir Nedir?

Elixir, fonksiyonel, eş zamanlı (concurrent) ve dağıtık programlama (distributed programming) için tasarlanmış, dinamik ve güçlü bir programlama dilidir. Elixir, özellikle yüksek performanslı ve hata toleranslı (fault tolerance) sistemler geliştirmek için idealdir.

## Temel Özellikler

- **Fonksiyonel Programlama**: Elixir, fonksiyonel programlamayı destekler ve immutable veri yapıları ile çalışır. Bu, daha güvenli ve öngörülebilir kod yazmanızı sağlar.
- **Eş Zamanlı (Concurrent) ve Dağıtık Sistemler**: Elixir, aynı anda birçok işlemi (process) verimli bir şekilde yürütebilir ve dağıtık sistemlerde mükemmel performans sergiler. Erlang VM (BEAM) üzerine inşa edildiği için bu özellikleri doğal olarak sunar.
- **Erlang VM (BEAM)**: Elixir, Erlang sanal makinesi (BEAM) üzerinde çalışır ve bu sayede Erlang’ın sağlam ve hata toleranslı özelliklerinden yararlanır.
- **Hata Toleransı**: Elixir, hata yönetimi konusunda güçlüdür ve sistemlerin kesintisiz çalışmasını sağlamak için **“let it crash”** felsefesini benimser. **[1] [2]**
- **Üretkenlik ve Bakım Kolaylığı**: Modern dil özellikleri ve zengin standart kütüphaneleri ile Elixir, geliştiricilerin üretkenliğini artırır ve kodun bakımını kolaylaştırır.

## Kullanım Alanları

Elixir, çeşitli alanlarda kullanılabilir:

- **Web Geliştirme**: Phoenix framework ile birlikte kullanılarak yüksek performanslı web uygulamaları geliştirilebilir.
- **Dağıtık Sistemler**: Yüksek erişilebilirlik ve düşük gecikme süreleri gerektiren sistemlerde idealdir.
- **Gerçek Zamanlı Uygulamalar**: Anlık mesajlaşma, oyun sunucuları ve IoT uygulamaları gibi gerçek zamanlı sistemlerde kullanılır.

## Örnek Kod

Aşağıda, basit bir Elixir fonksiyonunun nasıl tanımlanacağını gösteren bir örnek bulunmaktadır:

```elixir
defmodule Merhaba do
  def selam_ver do
    IO.puts "Merhaba, Dünya!"
  end
end

Merhaba.selam_ver()
```

# Elixir Kurulum Rehberi

Elixir programlama dilini bilgisayarınıza kurmak için aşağıdaki adımları takip edebilirsiniz. İşletim sisteminize göre farklı kurulum yöntemleri mevcuttur.

## MacOS Üzerine Elixir Kurulumu

1. **Homebrew Paket Yöneticisini Kurun** (Eğer Homebrew yüklü değilse):

   ```sh
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Elixir'i Homebrew ile Kurun**:

   ```sh
   brew install elixir
   ```

## Ubuntu/Linux Üzerine Elixir Kurulumu

1. **Paket Yöneticisini Güncelleyin**:

   ```sh
   sudo apt-get update
   ```

2. **Elixir'i Kurun**:

   ```sh
   sudo apt-get install erlang elixir
   ```

## Windows Üzerine Elixir Kurulumu

1. **Erlang/OTP'yi İndirin ve Kurun**:

   - [Erlang/OTP İndir](https://erlang.org/downloads)

2. **Elixir'i İndirin ve Kurun**:

   - [Elixir İndir](https://elixir-lang.org/install.html#windows)

**NOT:** Ayrıca Windows'ta Elixir'i winget, choco gibi paket yöneticileriyle de kolay bir şekilde kurabilirsiniz.

## Kurulum Sonrası Kontroller

Elixir'in doğru bir şekilde kurulduğunu doğrulamak için terminal veya komut istemcisinde `elixir -v` komutunu çalıştırabilirsiniz. Bu komut Elixir'in kurulu olduğunu ve sürüm numarasını gösterecektir.

```sh
elixir -v
```

Çıktısı:

```
Erlang/OTP 24 [erts-12.2.1] [source] [64-bit] [smp:20:20] [ds:20:20:10] [async-threads:1] [jit]

Elixir 1.12.2 (compiled with Erlang/OTP 24)
```

Şimdi kurulumu başarılı bir şekilde yaptığımıza göre interaktif terminalini tanıyalım ve temel bilgileri öğrenmeye başlayalım.

# IEx Nedir ve Nasıl Kullanılır?

IEx (Interactive Elixir), Elixir kodlarını interaktif olarak çalıştırabileceğiniz bir kabuktur(shell). IEx, Elixir dilini öğrenmek ve hızlı bir şekilde kod denemeleri yapmak için ideal bir araçtır.

## IEx'in Temel Özellikleri

- **Interaktif Çalışma Ortamı**: Elixir kodlarını doğrudan yazıp çalıştırabilirsiniz.
- **Anında Geri Bildirim**: Yazdığınız kodun çıktısını hemen görebilirsiniz.
- **Gelişmiş Yardım Sistemi**: Elixir modülleri ve fonksiyonları hakkında anında yardım alabilirsiniz.
- **Gelişmiş Debugging ve Profiling**: Kodunuzu adım adım çalıştırabilir ve performans analizleri yapabilirsiniz.

## IEx Nasıl Kullanılır?

### IEx'i Başlatma

IEx’i başlatmak için terminal veya komut istemcisinde `iex` komutunu yazmanız yeterlidir:

```sh
iex
```

Sizi şöyle bir ekran karşılayacaktır:

```
Erlang/OTP 24 [erts-12.2.1] [source] [64-bit] [smp:20:20] [ds:20:20:10] [async-threads:1] [jit]

Interactive Elixir (1.12.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```

#### Örneğin bir toplama işlemi yapalım ve sonucunu alalım.

```
Erlang/OTP 24 [erts-12.2.1] [source] [64-bit] [smp:20:20] [ds:20:20:10] [async-threads:1] [jit]

Interactive Elixir (1.12.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> 1+1
2
iex(2)>
```

#### Yardım Alma

IEx, Elixir modülleri ve fonksiyonları hakkında yardım almanızı sağlar. Yardım almak için h komutunu kullanabilirsiniz. Örneğin IO.puts fonksiyonu hakkında bilgi alalım:

```elixir
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
```

#### IEx'den Çıkma

IEx kabuğundan çıkmak için aşağıdaki yöntemleri kullanabilirsiniz:

- **Ctrl + C Tuş Kombinasyonu:** İki kez Ctrl + C tuşuna basın.

- **System.halt/0 Fonksiyonu:**

```
iex> System.halt()
```

**Not:**
**'/0'** bu fonksiyonun parametresiz halini kullanabileceğimizi göstermektedir. Parametre sayısına göre slash işaretinin yanındaki sayı değişebilir.

Daha fazla özelliğe farklı bölümlerde ayrıca değineceğiz şimdilik temeller için bunları bilmek yeterli olacaktır.

## Kaynaklar

1. [Let It Crash](https://wiki.c2.com/?LetItCrash)
2. [Erlang “Let it Crash” Approach to Building Reliable Services](https://medium.com/@vamsimokari/erlang-let-it-crash-philosophy-53486d2a6da)
