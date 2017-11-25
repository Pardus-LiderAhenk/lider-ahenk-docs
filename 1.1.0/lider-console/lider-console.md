# 5. Lider Arayüz Kullanımı

Lider Arayüz (Lider Konsol ); merkezi yönetim sisteminin sistem yöneticileri tarafından kullanılan arayüz uygulamasıdır.

Sistem yöneticileri kullanıcı ve sistemler üzerindeki görev ve politikaları bu uygulama aracılığı ile gerçekleştirirler. Bu uygulama bir Eclipse RCP uygulaması olarak geliştirilmiştir. 


## Lider Arayüz Giriş
Lider Arayüz, Apache  LDAP  Directory  ağacı  üzerinden  sistemlere  ve  kullanıcılara  erişir. Ekranın sol alt köşesindeki bağlantılar penceresi ile yeni bağlantı oluşturulur.

![Lider Arayüz Yeni Bağlantı](images/la.png)

**Bağlantı adı**, **Sunucu Adı** ve **Port** bilgileri girilerek **Ağ Parametresini Kontrol Et** butonuna tıklanır. Bu işlem sonucunda eğer girilen veriler doğru ise ""**Bağlantı baraşıyla kuruldu**"" sonucu alınır. Sonuç olumsuz ise ldap sunucu ip ve portlara erişim kontrol edilerek tekrar denenmelidir.

![Lider Arayüz Yeni Bağlantı](images/la-1.png)

Daha sonra Lider Arayüzü yönetecek ldap üzerinde tanımlı ve gerekli yetkilere(Görev ve Politika oluşturma yetkileri) sahip kullanıcı bilgileri girilir.

**Kimlik Doğrula** butonu ile gililen bilgilerin doğruluğu kontrol edilebilir.

![Lider Arayüz Yeni Bağlantı-1](images/la-2.png)

**Kök DSE'den DN leri Getir** onayı kaldırılarak **Kök DN leri Getir** butonuna tıklanır. Kök Dn geldikten sonra **Finish** butonuna tıklanır.

![Lider Arayüz Yeni Bağlantı-2](images/la-3.png)

Bu işlemlerden sonra ekranın sol alt köşesinde yeni bir bağlantı oluşur.

![Lider Arayüz Yeni Bağlantı-3](images/la-4.png)

Bağlantı üzerine çitf tıklayarak giriş yapabilirsiniz.

## Lider Ahenk LDAP Ağacı

Kullanıcılar Ldap yöneticisi tarafından eklendikten sonra, ahenkler ise sisteme kayıt olduktan sonra ldap ağacında görüntülenir.

![Lider Arayüz Ldap Ağacı](images/lider-ldap-agaci.png)

### Kullanıcılar

Kullanıcılar Ldap üzerindeki grupları(varsa) ile birlikte listelenirler. Üzerine tıklayarak kullanıcılar üzerinde yürütülen görevler-politikalar uygulanabilir.

### Ahenkler

Ahenkler kullanıcılardan bağımsız bir grup yapısında olabilir. Yine grup bilgileri ldap üzerinden alınır. Ağaç üzerindeki yerini sistem yöneticisi belirler.

Aktif ahenkler yeşil, pasifler kırmızı ile renklendirilmektedir. 

### Arama

Kullanıcı veya Ahenk aranmak istendiğinde ldap düğümü üzerine tıklanarak cn,dn,uid.... bilgilerinden biri girilerek arama yapılabilir. Sonuçlar **Arama Sonuçları** başlığında listelenir.

![Lider Arayüz Ldap Arama](images/ldap-arama.png)

Ayrıca bulunan kullanıcı veya ahenk'in ldap hiyerarşisi ekranın altında listelenir.

## Kullanım Öncesi

Kullanım öncesi mail ayarları ve kullanım sonrasında kullanılabilecek raporlamalar, sonuç izleme ekranları gibi özellikler **Lider** menüsünden yapılmaktadır.

### Lider Menü

Bu menüdeki seçenekler;

![Lider Menü](images/lider-menu.png)

**Politika Tanımları:** Sistemin genelinde kullanılacak politikalar buradan tanımlanır. **Lider Yönetim Paneli**'nde bu ekrana hızlı erişim bulunmaktadır.

