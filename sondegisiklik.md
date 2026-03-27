# Son Degisiklikler - Migros Stratejik Analiz Sunum Projesi

## Tarih: 2026-03-27

---

## 1. CSS Mimarisi Yeniden Yapılandırıldı (Code Architect)

**Dosya:** `wwwroot/css/presentation.css` (YENİ)

- **Ne:** Index.cshtml icindeki ~145 satir inline `<style>` blogu tamamen kaldirildi ve ayri bir CSS dosyasina tasindi.
- **Neden:** Web tasarim standartlarina gore CSS, HTML'den ayri tutulmalidir. Inline CSS bakim zorlugu yaratir, cache'lenemez ve tekrar kullanilamaz. Ayri dosya sayesinde tarayici CSS'i onbellegine alir, sayfa daha hizli yuklenir.

**Dosya:** `wwwroot/css/site.css` (GUNCELLENDI)

- **Ne:** Varsayilan ASP.NET MVC sablonu stilleri (footer, form-floating vb.) temizlendi.
- **Neden:** Bu stiller projede kullanilmiyordu ve bazi durumlarda (ornegin `body { margin-bottom: 60px }`) mevcut tasarimla cakisiyordu.

**Dosya:** `Views/Shared/_Layout.cshtml` (GUNCELLENDI)

- **Ne:** Yeni `presentation.css` dosyasi `<link>` ile baglandi.
- **Neden:** CSS dosyasinin sayfada aktif olmasi icin HTML'de referans verilmesi gerekir.

---

## 2. CSS Degisken Sistemi Genisletildi (Code Architect)

**Dosya:** `wwwroot/css/presentation.css`

- **Ne:** `:root` altinda 20+ yeni CSS degiskeni tanimlandi (--bg-card, --border-subtle, --text-primary, --shadow-orange, --transition-smooth vb.)
- **Neden:** Tum renk, golge, gecis ve radius degerleri tek noktadan yonetilir. Tutarlilik saglar, gelecekte tema degisikligini kolaylastirir.

---

## 3. Sidebar Navigasyonu Duzeltildi (UI/UX Designer)

**Dosya:** `Views/Shared/_Layout.cshtml`

### 3a. Yanlis Etiketler Duzeltildi
- **Ne:** Sidebar'daki sec-7 "AS-IS SUREC HARITASI", sec-8 "BALIK KILCIGI", sec-9 "5 NEDEN TEKNIGI" etiketleri icerikle eslesmiyor du. sec-9 icerikte hic yoktu.
- **Duzeltme:** sec-7 = "Balik Kilcigi", sec-8 = "5 Neden Teknigi". sec-9 kaldirildi.
- **Neden:** Navigasyon linkleri icerigin gercek basliklarini yansitmalidir, kullanici yanlisa yonlendirilmemeli.

### 3b. Tekrarli Ikonlar Degistirildi
- **Ne:** 5 farkli bolumde ayni `bi-map` ikonu kullaniliyordu.
- **Duzeltme:** Her bolume kendine ozgu ikon atandi (bi-grid-3x3-gap-fill, bi-arrows-angle-expand, bi-filter-square-fill, bi-calculator-fill, bi-diagram-2-fill, bi-share-fill, bi-search-heart).
- **Neden:** Gorsel hiyerarsi ve ayirt edilebilirlik icin her bolumun kendine ait bir ikonu olmalidir.

### 3c. Sidebar Stili Iyilestirildi
- **Ne:** Font boyutu kuculdu (0.82rem), gradient aktif link, ozel scrollbar, bolum ayirici (divider) eklendi.
- **Neden:** 8 bolum listelenince sidebar kalabalik duruyordu. Daha kompakt ve profesyonel gorunum saglandi.

---

## 4. Bolum Numaralari Duzeltildi (UI/UX Designer)

**Dosya:** `Views/Home/Index.cshtml`

