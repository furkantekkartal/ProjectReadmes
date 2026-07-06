# Authentic Bazaar

El yapımı Türk ürünleri için bir demo e-ticaret vitrini — tamamen saf HTML, CSS ve JavaScript ile, framework ve build adımı olmadan geliştirildi.

🇬🇧 [Click here for the English version](README.md)

> **Canlı deneyin:** <https://authenticbazaar.furkantekkartal.com>
>
> Hesap gerekmez — koleksiyonlarda gezinin ve sepeti dilediğiniz gibi doldurun. **Ödeme adımı bir demodur** (gerçek bir ödeme sayfası yerine bir uyarı mesajı gösterir).

Authentic Bazaar bir portfolyo projesidir, gerçek bir mağaza değildir; hiçbir şey satmaz. 22 ürünlük katalog (mozaik lambalar, seramikler, nazar boncukları ve pamuklu peştemaller), Avustralya'daki gerçek bir mağazanın (istanbulgrandbazaar.com.au) ilanlarından derlenmiştir; bu sayede içerik gerçek bir vitrin gibi görünür ve hissettirir.

## Özellikler

- Ana sayfada dönen tanıtım slaytlarıyla **hero slayt gösterisi**
- 4 ürün kategorisi ve ayrıca özel bir İndirim koleksiyonu için **koleksiyon sayfaları**
- **Filtreleme ve sıralama** — renk seçenekleri, fiyat aralıkları, "Sadece İndirimdekiler" kutusu ve sıralama menüsü (öne çıkanlar, fiyat, puan, isim)
- Görsel galerisi, renk varyantları, adet seçici, akordeonlar ve ilgili ürünlerle **ürün detay sayfaları**
- **Hızlı Bakış (Quick View) penceresi** — ürün listesinden ayrılmadan ürünü inceleyin ve sepete ekleyin
- Tarayıcının localStorage'ında saklanan **kalıcı sepet** ve ücretsiz kargo ilerleme göstergesi (A$50 eşiği)
- **Sepete eklendi bildirimi** (toast) ve üst menüde anlık güncellenen sepet sayacı
- Hamburger menülü, **tamamen duyarlı (responsive)** mobil tasarım

## Teknoloji yığını

Bu projenin asıl amacı **bilinçli olarak sıfır bağımlılıkla çalışmaktır**: bir framework'ün normalde sağladığı her şey, saf JavaScript ile elle yazılmıştır.

| Katman | Tercih |
|---|---|
| Frontend | Saf HTML, CSS ve JavaScript — framework yok, kütüphane yok |
| Yönlendirme | Sıfırdan yazılmış, hash tabanlı özel router (`#/collections/...`, `#/products/...`, `#/cart`) |
| Bileşenler | Sayfaya render edilen elle yazılmış JS modülleri (hero slayt, filtre paneli, hızlı bakış, sepet, toast) |
| Durum (state) | Ürün verisi bir JS dosyasında sabit; sepet durumu `localStorage`'da |
| Build | Yok — bundler yok, transpiler yok, `package.json` yok |
| Backend | Yok — sunucu kodu yok, veritabanı yok, giriş sistemi yok |
| Barındırma | Statik dosyaları sunan tek bir `nginx:alpine` Docker konteyneri |

## Ekranlar

### Ana sayfa

![Ana sayfa](images/01-home.png)

- En üstte kapatılabilir tanıtım şeridi ("A$50 üzeri siparişlerde ücretsiz teslimat | Türkiye'de el yapımı")
- Mağaza logosu, kategori menüsü ve arama / hesap / sepet ikonlarıyla koyu lacivert üst menü
- Üç slaytlı, ok kontrollü ve nokta göstergeli hero slayt gösterisi
- Avustralya doları fiyatları, yıldız puanları ve kırmızı SALE rozetleriyle "New Arrivals" ürün ızgarası — yanık halde fotoğraflanmış el yapımı mozaik lambalar, plaj çekimli havlularla yan yana

