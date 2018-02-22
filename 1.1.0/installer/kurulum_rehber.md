# Lider Ahenk Kurulum Rehberi
## Başlarken

### 1. Kurulum Uygulamasının ve Lider Console'un İndirilmesi

Kurulum uygulamasını ve Lider Arayüz yönetim aracını http://www.liderahenk.org/indir adresinden indirebilirsiniz.

> NOT: Bu uygulamalar sıkça iyileştirildiği ve yenilendiği için, elinizde bu uygulamalar olsa bile, lütfen kurulumlara başlamadan önce belirtilen adresten tekrar en güncel versiyonu indiriniz.
> Kurulum esnasında paketler Pardus 17 (depo.pardus.org.tr) depolarından alınmaktadır. Kurulumu yapmak istediğiniz dağıtımın, Pardus deposundan paket kurduğunda sorun teşkil etmemesine dikkat ediniz.

- - -

### 2. Kurulum Uygulamasının Ön Gereklilikleri

#### 2.1 SSH Paketleri

Kurulum uygulamasının çalıştığı makine ile kurulumun yapılacağı makine arasındaki bağlantı SSH ile kurulmaktadır. Bu nedenle `ssh` paketlerinin her iki tarafta da kurulu olduğundan emin olun. Kurulu değilse `sudo apt-get install -y ssh` komutu ile kurabilirsiniz.

#### 2.2 SSH Bağlantısı Root İzni
- Kolay kurulum uygulamasının genel çalışma mantığı SSH protokolü ile işlem yapılacak makineye bağlanıp gerekli komutları çalıştırmaktır.
- Linux işletim sistemlerinde paket kurma, kaldırma, konfigurasyon gibi işlemler çoğunlukla **"root"** izni ile yapılabilmektedir. Bu nedenle uygulamanın çalıştığı makineden işlem yapılacak makineye **"root"** olarak SSH bağlantısı kurulmaktadır.
- Fakat Debian tabanlı işletim sistemlerinin çoğunda varsayılan ayar olarak, **"root"** kullanıcısı ile SSH bağlantısı engellenmiştir. Bu sorunu aşmak için ilgili makinelerde SSH konfigurasyonunda PermitRootLogin satırında değişiklik yapılmalıdır. SSH'ı **"root"**a açmak için:
- SSH konfigurasyon dosyası açılır:

		sudo nano /etc/ssh/sshd_config

- - Açılan dosyada **"Authentication"** başlığı altında `PermitRootLogin without-password` ifadesinin olduğu satır `PermitRootLogin yes` olarak değiştirilir.
-  Kaydedip çıktıktan sonra SSH servisi baştan başlatılır:

		sudo service ssh restart

-  -  Daha sonra `ssh root@<IP_ADRESI>` komutuyla yapılan değişiklikler test edilebilir.

- - -

## 3. Kurulum Uygulamasının Çalıştırılması
- Sıkıştırılmış olarak indirilen kurulum uygulaması istenilen bir dizine çıkarılır.
- Oluşan **"lider-ahenk-installer-linux.gtk.x86_64"** klasörünün içine gidilir.
- Bu klasörün içinde **"lider-ahenk-installer"** isimli dosyaya çift tıklayarak çalıştırılır.
> NOT: Eğer kurulum sırasındaki log'ları görmek isterseniz komut satırından aynı dizinde içinde `./lider-ahenk-installer` komutuyla da çalıştırabilirsiniz. Çıkabilecek sorunların rahat çözülebilmesi açısından önerilir.

- - -

## 4. Kurulum Süreci
Bu rehberde Lider Ahenk'in sıfırdan kurulum süreci baştan sona kadar anlatılacaktır. Rehber ekran görüntüleriyle desteklenerek hazırlanmıştır.

> **LÜTFEN SADECE EKRAN GÖRÜNTÜLERİNE BAĞLI KALMAYIP YAZILANLARI MUTLAKA OKUYUNUZ!**

