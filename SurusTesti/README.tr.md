# NSW Sürüş Testi

Transport for NSW'nin resmî 48 sayfalık **A Guide to the Driving Test** kitabı, Türkçe ve animasyonlu tek sayfa hâline getirildi. 32 ders, her biri kendi SVG sahnesi ve sesli anlatımıyla — üstelik anlatım **sayfanın içine gömülü**, yani cihazda Türkçe ses paketi kurulu olmasa bile konuşuyor.

🇬🇧 English version: [README.md](README.md)

---

> ### 🚀 Canlı deneyin
>
> **Adres:** [https://surus.furkantekkartal.com](https://surus.furkantekkartal.com)
>
> Giriş yok, hesap yok, kurulum yok. Tamamı tek bir HTML dosyası — kaydedip internetsiz de açabilirsiniz.

---

## Neden var

Resmî kılavuz 48 sayfa İngilizce düz metin. Anlattığı şeylerin çoğu **mekânsal**: nereye bakacaksın, kaç metrede duracaksın, kafanı ne tarafa çevireceksin. Düz metin bunun için yanlış araç. Bu sayfa her kuralı küçük bir animasyona çeviriyor ve Türkçe sesli anlatıyor.

Bir de kitabın hiç cevaplamadığı soruyu cevaplıyor: *"Bu 19 maddeden hangisinde zayıfım, önce neye çalışmalıyım?"*

## Özellikler

- **32 animasyonlu ders** — her kural küçük bir SVG sahnesi: araç sürünüyor, kafa kör noktayı kontrol ediyor, sinyal yanıp sönüyor, mesafe kapanıyor. 8 bölüme ayrılmış, klavyeyle gezilebiliyor (`←` `→`, `Boşluk` sesli anlatım).
- **İnternetsiz çalışan anlatım** — 22 dakikalık Türkçe ses sayfanın içine base64 olarak gömülü. Cihazda Türkçe ses *varsa* tarayıcınınki kullanılıyor; yoksa gömülü kayıt devreye giriyor. Çalışma anında hiçbir şey indirilmiyor.
- **19 fail item** — puanın kaç olursa olsun testi bitiren ikili kurallar, her biri onu tetikleyen somut davranışla birlikte.
- **Testin iptal edilmesi** — sürüşle ilgisi olmayan, test *başlamadan* bitiren kontroller (araç uygun değil, evrak eksik). Ücret iade edilmiyor.
- **Skor kağıdı okuyucu** — Class C kağıdı (Form 1408) bir harf ızgarası. Harfe dokunun, memurun onu daire içine alarak ne demek istediğini öğrenin.
- **P1 / P2 kısıtlamaları tablosu** — geçtikten sonra neyin değiştiği, yan yana.
- **Sınav sabahı kontrol listesi** — tarayıcıda saklanıyor, bir gece önceden işaretleyebilirsiniz.
- **15 soruluk sınav** — sorular kitaptaki gerçek sayılardan; yanlış cevapta doğrusu hemen açıklanıyor.
- **Açık ve koyu tema** — kırmızı, sarı ve yeşil bu sayfada **rezerve**: yolda ne anlama geliyorsa burada da o anlama geliyor. Vurgu rengi bu yüzden Avustralya bilgi levhası mavisi.

## Teknik

| Katman | Teknoloji |
|---|---|
| Sayfa | Tek statik HTML dosyası — framework yok, derleme adımı yok |
| Grafik | Elle yazılmış satır içi SVG + CSS keyframe animasyonu |
| Anlatım | espeak-ng (Türkçe), base64 MP3 olarak gömülü; cihazda ses varsa Web Speech API |
| Servis | Docker içinde nginx:alpine, FTcom nginx ağ geçidinin arkasında |
| Dağıtım | Docker Compose, yalnızca production |

## Ekranlar

### Kapak
![Kapak](images/01-cover.png)

### Ders oynatıcı
Her ders bir animasyonlu sahneyi kuralın kendisiyle, önemli ölçülerle ve — varsa — karşılık geldiği fail item'la birlikte gösteriyor.
![Ders oynatıcı](images/02-lessons.png)

### 19 fail item
![Fail item](images/03-fail-items.png)

### Skor kağıdı okuyucu
![Skor kağıdı](images/04-score-sheet.png)

### P1 / P2 kısıtlamaları
![P kısıtlamaları](images/05-p-plates.png)

### 15 soruluk sınav
![Sınav](images/06-quiz.png)

### Mobil
<img src="images/07-mobile.png" width="320" alt="Mobil görünüm">

---

## Notlar

Bu sayfa resmî kılavuzun Türkçe özetidir, **resmî bir belge değildir**. Kural değişikliklerinde [nsw.gov.au](https://www.nsw.gov.au) ve Road User Handbook geçerlidir.

Kaynak: *Transport for NSW — A Guide to the Driving Test* (Pub. 07.047, 05/2026) ve Class C skor kağıdı (Form 1408, 02/2026).