Hero'dan footer'a tüm sayfa turu:

![Ana sayfa — tam tur](images/01b-home-full.png)

- Mosaic Lamps, Turkish Ceramics, Evil Eye, Cotton Towels ve SALE için "Shop by Collection" kutucukları
- "Create Your Own Mosaic Lamp" atölye afişi ve "Sale Picks" ızgarası
- "Bridging Istanbul & Australia" hikâye bölümü ve müşteri yorumları şeridi
- Güven şeridi (ücretsiz kargo, el yapımı, puan, güvenli ödeme) ile bülten kaydı ve ödeme ikonları içeren footer

### Koleksiyon sayfası

![Cotton Towels koleksiyonu](images/02-collection-towels.png)

- Başlık, açıklama ve tam genişlikte fotoğraflı kategori hero afişi
- Breadcrumb navigasyonu ve ürün sayısı (Cotton Towels için "8 products")
- "Refine Results" kenar paneli: renk seçenekleri, fiyat aralıkları ve "On Sale Only" kutusu
- Sağ üst köşede "Sort by" sıralama menüsü
- SALE rozetleri, üstü çizili eski fiyatlar ve yorum sayılı yıldız puanlarıyla ürün kartları

### İndirim koleksiyonu

![İndirim koleksiyonu](images/03-collection-sale.png)

- `#/collections/sales` adresinde, kırmızı temalı hero ile özel indirim sayfası: "Sale — Up to 42% Off Handcrafted Turkish Goods"
- Tüm kategorilerdeki indirimli ürünleri tek ızgarada toplar (15 ürün)
- Her kart, indirimli fiyatı üstü çizili orijinal fiyatın yanında gösterir
- Aynı filtre paneli ve sıralama kontrolleri burada da çalışır

### Ürün detayı

![Ürün detay sayfası](images/04-product-detail.png)

- Ana fotoğrafın altında küçük görsellerle büyük görsel galerisi
- SALE rozeti, indirimli fiyat, orijinal fiyat ve "Save A$20.00" etiketi
- Yorum sayılı yıldız puanı ve yeşil stok durumu satırı ("In Stock — Ships within 2–5 business days")
- Renk varyantı düğmeleri (bu örnekte Multicolour / Blue)
- Öne çıkan "Add to Cart" düğmesinin yanında adet seçici
- Düğmenin altında avantaj ikonları: A$50 üzeri ücretsiz kargo, hediye LED ampul

### Sepete eklendi bildirimi

![Sepete eklendi bildirimi](images/04b-add-to-cart-toast.png)

- "Add to Cart" tıklandığında sağ alt köşede koyu bir bildirim belirir: ürünün küçük görseli ve adıyla "Added to cart!"
- Üst menüdeki sepet ikonu, ürün sayısı rozetiyle anında güncellenir
- Sayfa yenilenmez — sepet durumu doğrudan localStorage'a yazılır

### Hızlı Bakış (Quick View)

![Hızlı Bakış](images/05-quick-view.png)

- Izgaradaki her ürün kartında, bir pencere açan Hızlı Bakış eylemi bulunur
- Pencere; ürün görselini, fiyatı, puanı ve kısa açıklamayı iki panelli bir düzende gösterir
- Adet seçici ve "Add to Cart" düğmesiyle sayfadan ayrılmadan alışveriş yapılabilir
- "View Full Details" bağlantısı tam ürün sayfasına götürür

### Sepet — boş

![Boş sepet](images/06-cart-empty.png)

- Sepet çizimiyle sıcak bir boş durum ekranı: "Your Cart is Empty"
- İki net yönlendirme düğmesi: "Shop the Sale" ve "Explore All"
- Footer görünür kalır; navigasyon hiçbir zaman çıkmaza girmez

### Sepet — dolu

![Dolu sepet](images/07-cart-filled.png)

