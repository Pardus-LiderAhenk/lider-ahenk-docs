**Politika Yönetimi**

Sistemin genelinde kullanılacak politikalar buradan tanımlanır.
Politika Listesi kısmında önceden tanımlanmış politikalar gösterilir.
Daha sonra kullanılmak üzere tanımlanan, henüz kullanımı düşünülmeyen veya 
geçici olarak iptal edilmek istenen politikalar aktif onayı kaldırılarak pasif edilebilir, güncellenebilir 
veya silinebilir.

Ayarlar kısmında seçilen politkanın altında bulunan görevler güncellenebilir veya silinebilir. 

![Politika_Listesi](../images/politikayonetimi/politikalistesi.png)

Betik Ayarları

Betik listesi kısmında daha önceden tanımlanmış betikler listelenir. 

Betik ayar listesi kısmında özel olarak yazılmış betik dosyalarının içeriği düzenlenmektedir. Betik adı girilir. 
Ardından betiğin türü Python, Bash, Perl ve Ruby olmak üzere 4 betik çeşidinden biri seçilir. 
Oluşturulan betiklerden biri seçilir ve betik parametreleri (eğer var ise) belirtilerek görev çalıştırılır.
Çalıştırılan betikler kaydet butonu ile Betik Listesine kaydedilebilir. Ardından istenildiği zaman politika
listesine eklenir.

![Betik](../images/politikayonetimi/betik.png)

İnternet Tarayıcı Ayarları

İnternet tarayıcı ayalarında internet tarayıcısının vekil sunucu, sertifika, giriş sayfası, 
sekme ayarları, gizlilik ayarları, döküman indirme gibi özelleştirmeler yapılabilir.

![Tarayıcı](../images/politikayonetimi/internet.png)

Oturum Yönetim Ayarları

Oturum yönetimi kısmında kullanıcıların hangi zaman aralığında giriş yaptığını ve oturum süresi gibi bilgileri görüntüleyebiliriz.
 Bunun yanı sıra hangi günler oturum açabileceği, ne kadar süre aktif kalabileceği gibi politikalarda belirlenebilir.

![Oturum_Yonetimi](../images/politikayonetimi/oturumyonetimi.png)

Rsyslog Ayarları

![Rsyslog](../images/politikayonetimi/rsyslog.png)

Sistem Gözlemcisi Ayar Listesi

Metin tabanlı bilgilerin kullanıcının masaüstünde görülmesini sağlar. Şablon İçeriği 
ve Şablon Ayarları eksiksiz girilerek şablon kaydedilir. 
Şablon İçeriği ve Şablon Ayarları ayrı ayrı girilmelidir. Ayarlar, Şablon Ayarları 
sekmesinde #VARSAYILAN olarak sunulan içerik gibi olacak şekilde özelleştirilebilir.

![Sistem_Gozlemci](../images/politikayonetimi/sistemgozlemcisi.png)

USB Erişim Ayarları

USB modülleri ve aygıtları üzerindeki izinleri düzenler.İlgili Ahenk makinesi üzerinde web kamerası, yazıcı, USB bellek ve fare-klavye izinlerini düzenler. 
İzin verme seçeneğinin seçilmesi sonucunda kullanıcı izin verilmeyen usb modülünü kullanamaz. İzin ver ya da verme
 seçeneklerinden hiçbirinin seçilmemesi durumunda ilgili usb elemanına izin verilmeyecektir. 
Bu nedenle izin için mutlaka "İzin ver" seçeneğinin seçilmiş olması gereklidir.

Bu politika da ek olarak beyazliste ve karaliste bulunmaktadır. Beyazlisteye eklenen USB aygıtlarına 
her koşulda izin verilirken karalisteye eklenen aygıtlara ise hiçbir şekilde izin verilmemektedir.

Bunu sağlamak için istenen listeye istenilen aygıtın üretici firması, modeli ve seri numarası girilir. Herhangi bir aygıt
seçilip "Ekle" butonuna basılmasıyla liste üzerinde ekleme yapılır. Yine aynı şekilde "Sil" butonuna basılmasıyla 
seçilen kayıt silinir.

![USB_Ayarlari](../images/politikayonetimi/usbayarlari.png)