Kurulum uygulaması çalıştırıldıktan sonra açılan ana ekranda **"LİDER KUR"**'a tıklayarak Lider bileşenlerinin kurulumuna başlıyoruz.

![installer_ana_menu](images/installer_ana_menu.png)

### 4.1. Lider Bileşenlerinin Kurulumları

Lider bileşenleri sırasıyla:

* MariaDB veritabanı
* OpenLDAP sunucusu
* Ejabberd (XMPP) sunucusu
* Apache Karaf üzerinde koşan, Lider sunucusudur.

**"LİDER KUR"**'a tıkladıktan sonra açılan ilk ekranda hangi bileşenleri kurmak istediğimiz soruluyor. Bu rehberde sıfırdan kurulum yaptığımız için hepsini seçiyoruz (varsayılan olarak tüm bileşenler seçili geliyor) ve **"İleri"**'ye basıp devam ediyoruz.

![installer_bilesen_secimi](images/installer_bilesen_secimi.png)

Organizasyon sayfasında iki bilgi istenmektedir. Bunlardan biri **"Organizasyon İsmi"**, diğeri ise **"Organizasyon CN"**'dir.
**"Organizasyon İsmi"** bölümüne kurumunuzun veya merkezi yönetim sisteminiz ismini yazabilirsiniz. **"Organizasyon CN"** bölümüne ise kurumunuzun domain'ini yazın. Örneğin LiderAhenk için: liderahenk.org
 
Bu sayfada girdiğiniz bilgilere göre LDAP ve XMPP sunucularının kurulum sayfalarında organizasyonunuza uygun öneriler hazır olarak gelecektir ve ekstra bilgi girmenize gerek kalmayacaktır.

![installer_organizasyon](images/installer_organizasyon.png)

Bu rehberde örnek olarak organizasyon ismi **"LiderAhenk"**, organizasyon CN'i ise **"liderahenk.org"** olarak kullanılacaktır.
 
>NOT: Kurulum uygulamasında bazı alanların üzerinde bilgi işaretleri yer almaktadır, bunların üzerine geldiğinizde doldurmanız gereken alanla ilgili bilgiler çıkacaktır. Kurulum sırasında bunlardan da faydalanabilirsiniz.

Organizasyon ismi ve CN'ini aşağıdaki gibi giriyoruz:

![installer_organizasyon_completed](images/installer_organizasyon_completed.png)

**"İleri"** tuşuna bastıktan sonra karşımıza sunucu kurulumlarının hangi lokasyonlara yapılacağını seçeceğimiz sayfa çıkacaktır.

![installer_lokasyonlar](images/installer_lokasyonlar.png)

Bileşenleri farklı lokasyonlara kurmak istiyorsak **"Bileşen(ler) farklı bilgisayarlara kurulsun (önerilen)"** seçeneğini seçip, her birinin IP'sini ilgili alanlara yazıyoruz. Hepsi aynı lokasyona kurulacak ise önce yukarıdaki **"Bileşen(ler) tek bir bilgisayara kurulsun"** seçeneğini seçiyoruz. Eğer yerel bilgisayara kurulacaksa IP girmenize gerek kalmadan devam edebilirsiniz. Hepsi uzak bir makineye kurulacaksa ilgili seçeneği seçip IP'yi giriyoruz.

> NOT: IP alanlarının yanındaki kutucuklar SSH bağlantısında hangi port'un kullanılacağını belirtmektedir. Varsayılan SSH ayarlarından farklı bir port kullanıyorsanız doğru numarayı girmelisiniz.

Bu rehberde tüm bileşenler tek bir uzak makineye kurulacaktır. Sayfayı aşağıdaki gibi dolduruyoruz.

![installer_lokasyonlar_completed](images/installer_lokasyonlar_completed.png)

#### 4.1.1 MariaDB Veritabanı Kurulumu