- **Ne:** sec-7 (Balik Kilcigi) "BOLUM VI" yaziyordu → "BOLUM VII" olarak duzeltildi. sec-8 (5 Neden) "BOLUM VII" yaziyordu → "BOLUM VIII" olarak duzeltildi.
- **Neden:** Sirali numaralama bozuktu (BOLUM VI iki kez kullanilmisti). Sunumda izleyici karisir.

---

## 5. SWOT Kutu Kenar Renkleri Eklendi (Frontend Developer)

**Dosya:** `wwwroot/css/presentation.css`

- **Ne:** `.s-border`, `.w-border`, `.o-border`, `.t-border` CSS siniflari tanimlandi (sirasiyla yesil, kirmizi, mavi, sari ust kenar). Hover durumunda renk golgesi eklendi.
- **Neden:** HTML'de bu siniflar kullaniliyordu ama CSS'te tanimli degildi → kutuların hicbir renk kenari yoktu. Simdi her SWOT kategorisi kendi rengiyle ayirt ediliyor.

---

## 6. Scroll Animasyonlari Eklendi (UI/UX Designer)

**Dosya:** `wwwroot/css/presentation.css` + `Views/Shared/_Layout.cshtml`

- **Ne:** Tum section kartlarina `fade-in-section` sinifi eklendi. IntersectionObserver ile sayfa kaydirildiginda bolumlerin asagidan yukariya yumusak sekilde belirmesi (fade-in-up) saglandi.
- **Neden:** Sunum sitesi icin bu cok onemli. Izleyiciler icerige bakarken her bolum animasyonla gelirse dikkat cekilir ve profesyonel gorunum saglanir.

---

## 7. Scroll Spy (Aktif Navigasyon Takibi) Eklendi (Frontend Developer)

**Dosya:** `Views/Shared/_Layout.cshtml`

- **Ne:** Kullanici sayfayi kaydirildiginda o an gorunen bolumun sidebar'daki linki otomatik olarak aktif (turuncu) olur.
- **Neden:** Sunumda hangi bolumde oldugunuz her an belli olmali. Izleyiciler sidebar'a bakarak konumu gorebilir.

---

## 8. Smooth Scrolling Eklendi (Frontend Developer)

**Dosya:** `wwwroot/css/presentation.css`

- **Ne:** `html { scroll-behavior: smooth; }` eklendi.
- **Neden:** Sidebar linklerine tiklandiginda sayfa ani ziplama yerine yumusak kaydirma yapar. Daha profesyonel sunum deneyimi.

---

## 9. Responsive Tasarim Eklendi (Frontend Developer)

**Dosya:** `wwwroot/css/presentation.css`

- **Ne:** 3 breakpoint eklendi: Tablet (992px), Mobil (768px), Kucuk Mobil (480px).
- **Degisiklikler:**
  - SIPOC grid: 5 kolon → 3 kolon (tablet) → 1 kolon (mobil)
  - Section card padding ve border-radius kucultuld
  - Tablo font boyutlari ayarlandi
  - Balik Kilcigi SVG padding azaltildi
  - Takim fotograf boyutlari kucultuld
- **Neden:** Orijinal tasarimda hicbir responsive breakpoint yoktu. SIPOC grid mobilde tamamen bozuluyordu.

---

## 10. Mobil Sidebar Davranisi Eklendi (Frontend Developer)

**Dosya:** `Views/Shared/_Layout.cshtml`

- **Ne:** 768px altinda sidebar varsayilan olarak gizli baslar, toggle butonuyla acilir. Link tiklaninca otomatik kapanir.
- **Neden:** Mobilde sidebar sabit durursa icerik gorunmez. Overlay menu modeli mobil standartlarinda zorunludur.

---

## 11. Takim Fotograf Placeholder'lari Duzeltildi (UI/UX Designer)

**Dosya:** `Views/Home/Index.cshtml`

