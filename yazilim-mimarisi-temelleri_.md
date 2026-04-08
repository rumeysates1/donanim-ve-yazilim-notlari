# 10. Yazılım Mimarisi Temelleri


## 1. Monolith vs Microservice

### Monolith Nedir?

Tüm uygulamanın tek bir kod tabanı olduğu klasik yapıdır. Başlangıç projeleri ve küçük ekipler için idealdir çünkü geliştirmek, debug etmek ve deploy etmek kolaydır.

```
my-app/
├── login.js      ← giriş işlemleri
├── products.js   ← ürünler
├── orders.js     ← siparişler
└── payments.js   ← ödemeler

→ Hepsi birlikte çalışır, birlikte deploy edilir.
```

### Microservice Nedir?

Her bir özelliğin (auth, ödeme, ürün) bağımsız bir servis olarak çalıştığı mimaridir. Netflix, Amazon gibi büyük sistemlerin tercihidir. Ancak bu karmaşıklıkla birlikte gelir: servisler arası iletişim, distributed tracing, container yönetimi gerektirir.

```
auth-service     → sadece giriş-çıkış işlemleri
product-service  → sadece ürünler
order-service    → sadece siparişler
payment-service  → sadece ödemeler

→ Hepsi birbirinden bağımsız çalışır.
```
---

## 2. MVC ve MVVM Mimari Desenleri

Kod satırlarının birbirine karışmasını önlemek için kodun sorumluluklarını üçe bölen desenlerdir.

### MVC — Model, View, Controller

Backend dünyasının temelidir (Laravel, Rails, Django).

**Restoran benzetmesi:**
```
Müşteri → Garson → Mutfak → Garson → Müşteri
(Kullanıcı) (Controller) (Model) (View)
```

| Katman | Görevi |
|---|---|
| **Controller** | HTTP isteğini alır, Model'e iletir, View'e gönderir. İş mantığı içermez. |
| **Model** | Veri ve iş kuralları. Veritabanı işlemleri burada. |
| **View** | Sadece gösterim. HTML veya JSON. İş mantığı içermez. |

**Veri akışı:** Tek yönlü → Controller → Model → View

### MVVM — Model, View, ViewModel

Frontend dünyasının temelidir (React, Vue, Angular). Sayfa yenilenmeden anlık güncelleme sağlar.

**Akıllı ev benzetmesi:**
```
Işık Şalteri ⇄ Kontrol Paneli → Elektrik Sistemi
   (View)        (ViewModel)        (Model)
```

**MVC ile MVMM arasındaki kritik fark:**

```
MVC:   View → Controller → Model      (tek yön)
MVVM:  View ⇄ ViewModel  → Model      (çift yön!)
```

---

## 3. State Management

### State Nedir?

**Uygulamanın o anki hafızasıdır.** Bir şey olunca değişir.
```
Kullanıcı giriş yaptı mı?   → state: true / false
Sepette kaç ürün var?        → state: 0, 1, 2...
Karanlık tema açık mı?       → state: true / false
Yükleniyor mu?               → state: true / false
```

### Local State 

Sadece tek bir bileşenin kendi içinde kullandığı state. `useState` ile tanımlanır.
Her bileşenin kendi local state'i **tamamen bağımsızdır.** 

### Global State 

Birden fazla bileşenin aynı anda bilmesi gereken state.

```
Header bileşeni   → "Merhaba Ahmet" göstermeli
Profil sayfası    → Ahmet'in bilgilerini göstermeli
Sepet sayfası     → Ahmet'in siparişlerini göstermeli
Admin paneli      → Ahmet admin mi diye kontrol etmeli
```

Merkezi bir **pano** gibi çalışır:
```
┌─────────────────────────┐
│      GLOBAL STATE       │
│                         │
│  kullanici: "Ahmet"     │
│  sepetAdedi: 3          │
│  tema: "karanlik"       │
└─────────────────────────┘
→ Herkes okuyabilir, herkes güncelleyebilir.
→ Pano değişince onu okuyan TÜM bileşenler otomatik güncellenir.
```

### Prop Drilling Problemi

Global state olmadan ortaya çıkan kabus. Veriyi katman katman elle taşımak zorunda kalırsın:

```
App (kullanıcı bilgisi burada)
  ↓ kullanıcıyı gönder
  Header
    ↓ kullanıcıyı gönder
    Navigation
      ↓ kullanıcıyı gönder
      UserMenu
        ↓ kullanıcıyı gönder
        Avatar  ← SADECE BURASI KULLANIYOR
```

Global state ile Avatar direkt panodan alır, aradaki hiç kimse taşımaz.

### Kötü State Yönetiminin Sonuçları

- **Prop drilling** — veriyi katman katman elle taşımak
- **Gereksiz render** — alakasız bileşenler de yeniden çizilir, uygulama yavaşlar
- **Sync sorunu** — aynı veriyi iki yerde tutunca biri güncellenir diğeri güncellenmez

### Özet Tablosu

| Kavram | Ne zaman kullan | Örnek |
|---|---|---|
| Local state | Sadece bir bileşen kullanıyorsa | Menü açık/kapalı |
| Global state | Birden fazla yer bilmesi gerekiyorsa | Kullanıcı girişi, sepet |
| Prop drilling | Kaçınılması gereken kötü pratik | Veriyi 5 katman taşımak |

---

## 4. Katmanlı Mimari (Controller → Service → Repository)

En önemli mimari prensiplerden biri. Kodu sorumluluğa göre 3 katmana bölmek. Her katmanın tek bir işi var, sadece bir altındakiyle konuşuyor.

```
Kullanıcı isteği
      ↓
  Controller   ← sadece HTTP bilir
      ↓
   Service     ← sadece iş kuralları bilir
      ↓
  Repository   ← sadece veritabanı bilir
      ↓
  Veritabanı
```

### Controller — Kapıcı

HTTP isteğini karşılar, Service'e iletir, cevabı döner. Hesaplama yapmaz, veritabanına gitmez.

### Service — Beyin

İş kuralları burada. "Stok 0 ise satma", "Admin değilse gösterme" gibi kararlar hep burada alınır. Veritabanını doğrudan bilmez.

### Repository — Depo Görevlisi

Sadece veritabanıyla konuşur. Veri çek, kaydet, sil. Başka hiçbir şey.

## Genel Özet

| Konu | Tek cümlelik özet |
|---|---|
| **Monolith** | Tüm kod tek yerde, birlikte deploy edilir |
| **Microservice** | Her özellik bağımsız bir servis olarak çalışır |
| **MVC** | Controller istek alır → Model veri işler → View gösterir (backend) |
| **MVVM** | View ile ViewModel çift yönlü bağlı, state değişince UI otomatik güncellenir (frontend) |
| **State Management** | Uygulamanın hafızası; local = tek bileşene ait, global = herkesin paylaştığı |
| **Katmanlı Mimari** | Controller → Service → Repository; her katmanın tek bir işi var |