Bu sayfada, MariaDB kurulacak makineye eğer kullanıcı adı ve parola ile bağlantı kurulacak ise **"Kullanıcı Adı"** bölümüne **"root"**, **"Parola"** bölümüne ise o makinenin root şifresini yazıyoruz. Eğer bir private key tanımlı ise ve özel anahtar kullanarak bağlanmak istiyorsak, **"Özel anahtar kullan"** seçeneğini seçiyoruz. Daha sonra **"Anahtar yükle"** butonuna basıp açılan ekranda kullanılacak özel anahtarı seçiyoruz. Özel anahtar oluşturulurken passphrase ile oluşturulduysa **"Passphrase (isteğe bağlı)"** alanına, anahtar oluşturulurken girilmiş olan passphrase'i giriyoruz.

Bu örnekte kullanıcı adı ve parola kullanılacaktır. Sayfayı aşağıdaki gibi dolduruyoruz.

![installer_mariadb_erisim](images/installer_mariadb_erisim.png)

**"İleri"**'ye bastığımızda aşağıdaki gibi bir ekran açılacak ve verilen bağlantı bilgileriyle kurulum yapılacak olan makineye bağlantı testi yapılacaktır.

![installer_auth_wait](images/installer_auth_wait.png)

> Not: Eğer testing sonunda başarısız olursa, kuruluma devam edilmesine izin verilmeyecektir. Böyle bir durumda girdiğiniz şifreyi, bağlanmaya çalıştığınız makinede SSH kurulu olup olmadığını ve SSH ayarlarında root kullanıcısına bağlantı izni verilip verilmediğini kontrol edin.

Test başarılı olursa yukarıdaki gibi bir ekran çıkacaktır. **"Tamam"**'a basıp devam ediyoruz.

MariaDB için kurulum yöntemini seçeceğimiz aşağıdaki  ekran karşımıza çıkacaktır.

Bu sayfada doldurmamız gereken bir **"Veritabanı root parolası"** alanı bulunmaktadır. Buraya girilen değer kurulacak olan veritabanında root kullanıcısın şifresi olacaktır.
Bu rehberde anlatım kolaylığı açısından tüm şifreler **"secret"** olarak verilecektir.

![installer_mariadb_kur_yontem_completed](images/installer_mariadb_erisim.png)

Yukarıdaki gibi şifreyi girdikten sonra **"İleri"**'ye basıyoruz ve karşımıza aşağıdaki gibi bir onay ekranı geliyor.

![installer_mariadb_onay](images/installer_mariadb_onay.png)

Bu ekranda girmemiz gereken herhangi bir bilgi yok, sadece yapılacak olan kurulum hakkında genel bir özet bilgi verilip, onay istenmektedir. Değiştirmek istediğimiz bir parametre varsa **"Geri"**'ye basarak geriye gidip değişiklik yapabiliriz, eğer yoksa **"İleri"**'ye basıp MariaDB kurulumunu başlatıyoruz.

![installer_mariadb_status](images/installer_mariadb_status.png)

Kurulumda yapılan işlemler ve tamamlanma durumu ekrandan aktarılmaktadır. Eğer bir hata ortaya çıkarsa yine bu ekranda görüntülenecektir.
Eğer bir hata oluşursa kurulum uygulamasında **"İleri"** butonu aktif olmayacak ve sadece geriye gidilmesine izin verilecektir.
Kurulum sırasında hata alındığında uygulama kapatılmadan aşağıdaki linkte anlatılanlar yapılmalıdır.

https://github.com/Pardus-LiderAhenk/lider-ahenk-installer/wiki/05.-Troubleshooting

Linkte anlatılanlar yapıldıktan sonra kurulum uygulamasına geri dönüp, hatanın alındığı ekrandan **"Geri"** butonuyla geri gidip sonra **"İleri"** tuşuna basarak tekrar kurulum sayfasına gelindiğinde kurulum tekrar başlar.

**"İleri"**'ye basarak devam ediyoruz ve LDAP kurulumuna geçiyoruz.

#### 4.1.2 OpenLDAP Kurulumu

