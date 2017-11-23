# 5. Lider Arayüz Kullanımı

Lider Arayüz (Lider Konsol ); merkezi yönetim sisteminin sistem yöneticileri tarafından kullanılan arayüz uygulamasıdır.

Sistem yöneticileri kullanıcı ve sistemler üzerindeki görev ve politikaları bu uygulama aracılığı ile gerçekleştirirler. Bu uygulama bir Eclipse RCP uygulaması olarak geliştirilmiştir. 


## Lider Arayüz Giriş
Lider Arayüz, Apache  LDAP  Directory  ağacı  üzerinden  sistemlere  ve  kullanıcılara  erişir. Ekranın sol alt köşesindeki bağlantılar penceresi ile yeni bağlantı oluşturulur.

![Lider Arayüz Yeni Bağlantı](images/la.png)

**Bağlantı adı**, **Sunucu Adı** ve **Port** bilgileri girilerek **Ağ Parametresini Kontrol Et** butonuna tıklanır. Bu işlem sonucunda eğer girilen veriler doğru ise **Bağlantı baraşıyla kuruldu.** sonucu alınır. Sonuç olumsuz ise ldap sunucu ip ve portlara erişim kontrol edilerek tekrar denenmelidir.

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

**Ahenk Bilgisi:**Sistemdeki ahenkler ip, mac adresi vb bilgiler ile listelenir. İncelenmek istenen ahenk'e tıklandığında o ahenk'in öznitelikleri  ve o ahenk üzerinden oturum açan kullanıcıların bilgilerini görüntülenir. Ahenk üzerinde kullanıcıların ne zaman oturum açıp ne zaman sonlandırdığına buradan bakılabilir.

**E-Posta Ayarları:**Herbir eklenti için sistem yöneticilerine, kullanıcılara veya e-posta guruplarına işlem ve sonucu hakkında e-posta bildirimi yapılabilir.

![Lider E-Posta Ayarları](images/eposta-ayarlari.png)

Bunu için eklenti seçilerek e-posta adresleri **Mail Gurubu Tanımla** alanına girilerek eklenir. E-posta gönderimi ** Zamanlanmış Gönder** veya **Hemen Gönder** olarak ayarlanabilir.

Bütün bu ayarlardan sonra **Mail Konfigurasyonunu Kaydet** butonuna **MUTLAKA** tıklanmalıdır.

**Çalıştırılan Görevler:**Sistem üzerinde çalışan ve tamamlanmış tüm görevler bu ekranda listelenir.

![Lider Çalıştırılan Görevler](images/calistirilan-gorevler.png)

Süreci devam eden görevler iptal edilebilir. İleri tarihli veya zamanlı çalıştırılan görevler ayrı ayrı takip edilebilir.

**Uygulanan Politikalar:**Görevlerde olduğu gibi sistemde uygulanan politikalar bu ekranda listelenir.

![Lider Uygulanan Politikalar](images/uygulanan-politikalar.png)

**Ldap Arama:** Arama kapsamı ve arama kriteri girilerek ahenk veya kullanıcı araması yapılabilir.

![Lider Ldap Arama](images/ldap-genel-arama.png)

Birden fazla arama kriteri için "+" butonuna tıklanarak ilgili alanlar girilmelidir.

**Lider'e Yüklenen Eklentiler:**

**Raporlama:** 

**USB Yetkilerini Listele:**

## Görev Uygulama

## Politika Uygulama

## Raporlama

### Rapor Şablonları

### Rapor Tanımları