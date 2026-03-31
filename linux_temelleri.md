# Linux Temelleri ve Komut Satırı Notları

Bu doküman, Linux işletim sisteminin yapısı, temel bileşenleri ve en çok kullanılan terminal komutları hakkında bir rehber niteliğindedir.

---

## 1. Linux Nedir? 
Birçok kişinin bildiğinin aksine, Linux tek başına bir işletim sistemi değil, bir **çekirdektir (kernel)**.

* **Çekirdek (Kernel):** Donanım ile yazılım arasındaki iletişimi sağlayan, bilgisayarın beyni gibi çalışan temel yazılımdır. RAM, işlemci ve disk gibi kaynakları yönetir.
* **Açık Kaynak (Open Source):** Linux çekirdeği açık kaynak kodludur; yani herkes kodu inceleyebilir, değiştirebilir ve özelleştirebilir.
* **GNU/Linux:** Günümüzde "Linux" dediğimiz işletim sistemi aslında Linux çekirdeği ve bu çekirdek üzerinde çalışan GNU araçlarının (komutlar, programlar) birleşimidir.
* **GNU:** "GNU's Not Unix" (GNU Unix Değildir) ifadesinin kısaltmasıdır. Yazılımların özgür olmasını amaçlar.

---

## 2. Kabuk (Shell) ve Ortam Değişkenleri 
Kullanıcı ile çekirdek arasında bir köprü görevi gören katmana **Shell (Kabuk)** denir.

* **Görevi:** Kullanıcıdan aldığı komutları çekirdeğin anlayacağı dile çevirir.
* **Yaygın Türler:** `bash` (en popüler olanı), `zsh`, `fish`, `ksh`.
* **Ortam Değişkenleri (Environment Variables):** Sistemin davranışını belirleyen değerlerdir.
    * `PATH`: Sistemde bir komut yazıldığında, bilgisayarın o programı hangi klasörlerde arayacağını belirler.
* **Görüntüleme Komutları:**
    * `set`: Shell değişkenlerini gösterir.
    * `printenv`: Ortam değişkenlerini gösterir.
    * `env`: Export edilmiş değişkenleri listeler.

---

## 3. Dosya Sistemi Yapısı 
Linux'ta her şey bir dizin (directory) yapısı ile başlar ve buna **root (kök dizin)** denir. Simgesi `/` işaretidir.

| Dizin | Açıklama |
| :--- | :--- |
| `/home` | Kullanıcıya özel dosyaların bulunduğu yer. |
| `/bin` | Temel komut programları (`ls`, `cd` vb.). |
| `/etc` | Sistem yapılandırma (ayar) dosyaları. |
| `/usr` | Kullanıcı uygulamaları ve dosyaları. |

---

## 4. Temel Terminal Komutları 
Terminalde işleri hızlandıran en önemli komutlar:

* `ls`: Bulunduğunuz klasördeki dosyaları listeler.
* `cd`: Klasörler arasında geçiş yapar (Change Directory).
* `mkdir`: Yeni bir klasör oluşturur. (Örn: `mkdir proje1`)
* `grep`: Dosya içinde belirli bir kelimeyi arar. (Örn: `grep hata log.txt`)
* `top`: Çalışan işlemleri, CPU ve RAM kullanımını canlı izlemeyi sağlar. (`q` ile çıkılır).

---

## 5. Dosya İzinleri ve Paket Yönetimi 
Linux güvenlik odaklı bir sistemdir. Her dosyanın 3 tür izni vardır:

1.  **r (Read):** Okuma 
2.  **w (Write):** Yazma 
3.  **x (Execute):** Çalıştırma 

**Kullanıcı Grupları:** Owner (Sahibi), Group (Grup), Others (Diğerleri).  
*Örnek komut:* `chmod +x script.sh` (Dosyayı çalıştırılabilir hale getirir).

### Paket Yöneticileri 
Program yüklemek, güncellemek ve silmek için kullanılır:
* **apt:** Debian ve Ubuntu tabanlı sistemler.
* **dnf:** Fedora ve RedHat tabanlı sistemler.
* **pacman:** Arch Linux tabanlı sistemler.

---

## 6. Servis Yönetimi (systemctl) 
Arka planda çalışan programlara **servis** denir (Web server, veritabanı vb.).

| Komut | Açıklama |
| :--- | :--- |
| `systemctl start [servis]` | Servisi başlatır. |
| `systemctl stop [servis]` | Servisi durdurur. |
| `systemctl restart [servis]` | Servisi yeniden başlatır. |
| `systemctl status [servis]` | Servis durumunu gösterir. |