OpenLDAP kurulumuna başlarken karşımıza erişim bilgilerini gireceğimiz sayfa çıkıyor.

![installer_ldap_erisim](images/installer_ldap_erisim.png)

Bir önceki adım olan MariaDB kurulumunda yaptığımız gibi gerekli alanları dolduruyoruz ve **"İleri"**'ye basıyoruz.
Karşımıza çıkan ekranda iki seçenek var. İlki sıfırdan yeni bir OpenLDAP kurmak, diğeri ise varolan bir LDAP'ı Lider Ahenk için konfigure etmek.
Bu rehberde tüm bileşenler sıfırdan kurulacağı için **"Yeni bir LDAP kur"** seçeneğiyle **"İleri"**'ye basarak devam ediyoruz.

![installer_ldap_kur_konf](images/installer_ldap_kur_konf.png)

Karşımıza kurulum yöntemini seçeceğimiz sayfa çıkıyor. Bu sayfada MariaDB kurulumunda yaptığımız gibi kurulum uygulaması içinde hazır olarak gelen paketi değiştirmeden (özel bir paket kurmak istemiyorsak) sadece aşağıdaki **"LDAP root parolası"** bölümünü dolduruyoruz.
**"LDAP root parolası"** bölümünde girilen değer, LDAP kurulurken oluşturulan veritabanındaki root kullanıcısının şifresi olacaktır.
Rehberde tüm şifreleri **"secret"** verdiğimiz için bu alana da **"secret"** giriyoruz ve **"İleri"**'ye basıyoruz.

![installer_ldap_kur_yontem_completed](images/installer_ldap_kur_yontem_completed.png)

Karşımıza aşağıdaki gibi bir konfigurasyon sayfası çıkıyor.

![installer_ldap_conf](images/installer_ldap_conf.png)

Bu sayfadaki konfigurasyon değerleri kurulumun başında girdiğiniz **"Organizasyon CN"** değerine göre hazır olarak getirilmiştir. Değiştirmek istediğiniz alanları tabii ki değiştirebilirsiniz. Şifre alanlarını değiştirmeniz önerilir.
Bu kurulum rehberinde tüm şifreleri **"secret"** yapacağımız için sadece **"Lider Console User Password"** alanını değiştirip **"İleri"**'ye basıyoruz.
Karşımıza aşağıdaki gibi kurulum hakkında özet bilgi veren bir sayfa geliyor. Değiştirmek istediğimiz bir parametre yoksa **"İleri"**'ye basıp onay vererek kurulumu başlatıyoruz.

![installer_ldap_onay](images/installer_ldap_onay.png)

OpenLDAP kurulum durumunu gösteren aşağıdaki gibi bir ekran gelecektir.

![installer_ldap_status](images/installer_ldap_status.png)

Eğer kurulumda herhangi bir hata alırsanız aşağıdaki linkte anlatılanları yaptıktan sonra kurulumu tekrar başlatınız.

https://github.com/Pardus-Kurumsal/lider-ahenk-installer/wiki/05.-Troubleshooting

OpenLDAP kurulumu başarılı bir şekilde sonlandığında ekran aşağıdaki gibi olacaktır.

![installer_ldap_status_completed](images/installer_ldap_status_completed.png)

OpenLDAP kurulumu bittikten sonra **"İleri"**'ye basarak bir sonraki bileşen olan Ejabberd kurulumuna geçiyoruz.

#### 4.1.3 Ejabberd Kurulumu
Ejabberd kurulumuna başlarken karşımıza erişim bilgilerini gireceğimiz sayfa çıkıyor.

![installer_xmpp_erisim](images/installer_xmpp_erisim.png)

Daha önceki bileşenlerin kurulumunda olduğu gibi gerekli alanları doldurup **"İleri"**'ye basıyoruz.
Karşımıza Ejabberd'ın kurulum yöntemini seçeceğimiz sayfa çıkıyor.