- Küçük görseller, seçilen renk varyantları, ürün başına adet seçiciler ve Remove bağlantılarıyla ürün listesi
- Ara toplam, kargo ve genel toplam içeren Order Summary kartı
- Ücretsiz kargo mantığı iş başında: A$50'de banner yeşile döner — "You qualify for free shipping!" — ve kargo FREE olur
- "Proceed to Checkout" düğmesi — demo olduğu için yalnızca, gerçek bir mağazada güvenli ödeme sayfasına yönlendirileceğini açıklayan bir tarayıcı uyarısı gösterir
- Özetin altında güven rozetleri (SSL Secure, Multiple Payment Options)

### Mobil görünüm

<img src="images/08-mobile-home.png" width="390">

- Tasarım telefon ekranlarına uyum sağlar: tek sütunlu ürün ızgarası ve kompakt üst menü
- Hero slayt gösterisi ve tanıtım şeridi dar ekranlarda da çalışmaya devam eder
- Navigasyon, solda bir hamburger ikonuna dönüşür

<img src="images/09-mobile-menu.png" width="390">

- Hamburger ikonu, sayfanın üzerine kayan bir çekmece menü açar
- Ana sayfaya, dört koleksiyona, SALE'e (kırmızı vurgulu) ve Sepete doğrudan bağlantılar
- Çekmecenin üstünde büyük bir kapatma düğmesi ve mağaza logosu

## Mimari

```
Tarayıcı
  └─ index.html  ─ saf JS modüllerini yükler (bundler yok)
       ├─ router.js        hash tabanlı router: location.hash'i okur
       │                   (#/, #/collections/<slug>, #/products/<slug>, #/cart)
       │                   ve eşleşen sayfayı render eder; bilinmeyen rotalar
       │                   ana sayfaya döner
       ├─ bileşenler       elle yazılmış modüller: heroSlideshow, filterSidebar,
       │                   quickView, toast, sepet sayfası, ürün sayfası ...
       ├─ js/data/products.js   4 koleksiyonda 22 sabit kodlu ürün
       └─ cart.js          localStorage'da sepet durumu (anahtar: igb_cart_v1)

Sunucu tarafı
  └─ nginx:alpine Docker konteyneri (yalnızca statik dosyalar)
       └─ ekosistemin merkezi ters proxy'sinin (ftcom-nginx) arkasında çalışır;
          authenticbazaar.furkantekkartal.com trafiği ona yönlendirilir
```

- **Hash router:** navigasyon yalnızca `location.hash` değerini değiştirir; tarayıcı sayfayı asla yeniden yüklemez. Router `hashchange` olayını dinler, slug'ı çözümler ve doğru görünümü render eder. Böylece hiçbir yönlendirme kütüphanesi olmadan SPA davranışı elde edilir.
- **Bileşenler:** her arayüz parçası (slayt gösterisi, filtre paneli, hızlı bakış penceresi, toast) küçük ve bağımsız bir JS modülüdür. Sanal DOM yoktur — modüller gerçek DOM öğelerini doğrudan oluşturur ve günceller.
- **Sepet:** `localStorage` etrafında ince bir modül. Ekleme, silme ve adet değişiklikleri anında kaydedilir; sepet sayfa yenilemelerinde ve tarayıcı yeniden başlatmalarında korunur. Ücretsiz kargo ilerlemesi de aynı durumdan hesaplanır.
- **Dağıtım:** sitenin tamamı, statik dosyaları sunan tek bir `nginx:alpine` konteyneridir. Ekosistemin ortak Docker ağında çalışır; merkezi ters proxy, genel alan adını karşılar ve trafiği bu konteynere iletir. Backend süreci de veritabanı da yoktur.

---

🇬🇧 [Click here for the English version](README.md)

*Bu README, [ProjectReadmes](../) koleksiyonunun bir parçasıdır — Furkan Tekkartal'ın projeleri için portfolyo dokümantasyonu.*
