# Wardrobe

Yapay zekâ destekli dijital gardırop. Kıyafetlerinizi fotoğraflayın → AI arka planı silsin, parçayı **görünmez manken (ghost mannequin)** üzerinde yeniden çizsin ve otomatik etiketlesin → sürükle-bırak tuvalinde kombin kurun → sanal manken (ya da kendi fotoğrafınız) üzerinde deneyin → tek cümleyle kombin önerisi isteyin.

🇬🇧 English version: [README.md](README.md)

---

> ### 🚀 Canlı deneyin
>
> **URL:** [https://wardrobe.furkantekkartal.com](https://wardrobe.furkantekkartal.com)
>
> **Demo giriş:** kullanıcı adı `demo` · şifre `demo1234`
>
> **Not:** kayıt **yalnızca davetiyelidir**. Yeni bir hesap için uygulama sahibinden davet kodu gerekir; bu yüzden uygulamayı keşfetmek için lütfen demo hesabını kullanın.

---

## Özellikler

- **Ghost mannequin görselleri** — her kıyafet için AI'ın ürettiği, "kimsenin üzerinde olmayan" bir versiyon: parça orijinal fotoğraftan kesilir ve katalog ürünü gibi hacimli biçimde yeniden çizilir. Orijinal fotoğraf hiçbir zaman atılmaz, tek dokunuşla geri gelir.
- **AI otomatik etiketleme (Claude)** — tek fotoğraf yeter: AI kıyafeti adlandırır, kategori ve alt kategoriyi seçer, ana ve yardımcı renkleri bulur, stil etiketlerini üretir.
- **HEIC destekli toplu ekleme** — yüzlerce fotoğrafı bir seferde bırakabilirsiniz. iPhone `.HEIC` dosyaları **tarayıcıda** JPEG'e çevrilip küçültülür; hepsi taslak alanına düşer ve siz onaylamadan gardıroba girmez.
- **Sürükle-bırak kombin tuvali** — kesilmiş parçalar birer sticker gibi davranır: tek parmakla taşıyın, iki parmakla ölçekleyin, katmanları sıralayın.
- **Üç farklı zeminde sanal deneme** — görünmez **ghost** manken, **sanal manken** (kadın/erkek) ya da **kendi fotoğrafınız**.
- **Kombin ⇄ deneme bağlantısı** — bir kombin doğrudan deneme kabinine gönderilir, üretilen görsel de aynı kombine geri işlenir. Hangisinin ana görsel olacağına siz karar verirsiniz: tuval mi, manken mi.
- **Doğal dilde kombin önerisi** — tek cümle yazın ("Hafta sonu kahveye çıkıyorum…"), Claude gerçekten sahip olduğunuz kıyafetlerden gerekçeli kombinler kursun; hava durumunu da hesaba katar.
- **Kullanıcı bazlı AI kredisi** — her AI çağrısının gerçek bir dolar maliyeti vardır; kullanıcının bakiyesinden düşülür ve aylık tavan uygulanır.
- **Davetiyeli erişim + admin araçları** — admin tek kullanımlık davet kodu üretir ve kullanıcılara kredi yükler.

## Teknoloji

| Katman | Teknoloji |
|---|---|
| Ön yüz | React 19, Vite 7, Tailwind CSS 4, React Router |
| Arka uç | Node.js 20, Express 4, eşzamanlılık sınırlı asenkron AI iş kuyruğu |
| Veritabanı | PostgreSQL (ortak sunucu, ayrı dev/prod veritabanları) |
| Kimlik | JWT, davet kodlu kayıt |
| AI — etiketleme & öneri | Claude Sonnet |
| AI — ghost mannequin & deneme | Gemini görsel modelleri (OpenRouter üzerinden) |
| AI — arka plan silme | PhotoRoom, hata durumunda yerel IMG.LY'ye düşer |
| Hava durumu | OpenWeather |
| Yayın | Nginx ters vekil arkasında Docker Compose |

## Ekranlar

Tüm ekran görüntüleri canlı uygulamadan, mobil görünümde (390 px) alınmıştır — arayüz mobil öncelikli tasarlanmıştır.

## Giriş & Kayıt

<img src="images/01-login.png" alt="Giriş ekranı" width="300"> <img src="images/02-register.png" alt="Kayıt ekranı" width="300">

- Kullanıcı adı **veya** e-posta ile giriş yapılır; oturumlar JWT ile tutulur.
- *Hesap Oluştur* davetiyelidir: ilk alan davet kodudur ve sunucuda anlık doğrulanır. Kodlar tek kullanımlıktır ve yalnızca admin üretebilir — uygulama bu sayede kapalı kalır.

## Ana Sayfa

<img src="images/03-dashboard.png" alt="Ana sayfa" width="390">

- Günün saatine göre selamlama, ardından iki sayı: **68 parça** ve **2 kombin**.
- *Son Eklenenler* en yeni parçaları gösterir — hepsi ghost mannequin görselleriyle.
- *Kombinler* satırında kayıtlı kombin kartları yer alır.
- Yüzen kamera düğmesi her yerden kıyafet ekler; alt barda beş sekme vardır: Ana Sayfa, Gardırop, Kombinlerim, Dene, Profil.

## Gardırop

<img src="images/04-wardrobe.png" alt="Gardırop" width="390">

- Tüm dolap katalog düzeninde listelenir — *"68 / 68 parça"* şu an hepsinin göründüğünü söyler.
- Arama kutusu ve canlı sayaçlı kategori çipleri (*Tümü, Aksesuar, Dış Giyim, Üst…*); filtre çekmecesi etiket ve renk filtreleri ekler.
- Karttaki küçük sepet ikonu parçayı **deneme kabinine** atar; gezinirken biriktirip hepsini tek seferde deneyebilirsiniz.
- Filtreler ve kaydırma konumu sayfalar arasında korunur: bir kıyafeti açıp geri döndüğünüzde tam kaldığınız yerdesiniz.

## Kıyafet Detayı

<img src="images/05-clothing-detail.png" alt="Kıyafet detayı" width="390">

- Kıyafet şeffaf zeminde durur — otomatik arka plan silmenin kanıtı.
- Görselin altındaki geçiş, *Ghost mannequin* (uygulamanın her yerinde kullanılan AI görseli) ile *Orijinal fotoğraf* (çektiğiniz kare) arasında geçiş yapar. **Orijinal her zaman saklıdır.**
- *Görseli yeniden üret*, ilk sonuç beğenilmediğinde ghost üretimini tekrar çalıştırır.
- İsim, kategori ve alt kategori AI'dan gelir ve satır içi düzenlenebilir; altında tespit edilen renkler ve stil etiketleri bulunur.

## Kıyafet Ekleme

<img src="images/06-clothing-add.png" alt="Kıyafet ekle" width="300"> <img src="images/07-bulk-add.png" alt="Toplu ekle" width="300">

- **Tekli ekleme:** fotoğraf çekin ya da galeriden seçin. Yükleme asenkron bir hattı başlatır — sıkıştırma → arka plan silme → ghost mannequin → Claude analizi → etiketler — ve arayüz sunucudaki gerçek aşamaları gösterir.
- **Toplu ekleme:** *"Yüzlerce fotoğraf olabilir. iPhone HEIC dosyaları tarayıcıda otomatik JPEG'e çevrilip küçültülür. Hepsi taslak olarak eklenir; onaylayana kadar gardıropta görünmez."*
- *İncele* sekmesi taslakları ızgarada gösterir. AI beğenmediği kesimleri işaretler; 200 fotoğrafın hepsini değil, yalnızca sorunluları elden geçirirsiniz.
- Üstteki şerit kalan PhotoRoom kotasını takip eder — arka plan silme ücretli bir API'dir.

## Kombin Düzenleyici

<img src="images/09-outfit-builder.png" alt="Kombin tuvali" width="300"> <img src="images/15-outfit-cover-choice.png" alt="Manken denemeli kombin" width="300">

- 3:4'lük tuvalde parçalar sticker gibi davranır: tek parmakla taşıyın, iki parmakla ölçekleyin, katman sırasını değiştirin.
- **Solda:** ana görsel *Tuval*'dir ve *Manken* alanı henüz boştur — *"Henüz denenmedi / Dokun ve dene"*.
- **Sağda:** deneme yapıldıktan sonra iki versiyon yan yana durur ve *"Ana görsel yap"* hangisinin listelerde kombini temsil edeceğine karar verir. Diğeri bu sayfada görünmeye devam eder.
- *Kullanılan Kıyafetler* parçaları hızlı silme düğmeleri ve *Ekle* seçicisiyle listeler.
- Alt barda *Dene* ve *Güncelle* bulunur; *Dene* tam olarak bu kombini deneme kabinine taşır.

<img src="images/16-outfits-covers.png" alt="Kombin listesi" width="390">

*Kombinlerim*'de iki kapak tipi yan yanadır: biri manken fotoğrafını, diğeri tuval kolajını gösterir.

## Sanal Deneme

Üç ayrı zemin — uygulamanın kalbi burasıdır.

### 1. Kabin

<img src="images/10-tryon-cabin.png" alt="Deneme kabini" width="390">

- Başlıkta harcanabilir bakiye ve yaklaşık kaç deneme hakkı kaldığı yazar.
- 1. adım *"Kimin üzerinde denensin?"*: **Ghost** (görünmez manken), **Fotoğrafım**, **Manken** (sanal manken).
- 2. adımda kabindeki parçalar listelenir; *"Tek kombin olarak dene"* hepsini tek çağrıda tek görünüm olarak birleştirir.
- 3. adımda görsel modeli seçilir; çağrı başı fiyatlar ve tahmini maliyet başlamadan önce görünür.

### 2. Ghost sonucu

<img src="images/11-tryon-progress.png" alt="Deneme sürüyor" width="300"> <img src="images/12-tryon-ghost-result.png" alt="Ghost deneme sonucu" width="300">

- İş sunucuda çalışır; *"1 işlem arka planda"* şeridi görünürken uygulamayı kullanmaya devam edebilirsiniz.
- Sonuç: gömlek ve pantolon **kimsenin üzerinde olmadan**, doğru dökümle havada durur. Alttaki film şeridi bütün girdi karelerini ve *Sonuç* karesini saklar.

### 3. Manken sonucu

<img src="images/13-tryon-mannequin-select.png" alt="Manken seçimi" width="300"> <img src="images/14-tryon-mannequin-result.png" alt="Manken deneme sonucu" width="300">

- *Manken* sekmesinde *Kadın* veya *Erkek* manken seçilir ve aynı kombin o beden üzerinde üretilir.
- Bu deneme bir kombinden başlatıldığı için düğme *"Kombine işle"* der: görsel yeni bir kombin açmadan mevcut kombine kaydedilir.
- Üçüncü seçenek olan *Fotoğrafım* ile aynı işlem kendi fotoğrafınız üzerinde yapılır.

## AI Kombin Önericisi

<img src="images/17-ai-input.png" alt="AI öneri girişi" width="300"> <img src="images/18-ai-result.png" alt="AI öneri sonucu" width="300">

- Planınızı tek cümleyle yazın — burada: *"Hafta sonu arkadaşlarımla kahve içmeye çıkıyorum, rahat ama şık bir kombin önerir misin?"*
- Opsiyonel şehir alanı, OpenWeather üzerinden öneriyi hava durumuna duyarlı hale getirir.
- Claude isimlendirilmiş kombinlerle cevap verir — *"Şık Kahve Buluşması Kombini"* — parçaların **neden** uyumlu olduğunu açıklar ve **yalnızca** gardıropta gerçekten bulunan kıyafetleri kullanır.
- *Bu Kombini Kaydet* öneriyi kayıtlı bir kombine çevirir; sonrasında tuvalde düzenleyip deneyebilirsiniz.
- Tüm önerilerin göründüğü tam sayfa görüntü: [18b-ai-result-full.png](images/18b-ai-result-full.png)

## İstatistik, Hareketler ve Profil

<img src="images/19-stats.png" alt="İstatistikler" width="260"> <img src="images/20-activity.png" alt="Hareketler" width="260"> <img src="images/21-profile.png" alt="Profil" width="260">

- **İstatistikler** — toplamlar, kategori bazında çubuklar (*Üst* 36, *Alt* 24, *Dış Giyim* 5…) ve bu ayki AI kullanımı ile gerçek maliyeti.
- **Hareketler** — güne göre gruplanmış zaman çizelgesi: eklenen parçalar, yapılan denemeler, istenen öneriler; her biri lightbox'ta açılan küçük görsellerle.
- **Profil** — kredi panosu: harcanabilir bakiye, hesap bakiyesi, aylık tavan, toplam yüklenen ve harcanan, ayrıca sağlayıcı bazında bu uygulamanın harcaması. Admin hesapları burada ayrıca davet kodu üretir ve kullanıcılara kredi yükler.

## Mimari

- **Mobil öncelikli SPA** — telefon genişliğinde, alt sekme barlı bir React uygulaması; Nginx tarafından servis edilir. Geri dönüldüğünde kaydırma konumu ve filtreler korunur, uzun listeler başa atmaz.
- **REST API + asenkron iş takibi** — Express arka ucu JSON uçları sunar; yavaş AI işleri (etiketleme, ghost mannequin, öneri, deneme) eşzamanlılık sınırlı arka plan işleri olarak çalışır, böylece 200 fotoğraflık bir aktarım makineyi boğmaz. Ön yüz iş bitene kadar durumu yoklar.
- **Her kıyafet için iki görsel** — orijinal fotoğraf ve ghost mannequin çıktısı birlikte saklanır; uygulama ghost halini gösterir ama orijinal her an geri getirilebilir veya yeniden üretilebilir.
- **Ortak PostgreSQL** — tek sunucuda ayrı dev ve prod veritabanları; şema migration'ları arka uç açılışında otomatik çalışır.
- **Kullanıcı bazlı yüklemeler Docker volume'unda** — orijinaller, kesimler ve deneme sonuçları konteyner dışındaki kalıcı diskte, kullanıcı bazında tutulur.
- **AI çağrısı başına kredi muhasebesi** — her sağlayıcı çağrısı dolar cinsinden fiyatlanıp kullanıcı bakiyesinden düşülür; aylık limit ve admin yüklemesi vardır.
- **Nginx arkasında Docker Compose** — ayrı dev ve prod yığınları; ters vekil `wardrobe.furkantekkartal.com` (prod) ve `wardrobe-dev.furkantekkartal.com` (dev) isteklerini doğru konteynere yönlendirir.

---

🇬🇧 English version: [README.md](README.md)

*Bu belge [ProjectReadmes](../) portfolyo derlemesinin parçasıdır.*
