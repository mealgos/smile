<div align="center">

# Smi/e

**Bulut tabanlı depo, stok ve saha yönetim platformu**

Masaüstü ERP · Mobil saha uygulaması · Operatör kontrol paneli — tek ekosistem.

</div>

---

## Smi/e nedir?

**Smi/e**, küçük ve orta ölçekli işletmelerin deposunu, siparişlerini, cari hesaplarını ve
saha ekiplerini uçtan uca yönetmesi için geliştirilmiş bir iş platformudur. Üç uygulamadan oluşur
ve hepsi aynı güvenli veritabanı üzerinde birebir senkron çalışır:

| Uygulama | Ne işe yarar | Teknoloji |
|---|---|---|
| 🖥️ **Masaüstü ERP** (`frontend/`) | Sipariş, cari, ürün/stok, çek, satın alma, teklif, personel, gider, raporlar ve yedekleme. Çevrimdışı-öncelikli çalışır. | Next.js + React + TypeScript + Electron |
| 📱 **Mobil** (`mobile/`) | Saha ve depo ekibi için: sipariş hazırlık, teslimat (şoför), mal kabul, sayım, sorgulama, cari görüntüleme, patron finansal özeti. | Expo (React Native) + TypeScript |
| 🛡️ **Operatör Paneli** (`operator/`) | Yalnızca operatöre özel, yerel çalışan firma yönetim paneli: firma ekleme, kapasite izleme, yedek/dışa aktarma. | Next.js + Electron |

---

## Öne çıkan özellikler

- **Çevrimdışı-öncelikli masaüstü** — internet kesilse de çalışmaya devam eder, bağlantı gelince kuyruğu senkronlar.
- **Gerçek zamanlı mobil–masaüstü senkron** — ofiste girilen sipariş sahada anında belirir; sahadaki işlem ofise anlık bildirimle düşer.
- **Kalem bazlı sipariş hazırlığı** — depo çalışanı ürünleri tek tek “Hazır” işaretler; sipariş durumu otomatik güncellenir.
- **Teslimat (şoför) akışı** — yoldaki teslimatlar, kalem bazlı teslim onayı, opsiyonel teslim fotoğrafı.
- **Stok sayımı & mal kabul** — varyantlı ürünlerde kombinasyon bazında sayım; gelen malın teslim takibi (stok mükerrer sayılmaz).
- **Barkod okuma** — kameradan barkodla anında ürün bulma (opsiyonel).
- **Rol ve yetki sistemi** — her kullanıcı yalnızca yetkili olduğu modülleri görür; hassas veriler (alış fiyatı vb.) yetkiye bağlıdır.
- **Finansal raporlar** — kâr/zarar, marj, cari yaşlandırma, ödeme dağılımı, en çok satılanlar; proaktif uyarılar.
- **Yedekleme & geri yükleme** — çok tablolu tutarlı yedek, geri dönüşüm kutusu ile güvenli silme.

---

## Mimari (özet)

- **Çok kiracılı (multi-tenant) hibrit model** — paylaşımlı kiracı (varsayılan) veya işletmeye özel adanmış veritabanı.
  İzolasyon veritabanı seviyesinde Row-Level Security ile sağlanır.
- **Supabase** (PostgreSQL + Auth) veri katmanı; Avrupa Birliği bölgesinde barındırma.
- **Şema göçleri** `supabase/migrations/` altında sürümlenir; her değişiklik tüm kiracılara kontrollü uygulanır.
- **Güvenlik** — uygulamalar yalnızca genel (public-safe) anahtarları taşır; ayrıcalıklı anahtarlar sadece operatör makinesinde kalır.

> Depo yapısı: `frontend/` (müşteri uygulaması) ve `operator/` (operatör paneli) tamamen bağımsızdır; birbirinden import etmezler.

---

## Depo yapısı

```
.
├── frontend/    # Masaüstü ERP (Next.js + Electron)
├── mobile/      # Mobil saha uygulaması (Expo)
├── operator/    # Operatör kontrol paneli (yerel-only)
├── supabase/    # Şema göçleri + çok-kiracılı sağlama runbook'ları
└── Brain/       # Proje bilgi tabanı (yol haritası, kararlar, şema referansı)
```

---

## Durum

- Masaüstü ERP: **üretimde** (Windows kurulum paketi ile dağıtılıyor, otomatik güncelleme).
- Mobil uygulama: **App Store yayınına hazırlanıyor** (TestFlight'ta test edildi).
- Operatör paneli: **çekirdek tamam**, yerel kullanımda.

---

<div align="center">
<sub>© 2026 <strong>Smi/e Corp</strong> — Tüm hakları saklıdır. Bu depo özel/kapalı kaynaktır.</sub>
</div>