![installer_xmpp_kur_yontem](images/installer_xmpp_kur_yontem.png)

Bu rehberde hazır gelen paketlerle kurulum yaptığımız için herhangi bir şey yapmaya gerek kalmaksızın **"İleri"**'ye tıklayıp bir sonraki sayfaya geçiyoruz.
Karşımıza Ejabberd'ın konfigurasyon parametrelerini gireceğimiz sayfa çıkıyor.

![installer_xmpp_conf](images/installer_xmpp_conf.png)

Bu sayfada başlangıçta girdiğimiz **"Organizasyon CN"** değeri ve LDAP kurulumundaki parametrelere göre uygun Ejabberd konfigurasyon parametreleri hazır olarak getirilmiştir.
 Herhangi birşey değiştirmeden (özel bir isteğimiz yoksa) aşağıdaki gibi sadece boş şifre alanlarını doldurup **"İleri"**'ye basıyoruz.

![installer_xmpp_conf_completed](images/installer_xmpp_conf_completed.png)

Ejabberd kurulumu başarılı bir şekilde sonlandığında ekran aşağıdaki gibi olacaktır.

![installer_xmpp_status](images/installer_xmpp_status.png)

Eğer kurulumda herhangi bir hata alırsanız aşağıdaki linkte anlatılanları yaptıktan sonra kurulumu tekrar başlatınız.

https://github.com/Pardus-LiderAhenk/lider-ahenk-installer/wiki/05.-Troubleshooting

Ejabberd kurulumu bittikten sonra kurulum uygulaması dışında yapmanız gereken önemli bir adım aşağıda anlatılmıştır. Lütfen bu adımı atlamayınız.

> NOT:Uygulamada Ejabberd kurulumu sırasında, paket kurulumu tamamlandıktan sonra iki adet kullanıcı Ejabberd'a kaydedilmektedir. Ejabberd dağıtımındaki bir bug nedeniyle, bazen bu kullanıcılar kaydedilemese bile, Ejabberd'dan kaydedilmiş gibi sonuç gelmektedir. Bu nedenle kurulum uygulamasında Ejabberd kurulumu başarılı bir şekilde bittikten sonra Ejabberd'ın kurulu olduğu makinede aşağıdaki komutları çalıştırmanız gerekmektedir:

>Komut yapıları şu şekildedir:
>
	sudo /opt/ejabberd-16.02/bin/ejabberdctl register admin {ejabberd_servis_adı} {kaydedilecek_admin_icin_sifre}
	sudo /opt/ejabberd-16.02/bin/ejabberdctl register {lider_sunucusu_kullanıcısı_adı} {ejabberd_servis_adı} {kaydedilecek_kullanıcı_icin_sifre}

>Bu rehberdeki örnek için komutlar şu şekildedir:
>
	sudo /opt/ejabberd-16.02/bin/ejabberdctl register admin im.liderahenk.org secret
	sudo /opt/ejabberd-16.02/bin/ejabberdctl register lider_sunucu im.liderahenk.org secret

>Bu komutları çalıştırdıktan sonra **"user already registered"** veya **"user successfully registered"** gibi sonuçlar almanız gerekmektedir.
Kullanıcıların oluşup oluşmadığını, tarayıcıdan **"http://EJABBERD_IP:5280/admin"** adresinden Ejabberd web arayüzüne girip kontrol edebilirsiniz.
Tam adres bu rehberdeki örnek için **"172.16.202.32:5280/admin"**, giriş bilgileri ise kullanıcı adı ve şifre olarak **"admin@im.liderahenk.org"** ve **"secret"**'dır.

- - -

Yukarıdaki notta anlatılanları yaptıktan sonra **"İleri"**' tuşuna basarak Lider sunucu kurulumuna geçiyoruz.

#### 4.1.4 Lider Sunucu Kurulumu

Lider sunucu kurulumuna başlarken karşımıza erişim bilgilerini gireceğimiz sayfa çıkıyor.

