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

[![Profil](../images/profiles/rsyslogProfile.png)](../images/profiles/rsyslogProfile.png)

[![Profil](../images/profiles/rsyslogPolicy.png)](../images/profiles/rsyslogPolicy.png)
<link href=/lider3.0/assets/style.css rel=stylesheet></link>
