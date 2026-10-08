# Telegram Skills

Özel Telegram asistanım **Kayra**'nın kontrol odası. *Yetenek*, botun bir fotoğraf ya da yazı gönderdiğimde, ya da zamanı gelince kendiliğinden yaptığı tek bir iştir. Bu panel her yeteneği bir kart olarak gösterir (en son ne zaman çalıştı, nasıl gitti, ne sıklıkta çalışıyor) ve her birini açıp kapatmamı sağlar.

🇬🇧 English version: [README.md](README.md)

---

> ### 🔒 Özel
>
> **Adres:** [https://skills.furkantekkartal.com](https://skills.furkantekkartal.com) (şifre korumalı)
>
> Aşağıdaki ekran görüntüleri üretilmiş örnek veriyle alındı, gerçek çalışmalar değil.

---

![Pano](images/01-dashboard.png)

## Neden var

Bot tek işle başladı (fotoğraftan yükleme planlayıcısına kamyon eklemek), on işe çıktı: el yazısı listeleri tabloya işlemek, etiketinden plakayı kullanıldı diye işaretlemek, vardiya kâğıdını okuyup ücret hesaplamak, konum geçmişinden çalışma saati çıkarmak, açıklaması olmayan banka transferinin ne olduğunu sormak ve zamanlı birkaç bildirim. Şimdiye kadar bir yeteneğin hâlâ çalışıp çalışmadığını öğrenmenin ya da birini durdurmanın tek yolu terminalden sormaktı. Bu sayfa cevabı tek ekranda veriyor.

## Özellikler

- **Yetenek başına bir kart** — tür (fotoğraf, yazı, zamanlı, otomatik), son çalışma ve sonucu, son 7 gündeki çalışma sayısı, ortalama süre ve 14 günlük çubuk şeridi
- **Aç / kapat anahtarı** — kapalı yetenek "This skill is turned off in the panel." diye cevap verir ve hiçbir şey yapmaz; zamanlı yetenekler sırasını atlar
- **Şimdi çalıştır** — zamanlı yetenekler karttan tetiklenebilir
- **Canlı akış** — her çalışma olduğu anda: zaman, yetenek, tetikleyici, sonuç, süre ve tek satır özet. 10 saniyede bir yenilenir
- **Seçili yetenek** — nerede çalıştığı, hangi modelin okuduğu, nasıl tetiklendiği, son hata ve son beş çalışma
- **Botun nabzı** — üst bar botun yoklama yapıp yapmadığını ve en son ne zaman yaptığını gösterir

![Seçili yetenek](images/02-selected-skill.png)

## Nasıl çalışır

Panel hiçbir komut çalıştırmaz. Botun yazdığı üç dosyayı okur, botun okuduğu iki küçük dosyayı yazar:

| Dosya | Kim yazar | Kim okur | Ne |
|---|---|---|---|
| `runs.jsonl` | bot ve araçları | panel | çalışma olayları: ilerleme kartının başı, etiketi ve sonu, ya da tek satırlık çalışma |
| `heartbeat.json` | bot, her yoklama turunda | panel | 90 saniye sessizlik "bot yanıt vermiyor" demektir |
| `telegram.log` | bot | panel | gönderilen mesaj sayısı |
| `skills.json` | **panel** | bot ve araçları | hangi yetenekler açık; dosya yoksa hepsi açık |
| `queue/*.json` | **panel** | sunucudaki küçük bir çalıştırıcı | "şimdi çalıştır" istekleri; komut sunucudaki izinli listeden gelir |

Bot her iş için Telegram'da zaten canlı bir ilerleme kartı gösterdiğinden çalışma kaydı o karta bağlanır: kartın açılması çalışmanın başı, son hâli sonudur. İzlenebilsin diye hiçbir yeteneği yeniden yazmak gerekmedi.

## Tasarım

Görsel tasarımı **Google Stitch** üretti ("Kayra Control Plane" tasarım sistemi: koyu arduvaz yüzeyler, zümrüt vurgu, ince çizgiler, Plus Jakarta Sans ile JetBrains Mono). Ön yüz o tasarım sistemini uygular; Stitch'in çizdiği örnek sayıların yerinde gerçek veri durur.

![Telefon](images/03-mobile.png)

## Teknoloji

| Katman | Teknoloji |
|---|---|
| Sunucu | Yalnız Python standart kütüphanesi (`http.server`), scrypt şifre özeti, imzalı oturum çerezi |
| Ön yüz | Düz HTML, CSS ve tek bir JavaScript modülü; çatı yok, derleme adımı yok |
| Yazı tipi ve simgeler | Yerelde barındırılan Plus Jakarta Sans, JetBrains Mono ve Material Symbols alt kümesi |
| Güvenlik | Sıkı Content-Security-Policy (satır içi betik ya da stil yok, üçüncü taraf isteği yok), salt okunur konteyner |
| Sunum | FTcom nginx ağ geçidinin arkasında tek Docker konteyneri |
| Kurulum | Docker Compose, yalnız prod |

![Giriş](images/04-login.png)
