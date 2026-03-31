#  Veritabaný Mantýðý ve SQL Temelleri

Bu notlar, iliþkisel veritabanlarýnýn çalýþma prensiplerini ve temel SQL komutlarýný içeren bir baþlangýç rehberidir.

---

## 1. Ýliþkisel Veritabaný (Relational Database) 
Verilerin birbirleriyle belirli mantýksal baðlar kurularak **tablolar** halinde saklandýðý bir sistemdir. 

* **Yapý:** Her tablo belirli bir varlýðý (Müþteriler, Kitaplar vb.) temsil eder.
* **Düzen:** Veriler satýr ve sütunlardan oluþur. Bu sayede veri tekrarý önlenir ve bilgiler düzenli bir þekilde saklanýr.



---

## 2. Anahtarlar: Primary Key ve Foreign Key 

Tablolar arasýndaki baðlantýyý saðlayan ve verilerin benzersizliðini koruyan yapýlardýr.

| Kavram | Taným | Örnek |
| :--- | :--- | :--- |
| **Primary Key (Birincil Anahtar)** | Her satýrý benzersiz yapan kimlik numarasýdýr. Boþ býrakýlamaz. | T.C. Kimlik No, Öðrenci No |
| **Foreign Key (Yabancý Anahtar)** | Bir tablodaki veriyi baþka bir tabloya baðlamak için kullanýlan "köprü"dür. | Sipariþ tablosundaki "Müþteri No" |

---

## 3. SQL Sorgu Temelleri 

Veritabanýndaki ham veriyi anlamlý raporlara dönüþtürmek için kullanýlan 3 ana komut:

* **SELECT:** Tablodaki verileri çaðýrarak belirli sütunlarý listeler. ??
* **JOIN:** **Primary Key** ve **Foreign Key** baðýný kullanarak iki farklý tabloyu yan yana getirir. 
* **GROUP BY:** Benzer verileri gruplayarak üzerlerinde hesaplama (toplam, ortalama, sayým) yapar. 

---

## 4. Index 

Veritabanýndaki verilere çok daha hýzlý eriþmek için oluþturulan özel bir yapýdýr. Týpký bir kitabýn baþýndaki "Ýçindekiler" bölümü gibi çalýþýr.

### Neden Kullanýlýr?
1. **Hýz:** Milyonlarca satýr arasýndan aranan veriyi tüm tabloyu taramadan bulur.
2. **Sýralama:** Verilerin alfabetik veya sayýsal olarak hýzlýca dizilmesini saðlar.
3. **Performans:** Sunucu iþlemcisini gereksiz taramalardan kurtarýr.

> ** Önemli Not:** Ýndeksler arama hýzýný artýrsa da diskte ek yer kaplar ve veri yazma (ekleme/güncelleme) iþlemlerini yavaþlatabilir. Bu yüzden sadece **sýkça sorgulanan** sütunlara eklenmelidir.