![installer_lider_erisim](images/installer_lider_erisim.png)

Gerekli bilgileri girip **"İleri"**'ye basarak devam ediyoruz. Karşımıza aşağıdaki gibi kurulum yöntemini seçeceğimiz bir sayfa geliyor.

![installer_lider_kur_yontem](images/installer_lider_kur_yontem.png)

Lider sunucu, üzerine gerekli Lider feature'ları yüklenmiş bir Apache Karaf instance'ı olduğu için, dağıtımı TAR.GZ şeklinde olmaktadır. Lider dağıtımı kurulum uygulamasının içine gömülü olarak hazır gelmektedir. **"İleri"**'ye basıp devam ediyoruz.
Devam ettiğimizde Lider sunucu için aşağıdaki gibi bir konfigurasyon ekranıyla karşılaşıyoruz.

![installer_lider_conf_1](images/installer_lider_conf_1.png)

![installer_lider_conf_1](images/installer_lider_conf.png)

Yukarıdaki ekranlarda gösterilen tüm alanlar daha önceki bileşenlerin kurulumlarında girilen parametrelere göre otomatik olarak getirilmiştir. 

>NOT:Dosya sunucu kurulumu için herhangi bir debian dağıtımı kullanılabilir. Dosya sunucu üzerinde `sshpass` ve `rsync` paketlerinin kurulu olması ve yukarıdaki ekranda belirlenen **"Dosya Sunucusu Kullanıcı Adı"** ve **"Dosya Sunucusu Parolası"** alanlarına girilen kullanıcı-parola ile erşime açık olmalıdır. Bu değerler daha sonra **"/opt/lider-distro-1.1/etc/tr.org.liderahenk.cfg"** konfigürasyon dosyasından değiştirilebilir.

Özel bir değişiklik yapmak istemiyorsanız, bu konfigurasyon ekranında değiştirmeniz gereken bir yer yoktur. **"İleri"**'ye basıp devam ediyoruz, karşımıza aşağıdaki gibi onay ekranı geliyor.

![installer_lider_onay](images/installer_lider_onay.png)

**"İleri"**'ye basarak onaylıyoruz ve kurulumu başlatıyoruz.

Eğer kurulumda herhangi bir hata alırsanız aşağıdaki linkte anlatılanları yaptıktan sonra kurulumu tekrar başlatınız.

https://github.com/Pardus-LiderAhenk/lider-ahenk-installer/wiki/05.-Troubleshooting

Lider sunucu kurulumu başarılı bir şekilde sonlandığında ekran aşağıdaki gibi olacaktır.

![installer_lider_status_completed](images/installer_lider_status_completed.png)

#### 4.1.5 Dosya Sunucu Ayarları
Dosya sunucu kurulumu için herhangi bir debian dağıtımı kullanılabilir. Dosya sunucu üzerinde `sshpass` ve `rsync` paketlerinin kurulu olması gerekmektedir. Ayrıca Lider Kurulum esnasında belirtilen dosyalar ve dizinler bu sunucuda oluşturulmalıdır. Yani;

`/home/pardus/plugins`
> Not: **"plugins"** dizini altına https://github.com/Pardus-LiderAhenk adresinden eklentiler indirilerek kopyalanmalıdır.

`/home/pardus/agent-files/{0}` dizinleri ve; `/home/pardus/sample-agreement.txt` dosyası elle oluşturulmalıdır.

Bu değerler **"/opt/lider-distro-1.1/etc/tr.org.liderahenk.cfg"** konfigürasyon dosyasından değiştirilebilir.

Dosya sunucu ayarları da tamamlandıktan sonra, bileşenlerin hepsinin kurulumu tamamlanmıştır. Ahenk kurulumuna geçmeden önce yapılması gereken, bileşenlerin aktif ve çalışır durumda olup olmadığını kontrol edilmelidir. Yukarıda kurulmuş olan beş bileşeni kontrol ettikten sonra Ahenk kurulumuna başlayabilirsiniz.
