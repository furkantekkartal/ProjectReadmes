# Furkan Tekkartal — Proje Portfolyosu

[furkantekkartal.com](https://furkantekkartal.com) üzerinde çalışan tüm uygulamaların ekran görüntülü, detaylı dokümantasyonu. Her proje sayfası canlı uygulamanın bütün ekranlarını tek tek gezdirir; demo hesaplarla kendiniz de deneyebilirsiniz.

🇬🇧 English version: [README.md](README.md)

---

## Projeler

| Proje | Nedir | Canlı uygulama | Dokümanlar |
|---|---|---|---|
| 🥗 **HealthNHabits** | Yapay zekâlı yemek tarayıcısına sahip sağlık takibi: yemeğin fotoğrafını çek, kalori ve makroları al | [Aç](https://healthnhabits.furkantekkartal.com) | [Türkçe](HealthNHabits/README.tr.md) · [English](HealthNHabits/README.md) |
| 👗 **Wardrobe** | Yapay zekâlı dijital gardırop: ghost mannequin görselleri, otomatik etiketleme, HEIC destekli toplu ekleme, kombin tuvali, ghost/manken/kendi fotoğrafın üzerinde sanal deneme | [Aç](https://wardrobe.furkantekkartal.com) | [Türkçe](Wardrobe/README.tr.md) · [English](Wardrobe/README.md) |
| 🧾 **Receiptly** | Yapay zekâ OCR'lı fiş tarama ve ev bütçesi takibi | [Aç](https://receiptly.furkantekkartal.com) | [Türkçe](Receiptly/README.tr.md) · [English](Receiptly/README.md) |
| 🎯 **HomeMadeKahoot** | Gerçek zamanlı çok oyunculu quizlerle Kahoot tarzı İngilizce öğrenme platformu | [Aç](https://homemadekahoot.furkantekkartal.com) | [Türkçe](HomeMadeKahoot/README.tr.md) · [English](HomeMadeKahoot/README.md) |
| 🔧 **Dükkanım** | Oto tamirhaneleri için yönetim sistemi: araçlar, servis kayıtları, faturalama | [Aç](https://dukkanim.furkantekkartal.com) | [Türkçe](Dukkanim/README.tr.md) · [English](Dukkanim/README.md) |
| 🏺 **Authentic Bazaar** | Sıfır bağımlılıklı vanilla-JS e-ticaret vitrini (demo mağaza) | [Aç](https://authenticbazaar.furkantekkartal.com) | [Türkçe](AuthenticBazaar/README.tr.md) · [English](AuthenticBazaar/README.md) |
| 📊 **Deneme Takip Sistemi** | Deneme sınavı takibi: Excel sonuç dosyaları öğrenci bazlı dashboard ve trend grafiklerine dönüşür (giriş korumalı) | [Aç](http://examvisualizer.furkantekkartal.com) | [Türkçe](ExamVisualizer/README.tr.md) · [English](ExamVisualizer/README.md) |
| 🚗 **NSW Sürüş Testi** | NSW sürücü sınavı kılavuzu: 32 animasyonlu Türkçe ders, sayfaya gömülü sesli anlatım, skor kağıdı okuyucu ve 15 soruluk sınav | [Aç](https://surus.furkantekkartal.com) | [English](SurusTesti/README.md) · [Türkçe](SurusTesti/README.tr.md) |

**Demo hesaplar:** Giriş gerektiren her uygulamada kullanıcı adı `demo`, şifre `demo1234`.

## Bu ekosistem nasıl çalışıyor

Tüm uygulamalar, kendi kiraladığım bulut sunucularda tek bir altyapıyı paylaşır:

- Her proje **Docker container**'ları olarak yayınlanır (dev ve prod ayrı stack'ler).
- Tek bir **Nginx gateway**, `<proje>.furkantekkartal.com` subdomain'lerini doğru container'a yönlendirir (`-dev` subdomain'leri geliştirme sürümünü sunar).
- Paylaşılan bir **PostgreSQL** örneği, uygulama ve ortam başına ayrı veritabanı barındırır.
- Yapay zekâ özellikleri (yemek analizi, OCR, kombin önerisi, sanal deneme, quiz üretimi) OpenRouter, Gemini, Claude ve FASHN API'leri üzerinden çalışır.

---

🇬🇧 English version: [README.md](README.md)

*Tüm ekran görüntüleri, özel demo hesaplarıyla canlı production uygulamalarından alınmıştır.*