**Ahenk Bilgisi:** Sistemdeki ahenkler ip, mac adresi vb bilgiler ile listelenir. İncelenmek istenen ahenk'e tıklandığında o ahenk'in öznitelikleri  ve o ahenk üzerinden oturum açan kullanıcıların bilgilerini görüntülenir. Ahenk üzerinde kullanıcıların ne zaman oturum açıp ne zaman sonlandırdığına buradan bakılabilir.

**E-Posta Ayarları:** Herbir eklenti için sistem yöneticilerine, kullanıcılara veya e-posta guruplarına işlem ve sonucu hakkında e-posta bildirimi yapılabilir.

![Lider E-Posta Ayarları](images/eposta-ayarlari.png)

Bunu için eklenti seçilerek e-posta adresleri **Mail Gurubu Tanımla** alanına girilerek eklenir. E-posta gönderimi **Zamanlanmış Gönder** veya **Hemen Gönder** olarak ayarlanabilir.

Bütün bu ayarlardan sonra **Mail Konfigurasyonunu Kaydet** butonuna **MUTLAKA** tıklanmalıdır.

**Çalıştırılan Görevler:** Sistem üzerinde çalışan ve tamamlanmış tüm görevler bu ekranda listelenir.

![Lider Çalıştırılan Görevler](images/calistirilan-gorevler.png)

Süreci devam eden görevler iptal edilebilir. İleri tarihli veya zamanlı çalıştırılan görevler ayrı ayrı takip edilebilir.

**Uygulanan Politikalar:** Görevlerde olduğu gibi sistemde uygulanan politikalar bu ekranda listelenir.

![Lider Uygulanan Politikalar](images/uygulanan-politikalar.png)

**Ldap Arama:** Arama kapsamı ve arama kriteri girilerek ahenk veya kullanıcı araması yapılabilir.

![Lider Ldap Arama](images/ldap-genel-arama.png)

Birden fazla arama kriteri için "+" butonuna tıklanarak ilgili alanlar girilmelidir.

**Lider'e Yüklenen Eklentiler:** Lider üzerinde yüklü olan eklentiler bu ekrandan incelenebilir.

![Lider Ldap Arama](images/yuklu-gelen-eklentiler.png)

Eklentiler için versiyon kontrolu, kullanıcı-makine odaklı ve politika-görev özellikleri bu ekrandan takip edebilirsiniz.

