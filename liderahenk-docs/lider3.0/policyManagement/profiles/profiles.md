**Profiller**

Bir eklentide gerçekleştirilebilecek yapılandırma ayarlarının bütününe Profil denir. Bir veya birden fazla profil bir 
araya gelerek politikayı oluşturur. Tek başına çalıştırılamaz. Bir politika üzerine eklendikten sonra kullanılabilir. 
Örneğin; Tarayıcı eklentisi için; Lider Arayüz üzerinden eklenti aracılığı ile anasayfa belirleme gibi yapılandırma 
ayarlarının belirlenip kaydedilmesi ile profil oluşturulabilir.

![Profile](../images/profiles/profiles.png)

**İnternet Tarayıcı Ayarları**

İnternet tarayıcı ayalarında internet tarayıcısının vekil sunucu, giriş sayfası, sekme ayarları, gizlilik ayarları, 
döküman indirme gibi özelleştirmeler yapılabilir.

![Profile](../images/profiles/browserProfile.png)

![Profile](../images/profiles/browserPolicy.png)

**Rsyslog Ayarları**

Rsyslog eklentisi bir profil eklentisi olup Ahenk makinesinde bulunan log dosyalarının- rotasyon konfigürasyonun 
sağlanmasına yardımcı olmaktadır.

Profilde, kullanıcı log dosyalarının rotasyon sıklığını (günlük, haftalık, aylık, yıllık), ne kadar eski logu tutacağı 
bilgisini, log dosyasının rotasyonu için gereken dosya büyüklüğü miktarını(MB) belirleyebilmektedir. Ayrıca kullanıcıya 
log dosyaları ile ilgili; rotasyondan sonra yeni log dosyası yaratılsın, eski log dosyaları sıkıştırılsın, log dosyası 
yok ise hata verilmeden geçilsin gibi seçenekler de sunulmaktadır.

Kullanıcı tabloya rotasyonunu sağlamak istediği log dosyalarını, nereye rotasyon sağlanacağını ve yerelde mi yoksa uzak 
makinaya mı yedekleneceği bilgilerini ekleyerek konfigürasyonu sağlayabilmektedir. Uzak sunucuya yedeklenecek olan 
log dosyaları için uzak sunucu adres, port ve protokol bilgileri de girilmelidir.

![Profile](../images/profiles/rsyslogProfile.png)

![Profile](../images/profiles/rsyslogPolicy.png)

**Betik Ayarları**

Betik listesi kısmında daha önceden tanımlanmış betikler listelenir.

Betik ayar listesi kısmında özel olarak yazılmış betik dosyalarının içeriği düzenlenmektedir. Betik adı girilir. 
Ardından betiğin türü Python, Bash, Perl ve Ruby olmak üzere 4 betik çeşidinden biri seçilir. Oluşturulan betiklerden 
biri seçilir ve betik parametreleri (eğer var ise) belirtilerek görev çalıştırılır. Çalıştırılan betikler kaydet butonu 
ile Betik Listesine kaydedilebilir. Ardından istenildiği zaman politika listesine eklenir.

![Profile](../images/profiles/scriptProfile.png)

![Profile](../images/profiles/scriptPolicy.png)

**Oturum Yönetim Ayarları**

Oturum yönetimi kısmında kullanıcıların hangi zaman aralığında giriş yaptığını ve oturum süresi gibi bilgileri 
görüntüleyebiliriz. Bunun yanı sıra hangi günler oturum açabileceği, ne kadar süre aktif kalabileceği gibi politikalarda 
belirlenebilir.

![Profile](../images/profiles/sessionManagementProfile.png)

![Profile](../images/profiles/sessionManagementPolicy.png)

**Sistem Gözlemcisi Ayarları**

Metin tabanlı bilgilerin kullanıcının masaüstünde görülmesini sağlar. Şablon İçeriği ve Şablon Ayarları eksiksiz girilerek 
şablon kaydedilir. Şablon İçeriği ve Şablon Ayarları ayrı ayrı girilmelidir. Ayarlar, Şablon Ayarları sekmesinde 
"Bilgisayar Bilgisi" olarak sunulan içerik gibi olacak şekilde özelleştirilebilir.

![Profile](../images/profiles/systemMonitoringProfile.png)

![Profile](../images/profiles/systemMonitoringPolicy.png)

**USB Erişim Ayarları**

USB modülleri ve aygıtları üzerindeki izinleri düzenler.İlgili Ahenk makinesi üzerinde web kamerası, yazıcı, USB bellek 
ve fare-klavye izinlerini düzenler. İzin verme seçeneğinin seçilmesi sonucunda kullanıcı izin verilmeyen usb modülünü 
kullanamaz. İzin ver ya da verme seçeneklerinden hiçbirinin seçilmemesi durumunda ilgili usb elemanına izin verilmeyecektir. 
Bu nedenle izin için mutlaka “İzin ver” seçeneğinin seçilmiş olması gereklidir.

Bu politika da ek olarak beyazliste ve karaliste bulunmaktadır. Beyazlisteye eklenen USB aygıtlarına her koşulda izin 
verilirken karalisteye eklenen aygıtlara ise hiçbir şekilde izin verilmemektedir.

Bunu sağlamak için istenen listeye istenilen aygıtın üretici firması, modeli ve seri numarası girilir. Herhangi bir aygıt 
seçilip “Ekle” butonuna basılmasıyla liste üzerinde ekleme yapılır. Yine aynı şekilde “Sil” butonuna basılmasıyla seçilen 
kayıt silinir.


![Profile](../images/profiles/usbProfile.png)

![Profile](../images/profiles/usbPolicy.png)