- **Ne:** Kirik `/images/user1.jpg` referanslari kaldirildi. Yerine gradient arka planli, Bootstrap Icons kullanilarak olusturulmus SVG-benzeri placeholder avatarlar eklendi.
- **Neden:** Orijinalde resim dosyasi (user1.jpg) wwwroot/images klasorunde yoktu → kirik resim ikonu gorunuyordu. Yeni placeholder hem gorsel hem de profesyonel.

---

## 12. Particles.js Etkilesimi Gelistirildi (UI/UX Designer)

**Dosya:** `Views/Shared/_Layout.cshtml`

- **Ne:** Mouse hover'da parcaciklarin birbirine baglanmasi (grab modu) eklendi. Parcacik sayisi 60→50, hiz ve opasite ayarlandi.
- **Neden:** Sunum sirasinda mouse hareketi ile arka planda hafif bir etkilesim sunum kalitesini arttirir.

---

## 13. Section Card Hover Efekti Iyilestirildi (UI/UX Designer)

**Dosya:** `wwwroot/css/presentation.css`

- **Ne:** Hover'da ust kenarda gradient turuncu cizgi (::before pseudo element) belirme efekti eklendi. Turuncu golge (shadow-orange) eklendi.
- **Neden:** Orijinalde hover'da sadece translateY ve border-color degisiyordu. Yeni efekt daha estetik ve dikkat cekici.

---

## 14. Liste Bullet Stili Modernlestirildi (UI/UX Designer)

**Dosya:** `wwwroot/css/presentation.css`

- **Ne:** Buyuk "•" metin karakteri yerine 8px turuncu CSS daire (border-radius: 50%) kullanildi.
- **Neden:** Metin bullet'i farkli tarayici/fontlarda tutarsiz gorunur. CSS dairesi her yerde ayni gorunur ve boyutu kontrol edilebilir.

---

## 15. Erisilebilirlik (Accessibility) Iyilestirmeleri (Frontend Developer)

**Dosyalar:** `_Layout.cshtml`, `Index.cshtml`

- **Ne:**
  - Sidebar toggle butonuna `aria-label` eklendi
  - Nav elemanina `role="navigation"` ve `aria-label` eklendi
  - Migros logo'larina `alt` text eklendi
  - SVG Balik Kilcigi diyagramina `role="img"` ve `aria-label` eklendi
- **Neden:** WCAG 2.1 standartlarina uyum. Ekran okuyucular icin erisim saglama.

---

## 16. Footer Eklendi (UI/UX Designer)

**Dosya:** `Views/Home/Index.cshtml` + `wwwroot/css/presentation.css`

- **Ne:** Sayfa sonuna "YBS2210 Stratejik Surec Analizi - Migros Ticaret A.S. Proje Sunumu" footer'i eklendi.
- **Neden:** Profesyonel sunumlarda sayfa sonu bilgi satiri standarttir. Ders kodu ve proje ismi belirtilir.

---

## 17. Title Tag Guncellendi (Code Architect)

**Dosya:** `Views/Shared/_Layout.cshtml`

- **Ne:** "LunaMigrosProject" → "Migros Stratejik Analiz" olarak duzeltildi.
- **Neden:** Tarayici sekmesinde proje kodu yerine anlamli baslik gosterilmeli.

---

## Degisiklik Yapilan Dosyalar Ozeti

| Dosya | Islem |
|-------|-------|
| `wwwroot/css/presentation.css` | YENI - Tum sunum stilleri |
| `wwwroot/css/site.css` | GUNCELLENDI - Gereksiz stiller temizlendi |
| `Views/Shared/_Layout.cshtml` | GUNCELLENDI - Sidebar, scroll spy, animasyon, responsive |
| `Views/Home/Index.cshtml` | GUNCELLENDI - Inline CSS kaldirildi, animasyon class'lari, placeholder, bolum numaralari, footer |
| `sondegisiklik.md` | YENI - Bu dosya |