**Raporlama:** İleride [Raporlama](#Raporlama) başlığında detaylı bir şekilde değinilmiştir.


**USB Yetkilerini Listele:** *USB Yetkisi Ver/Kaldır* eklentisi ile verilen yetki ver/kaldır görevlerinin sonuçları bu ekrandan izlenir.

![Lider USB Yetkileri](images/usb-yetkileri.png)

Yetki verilenler veya yetkisi alınan kullanıcılar ayrı ayrı süzülebilir. Kullanıcın yetkisini değiştirmek için *USB Yetkisi Ver/Kaldır* eklentisi kullanılmalıdır, bu ekranda sadece görüntüleme yapılır.

**Servis İzleme Listesi:** *Servis İzle ve Yönet* eklentisi çalıştırıldıktan sonra oluşan geri bildirimler bu ekranda istelenir.

![Lider Servis İzleme Listesi](images/servis-izleme-listesi.png)

Herhangi bir izeleme görevin üzerine çift tıklandığında görevin sonuçları görüntülenir.

**Servis Raporu:** Servis genel raporlama ekranıdır. Arama kriterleri girilmediği taktirde tüm ahenkler üzerinde çalışan servisleri aktif-pasif durumları ile birlikte getirir.

![Lider Servis Raporu](images/servis-raporu.png)

Örneğin servis durumu "Stopped" olan servisler süzülebilir. Veya ssh, cups, cron vs servisin hangi ahenkler üzerinde durduğu bilgisine buradan ulaşılabilir.

![Lider Servis Raporu Stop](images/servis-raporu-stop.png)

Tüm ahenkler üzerinde çalışan bir servisin durumu hakkında bilgi alınabilir.

**Betik Tanımları:** Sistem genelinde kullanılan betikleri bu ekrandan tanımlanır. **Bash, Python, Perl, Ruby** betikleri yazılabilir.

![Lider Ldap Betik Tanımları](images/betik-tanimlari.png)

Burada yazılan betikler görev eklentisi olarak uygulanmaktadır.

**Paket Yöneticisi Görevler Ekranı:** Paket Kur/Kaldır görevi sonuçları bu ekranda listelenir.

![Lider Ldap Paket Yöneticisi](images/paket-yonetici-gorev-ekrani.png)

Görevin çalıştırıldığı ahenkler ve başarı durumu, gönderilen görevin üzerine çift tıklayarak veya **İncele** butonuna tıklayarak görülebilir.

**Disk Kota Politikası Ekranı:** Kullanıcı, grup veya birimin tamamı veya birkaç karakteri girilerek arama yapılır. Bulunan kullanıcı/gurup/birim üzerine tıklandığında o kullanıcıya uygulanan politika listelenir.

![Lider Disk Kota](images/disk-kota-politikasi-ekrani.png)

Listelenen politikaların üzerine çift tıklanılarak ceya **İncele** butonuna tıklanılarak uygulanan DN'ler ve hata/başarı oranları görülebilir.

**Yedekleme Görevleri Ekranı:** Yedekleme görevleri çalıştırıldıktan sonra (yedekleme uzun sürebilir) bu ekrandan takip edilebilir.

![Lider Yedekleme Görevleri](images/yedekleme-gorevleri-ekrani.png)

Uygulanan ahenklere ait yedekleme sonuçları, anlık olarak izlenebilir. Tamamlanan veya devam edenlerin tamamlanma oranları, transfer edilen dosya boyutu, ulaşmayan ahenkler bu ekrandan görülebilir.

![Lider ](images/yedekeme-sonuc.png)

**Yedekleme Sunucu Konfigurasyonu:** *Dizin Yedekle* görevi uygulanırken girilen yedekleme ayarları bu ekrandan da düzenlenebilir.

![Lider Yedekelem Sunucusu](images/yedekleme-sunucusu-konfiugrasyonu.png)

Değiştirilen ayarlar sistemin genelinde aktif olur.

## Görev Uygulama

*Lider Ahenk LDAP Ağacı* üzerindeki kullanıcı, grup ve ahenkler üzerine anlık olarak gönderilmek istenen işlemler **görev** olarak adlandırılır.

Kullanıcı ve kullanıcı grupları üzerine uygulanacak görevler ile ahenkler üzerine uygulanan görevler farklılık göstermektedir. Lider Arayüz bu farklılıkları kullanıcıya hissettirmeden yapmakta, kullanıcıya uygulanacak eklenti ahenkler üzerinde aktif olmamaktadır.

Fakat bazı eklentiler hem görev hemde politika olarak uygulanabilmektedir.

Görev uygulama adımları;

 * *Lider Ahenk LDAP Ağacı* üzerinden kullanıcı/grup seçimi yapılır
 * *Lider Yönetim Paneli*  üzerinden uygulanmak istenen görev eklentisi butonuna basılır
 * Eklenti türüne göre gerekli adımlar takip edilir.

Herbir eklentinin uygulanış biçimi farklı olabilir. Bu nedenle **Lider Ahenk Dokümanlar** adresinden [Eklentiler](http://docs.liderahenk.org/) başlığı altından kullanılmak istenen eklenti incelenebilir.

## Politika Uygulama

Herbir politika en az bir profilden oluşmaktadır. Profiller topluluğu ise politikaları oluşturur.

![Lider Ldap Arama](images/politika.png)

*+* simgesi ile yeni bir politika oluşturulur. Kalem butonu ile seçili politika üzerinde profil tanımlama ekranı açılır.

![Lider Ldap Arama](images/profil.png)

Profiller için **Lider Ahenk Dokümanlar** adresinden [Eklentiler](http://docs.liderahenk.org/) başlığı altından kullanılmak istenen eklenti incelenebilir. Bu ekranda gelen eklentiler sistemde yüklü olan ve profil olarak oluşturulup, politika şeklinde uygulanabilen eklentilerdir.

Örneğin **Masaüstü Arkaplan** eklentisi bir görev olarak uygulanabildiği gibi kullanıcı nerede oturum açarsa açsın karşısına çıkacak bir profil olarak da buradan tanımlanbilir. **Profiller uygulandıktan sonra kullanıcı oturumlarının kapatılıp açılması gereklidir.**

Daha sonra kullanılmak üzere tanımlanan,  henüz kullanımı düşünülmeyen veya geçici olarak iptal edilmek istenen politikalar **Aktif** onayı kaldırılarak pasif edilebilir.

Tanımlanmış profiller açılır menüden değiştirilebilir, eklenebilir, düzenlenebilir ve silinebilir durumdadır. Aktif-Pasif edilebilme tüm profiller için geçerlidir.


## Raporlama

### Rapor Şablonları

### Rapor Tanımları