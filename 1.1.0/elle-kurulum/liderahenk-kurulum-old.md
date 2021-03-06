Kurulum adımları;

* Veritabanı Sunucusu(MariaDB)
* LDAP(slapd)
* XMPP(Ejabberd)
* Dosya Sunucu
* KARAF(Lider)


bileşenlerinden oluşmaktadır.

##LiderAhenk Depo

LiderAhenk kurulumu için gerekli paketler "repo.liderahenk.org" deposunda bulunmaktadır. Deponun sisteminize tanımlanması için uçbirim(konsol)da;

	sudo wget http://repo.liderahenk.org/liderahenk-archive-keyring.asc && sudo apt-key add liderahenk-archive-keyring.asc &&  rm liderahenk-archive-keyring.asc

komutları ile "liderahenk-archive-keyring.asc" key dosyası indirilerek sisteme yüklenmelidir. Ardından;

	sudo printf  "deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main" | sudo tee -a /etc/apt/sources.list

komutu ile depo adresi "/etc/apt/sources.list" dosyasına eklenir. 

```
Not: Yukarıdaki adımı uçbirimde bir metin editörü(vi,nano,pico) yardımı ile ;

	deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main

satırını "/etc/apt/sources.list" dosyasına elinizle de tanımlayabilirsiniz.
``` 

Daha sonra;

	sudo apt update

komutu ile güncel paket listesi alınarak kurulumlara başlanmalıdır.

##Veritabanı Sunucusu##

Veritabanı olarak  MariaDB kullanılmaktadır. Veritabanları birbirleriyle ilişkili bilgilerin depolandığı alanlardır. Lider Sunucu veritabanıdır. Bir kez kurulur.

	sudo apt install mariadb-server -y

Kurulum işlemleri aşamasında mariadb-server root şifresi ekrana gelir.

![MariaDB Şifre-1](images/mariadb-sifre-1.png)

Bu örnekte root şifresi **SIFRE**  olarak ayarlanmıştır.

![MariaDB Şifre-1](images/mariadb-sifre-2.png)

Aynı şifre tekrar girilip **enter** tuşu ile kurulum işlemine devam edilir. Kurulum işlemi başarı ile gerçekleştikten sonra artık **mariadb-server** kurulumu tamamlanmış demektir.

Kurulum başarı ile sonlandıktan sonra LiderAhenk sistemi için utf8 karakter setini kullanan liderdb adında bir veritabanı oluşturulması gerekiyor. Bu işlemi tamamlamak için Linux konsol da aşağıdaki komutun çalıştırılması yeterli olacaktır.

	mysql -uroot -pSIFRE -e "CREATE DATABASE liderdb DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci"

```
Not: Eğer mariadb-server kurulu sunucu, lider kurulumu yapılacak sunucudan bağımsız bir sunucu olacak ise, mariadb konfigürasyon dosyasında (/etc/mysql/my.cnf ) yer alan bind-address parametresi satırının önüne **#** simgesi yazılarak;

	#bind-address	 = 127.0.0.1

şeklinde bu satır kapatılabilir(yorum haline getirilir, bu konfigurason sonucunda veritabanına sadece o makineden erişim sağlanabilir) veya;

	bind-address	 = 0.0.0.0

şeklinde yazılabilir(Bu sayede servis başka sunucuların erişimine açılmış olacaktır) veya;

	bind-address	 = lider-sunucu-ip

lider-sunucu-ip adresi yazılabilir(Bu sayede servis sadece lider sunucunun erişimine açılmış olacaktır). 

Bu ayarı nasıl bir yapı kurulacaksa ona göre şekillendirilmelidir. Tek bir sunucuda tüm lider bileşenleri olacaksa bu alana lider-sunucu-ip adresi yazılarak ilerlenebilir.
```
Lider sunucunun veritabanı sunucusundaki veritabanına ulaşması için liderdb database grant yetkilerinin verilmesi gerekir. Bunun için;

	mysql -uroot -pSIFRE

ile giriş yapılır,

	show databases;

komutu ile veritabanlarının listesi;

    MariaDB [(none)]> show databases;
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | liderdb            |
    | mysql              |
    | performance_schema |
    +--------------------+

şeklinde görüntülenir.

	use liderdb;

ile **liderdb** veritabanı seçilir, daha sonra;

	select password('SIFRE'); 

komutu ile 41 karakter hexadecimal şifre üretilir. Daha sonra 

	grant all privileges on * to root@' %' identified by 'hexadecimal_karakterler' ;

komutu ile grant yetkisi verilir.

	exit

komutu ile mariadb'den  çıkılır.


	sudo systemctl restart mysql.service

Yapılan düzenlemerin geçerli olması için yukarıdaki komut çalıştırılarak  mariadb servisi yeniden başlatılır.

##LDAP Sunucu##

LDAP bileşeni için bu örnekte OpenLDAP kullanılacaktır. LiderAhenk, kullanıcı ve makine yönetimi için LDAP'a ihtiyaç duymaktadır. Kullanıcı ve makine bilgileri LDAP üzerinde tutulur ve Lider-Console (LiderAhenk arayüz uygulaması) 'dan bu ldap'a bağlanarak politika yönetimi yapılır. Bir kez kurulur.

	sudo apt install slapd ldap-utils

komut sonrasında paket yöneticisi slapd kurulumu için ön gereksinim ya da gereksinimler var ise kurulacak bu bileşenlerin listesini gösterir ve kurulum için **E/e** onay bekler.

**Enter** tuşu yardımı ile kurulum onaylandıktan sonra, doğrulanmamış paketler var ise tekrar bu paketlerin kurulumu için **e/E** onay ekranı gösterilir. **E** yazıp **Enter** tuşuna basarak bu işlemi de onayladıktan sonra paket yöneticisi gerekli paketleri indirme ve kurma işlemine başlar.

Slapd kurulum sırasında kullanıcıdan bir yönetici (administrator)  parolası belirlenmesini ister. Bu örnekte kullanıcı parolası **SIFRE** olarak belirlenmiştir.

![Slapd Şifre-1](images/slapd-passw-1.png)

Parola bilgisi olarak **SIFRE** girildikten sonra paket parolayı doğrulamanız için sizden tekrar girmenizi isteyecektir.

![Slapd Şifre-2](images/slapd-passw-2.png)

Yine SIFRE girdikten sonra **enter** tuşuna tıklayarak kurulumun devam etmesi sağlanır.

Paket yöneticisi slapd servisini başlattıktan sonra kurulumu tamamlar. Open LDAP temel kurulumu bu şekilde tamamlanmış olur.

Şimdi ldap dizin(veritabanı) ve dizin yöneticisi kullanıcısı oluşturmak için openldap konfigürasyonu yapalım. Bunu için;

	sudo dpkg-reconfigure slapd

komutunu çalıştırılmalıdır.

![Slapd Yapılandırma](images/slapd-yapilandirma.png)

**Hayır** seçeneği seçilerek devam edilir.

![Slapd DNS](images/slapd-dns.png)

Bu adımda temel dn adı verilir. Örneğin; **“liderahenk.org”** şeklinde alan adı girilerek **"dc=liderahenk,dc=org”** şeklinde temel DN'ye sahip dizin oluşturacaktır. **“liderahenk.org”**  şeklinde dn bu alana yazılır.

![Slapd Örgüt Adı](images/slapd-orgut-adi.png)

Bu adımda örgüt adı (organizational name) girilmelidir. Bu alana kurum adı veya birim adı girilebilir. Örneğin; **“LiderAhenk"**

![Slapd Konf Şifre-1](images/slapd-konf-pass-1.png)

Slapd konfigure edilirken tekrar şifre ister, bir önceki adımda verilen şifre **SIFRE** verilir.

![Slapd Konf Şifre-1](images/slapd-konf-pass-2.png)

Aynı şifre girilerek **Enter** tuluna basılır.

![Slapd Veritabanı](images/slapd-veritabani.png)

Yukarıdaki seçeneklerden **“HDB”** seçilerek devam edilmelidir.

![Slapd Sil](images/slapd-sil.png)

Slapd paketi tamamen kaldırıldığında veritabanının da kaldırılması için **Evet** seçeneği seçilerek devam edilmelidir.

![Slapd Veritabanı Taşıma](images/slapd-veritabani-tasi.png)

Eski veritabanı taşıma sorusuna **Hayır** cevabı verilerek devam edilir.

Bu örnekte;

 - Ldap domain adı : liderahenk.org
 - Ldap dizin(Veritabanı) adı : dc=liderahenk,dc=org
 - Ldap dizin(Veritabanı) Yönetici Kullanıcısı : cn=admin,dc=liderahenk,dc=org
 - Ldap dizin(Veritabanı) Yönetici Kullanıcısı Şifresi : SIFRE

İşlem adımlarının kontrolünü yapalım. Bunun için bir ldap arayüzüne ihtiyacımız var. Bu örnekte test işlemi için **Apache Directory Studio** kullanılacaktır.  Apache Directory Studio ldap arayüzünü https://directory.apache.org/studio/download/download-linux.html adresinden indirip kullanabilirsiniz.

Apache directory studio açıldıktan sonra sol tarafta bulunan bağlantılarım(connections) bölümüne sağ tıklayarak yeni bağlantı oluştur seçilir.

![ADS Yeni Bağlantı](images/ads-yeni-baglanti.png)

Burada ;

 - Bağlantı adı (İsteğe bağlı bir bağlantı adı)
 - Hostname (İp, sunucuda açılıyorsa localhost girilebilir)
 - Port (Ldap portu)

bilgileri girilir. 

![ADS Bağlantı Bilgileri](images/ads-baglanti-ilk.png)

Bağlantıyı kontrol et ile (Check network parameters) ile bağlantının doğruluğu kontrol edilir.

![ADS Bağlantı Doğrula](images/ads-baglanti-dogrula.png)

Bağlantı başarılı olmalıdır.

![ADS Admin Bağlantı](images/ads-baglanti-admin.png)

Ldap dizin (veritabanı) yöneticisi kullanıcı adı ve şifre(SIFRE olarak tanımlanmıştı) yazılarak, kullanıcı otantikasyonu test edilir. 

![ADS Bağlantı Son](images/ads-baglanti-dogrula-son.png)

Bağlantı başarılı sonucu vermelidir.

![ADS Base DN](images/ads-base-dn.png)

Bir sonraki adımda, Base DN ayarlaması yapılır. Buraya daha önce oluşturulan dizin(veritabanı adı girilir.) ve bitir ile bağlantı gerçekleştirilir.

LDAP sunucunuzun yapılandırma erişimi için bir şifre belileyin ve bunu LDAP şifre satırı haline getirin. Bunun için;

	sudo su
	slappasswd

Komutu ile “yapılandırma(konfigürasyon) kullanıcısı” şifresi  girmenizi isteyecektir.  Be şifre LDAP sunucunuzun yapılandırma erişimi için gerekmektedir.

	New Password: <şifrenizi giriniz>
	Re-enter new password: <şifrenizi tekrar giriniz>
	{SSHA}KopyalayacağınızŞifreSatırı

ekranda beliren şifreyi kopyalayınız ve bu şifreyi;

	sudo pico /etc/ldap/slapd.d/cn=config/olcDatabase={0}config.ldif 

dosyanın içerisindeki olcRootDN: satırının altına

	olcRootPW: {SSHA}KopyalayacağınızŞifreSatırı

şeklinde kopyalayın, OpenLDAP sunucunuzu durdurun ve bunun için aşağıdaki komutu çalıştırın.

	systemctl stop slapd.service

OpenLDAP sunucunuzu aşağıdaki komut ile  yeniden başlatabilirsiniz.

	systemctl start slapd

Burada yapılandırma(konfigürasyon) yöneticisi kullanıcı adı **“cn=admin,cn=config”** dir.  Şimdi lider ahenk şemalarını ldap'a yükleyelim. Bu şemelar ldap düğümleri oluşturma adında, düğümlere 

	- parduAccount
	- pardusLiderAhenkConfig
	- pardusLider

nesne sınıflarını oluşturmayı sağlar. 

Daha sonra liderahenk.ldif dosyası konsolda 

	sudo wget https://raw.githubusercontent.com/Pardus-LiderAhenk/lider-ahenk-installer-console/master/lider-installer/conf/liderahenk.ldif && sudo cp liderahenk.ldif /tmp

adresinden indirilerek **/tmp** klasörü altına kopyalanır. Lider ahenk şemaları varolan ldap'a yüklenmelidir. Bunun için ;

	ldapadd -x -f /tmp/liderahenk.ldif -D "cn=admin,cn=config" -w $CNCONFIGADMINPASSWD

komutu ile ldif ldap'a yüklenir. Burada **cn=admin,cn=config** config kullanıcısı,  **$CNCONFIGADMINPASSWD** yapılandırma(konfigürasyon) kullanıcısı şifresidir. Bir önceki adımda belirlenmiştir. Örneğin;

	ldapadd -x -f /tmp/liderahenk.ldif -D "cn=admin,cn=config" -w SIFRE

şeklinde olmalıdır.

Bu dosya herhangi bir ldap arayüzü ile ldap'a bağlanarakta sisteme yüklenebilir. Bu yüklemeden sonra ldap yeniden başlatılmalıdır. Bunun için aşağıdaki komutu çalıştırın.

	sudo systemctl restart slapd.service

```
NOT : Ldap yeniden başlatılmaz ise lider nesne sınıfları ldap düğümleri oluşturulurken görüntülenmeyecektir.
```

Apache Directory ile Ldap üzerinde;

	* liderAhenkConfig Düğümü
	* lider_console Kullanıcısı
	* Ahenkler, Kullanıcılar Gurubu


düğümleri oluşturulur. 

```
Not:Bu adım için ldap'a **admin** kullanıcısı ile (cn=admin,dc=liderahenk,dc=org) giriş yapılmalıdır. 
```

Temel DN (bu örnekte dc=liderahenk,dc=org) üzerine;

![ADS New Entry](images/ads-new-entry.png)

sağ tıklandıktan sonra **“new/New Entry”** adımları izlenerek oluşturulur.

![ADS New Entry Next](images/ads-new-entry-next.png)

için “Sonraki(Next)” tuşuna tıklayarak devam edilir.

![ADS liderAhenkConfig Düğümü](images/ads-liderahenk-dugum.png)

LiderAhenkConfig düğümü için “pardusLiderAhenkConfig” nesnesini seçip “Ekle(Add)” ile resimde görüldüğü üzere “Seçilmiş nesne sınıfı(Selected object classes)” bölümü eklenir.  Bir sonraki adım için “Sonraki(Next)” tuşuna tıklayarak devam edilir.

![ADS RN Add](images/ads-rn.png)

“RDN”  alanı “cn” olarak belirlenir ve “liderAhenkConfig” yazılarak devam edilir.
Bunun ardından liderServiceAddress değişkenine

![ADS liderServiceAddress](images/ads-http.png)

lider sunucu ip adresi http://x.x.x.x:8181 olarak yazılır.
Burada lider sunucu ip adresi ahenk makinelerinin ve lider sunucunun erişebileceği şekilde olmalıdır.
Not:Belirlenecek ip adresi 127.0.0.1 olmamalıdır !

Lider konsol kullanıcısı oluşturmak için Ldap temel düğümü üzerinde  sağ tıklanarak;

![ADS Lider Console](images/ads-lider_console.png)

pardusAccount, pardusLider nesne sınıfları ve

![ADS Lider Console](images/ads-inetorgperson.png)

inetOrgPerson nesne sınıfları seçilerek “Ekle(Add)” tuşuna tıklanarak “Seçilmiş nesne sınıfı(Selected object classes)” alanına eklenenir.

![ADS LiderConsole](images/ads-lider_console-2.png)

“RDN” alanı  “cn” olarak belirlenir ve “lider_console” yazılarak lider konsol kullanıcısı oluşturulur.

![Lider Console Şifre](images/lider-console-pass.png)

Lider konsol kullanıcı şifresi belirlenir. “Tamam(OK)” tuşuna tıklanarak düzenleme tamamlanır.

![Lider Console Son Durum](images/lider-console-son-durum.png)

Ldap düğümü üzerinde “lider_console” seçili iken ;

![Lider Privilege-1](images/lider-privilege-1.png)

sağ tıklanarak gelen menüde  “Yeni Öznitelik (New Attribute)” seçeneğine tıklanır ve  aşağıdaki resimde görülen “Öznitelik Tipi(Attibute type)” alanı  açılır.  Bu alanda; 

![Lider Privilege-2](images/lider-privilege-2.png)

Öznitelik tipi(Attribute type)  liderPrivilege olarak seçilir. Bu alan lider konsol kullanıcısının yetkisinin belirlendiği alandır ve değer olarak;

![Lider Privilege All](images/lider-privilege-all.png)

[TASK:dc=liderahenk,dc=org:ALL] şeklinde belirlenir. Aynı şekilde yeni bir öznitelik ekleyerek [REPORT:ALL] verilir.

Burada dc=liderahenk,dc=org yerine ilgili veritabanı temel ismi yazılır. Bu temel isim ilgili kullanıcının yönetmesini istediğimiz düğüm anlamına gelmektedir. Bu kullanıcıya veratabanı temel ismini vererek bütün ldap ağacını  yönetebilir demiş oluyoruz. ALL bütün eklentileri yönetebilir anlamına gelmektedir. True ise aktif durumda olduğunu gösterir.

Ahenkler, Kullanıcılar grublarını oluşturmak için ldap temel ismine sağ tıklayarak yeni düğüm oluştur seçeneği seçilir. Nesne sınıfını belirlemek içim “Next” tuşuna tıklayarak devam edilir.

![Ahenkler - Kullanıcılar Gurubu-1](images/ahenkler-kullanicilar.png)

Ahenkler düğümü için gelen menüde “organizationalUnit”  nesne sınıfı eklenir.

![Ahenkler - Kullanıcılar Gurubu-2](images/ahenkler-kullanicilar-2.png)

**“RDN”**: alanı  **“ou”** olarak belirlenir ve  **“Ahenkler”**  yazılarak  grup oluşturulur. Ahenkler grubu seçili iken sağ tıklanır, gelen menüde **"New Attribute"** seçillerek **"Attribute Type"** alanına **"description"** yazılır ve **"Finish"**'e tıklanır. Daha sonra bu alana **"pardusDeviceGroup"** yazılır. Bu adım **"Ahenkler"** grubu gibi oluşturulan tüm ahenk gruplarına uygulanmalıdır.

Aynı adımlar takip edilerek **"Kullanıcılar"** gurubu oluşturulur(Description tanımlaması sadece ahenk gruplarına uygulanır, kullanıcı gruplarında bu adıma gerek yoktur).

Son durumda ldap ağacı üzerinde son durum;

![Ldap Son Durum](images/ldap-son-durum.png)

şeklinde olmalıdır.

##XMPP Sunucu##

Xmpp (Ejabberd)  "Genişletilebilir Mesajlaşma ve Varlık Protokolü" olarak adlandırılır. Komut satırında;

    sudo apt install ejabberd=16.06-0 -y

komutu ile kurulur. 

```
Uyarı: Ejabberd konfigürasyonlarının tutulduğu ejabberd.yml dosyası çok hassas bir yapıya sahip olduğundan ayarlarının bozulmaması için;

	sudo apt-mark hold ejabberd
    
ile paketinin güncellenmesi engellenmelidir. Güncellenebilmesi için;
	
    sudo apt-mark unhold ejabberd
    
komutu yeterlidir.
```

Bütün ahenklerin bağlandığı bileşendir. Lider Sunucu ve ahenkler bu bu bileşen üzerinden haberleşirler. Bir kez kurulur. 

Kurulum sonrası konfigurasyon için konsolda;

	wget https://raw.githubusercontent.com/Pardus-LiderAhenk/lider-ahenk-installer-console/master/lider-installer/conf/ejabberd.yml

adresinde  bulunan  ***ejabberd.yml***  dosyasını;

	sudo cp ejabberd.yml /opt/ejabberd-16.06/conf/

***/opt/ejabberd-16.06/conf/ejabberd.yml*** dosyasının yerine kopyalayınız. Kopyalama işleminden sonra gerekli konfigürasyon için aşağıdaki yolları izleyiniz.

Not: Bu konfigürasyon  **“ejabberd ejabberd-16.06”** versiyonuna göre **ejabberd.yml** dosyasında yapılmıştır. Farklı bir sürümde yml dosyası değiştiği için bu yml için belirlenen ayarlar değişkenlik gösterebilir. Bu nedenle sürüm ve yml dosyalarının yukarıda kurulan sürümlerle aynı olmasına dikkat ediniz.

**ejabberd.yml** dosyasını konsolda bir editör ile açınız;

	sudo pico /opt/ejabberd-16.06/conf/ejabberd.yml

Açılan dosyada aşağıdaki satırlara gerekli bilgiler tanımlanır.

	hosts:
		 #	- "localhost"
 		- "#SERVICE_NAME"

***localhost*** satırı kapatılır, altına kullanılacak ***#SERVICE_NAME** (Örn: im.liderahenk.org) tanımlaması yapılır.

	ldap_servers:
   		- "#LDAP_SERVER"

***ldap server*** farklı bir bilgisayarda ise ip, lider sunucu ile aynı bilgisayar ise ***localhost*** satırı açık kalmalıdır.

	ldap_rootdn: #LDAP_ROOT_DN"

***ldap rootdn***(Örn:"cn=admin,dc=liderahenk,dc=org") tanımlaması değiştirilir.

	ldap_password: "#LDAP_ROOT_PWD"

***ldap password*** (Örn: "SIFRE" ) admin şifresi buraya tanımlanır.

	ldap_base: "#LDAP_BASE_DN"

***ldap base dn*** (Örn: "dc=liderahenk,dc=org" ) bilgisi girilir.

	host_config:
	   "#SERVICE_NAME":
     	  auth_method:
       	    - internal
       	    - ldap
       	    - anonymous

***host_config*** (Örn: "im.liderahenk.org": )satırları yukarıdaki şekilde olmalıdır. 

```
Not: Ejabberd.yml dosyası çok hassas bir dosyadır, herhangi boşluk veya karakter hatasında çalışmayabilir. Bu nedenle konfigurasyon dosyasında mümkün olduğu kadar varolan ayaların üzerinde değişiklik yapılarak gidilmelidir. Yeni satır eklemek veya başka bir yerden veri kopyalamak hataya neden olabilmektedir.
```

***Ejabberd.yml*** konfigürasyon dosyası düzenlendikten sonra ejabberd sunucusu aşağıdaki komutlar yardımı ile yeniden başlatılır.

	cd /opt/ejabberd-16.06/bin
    sudo ./ejabberdctl start

daha sonra

	sudo ./ejabberdctl status

komutu ile alınan çıktıda 

    The node ejabberd@localhost is started with status: started
    ejabberd 16.06 is running in that node

cevabı alınmış olmalıdır. Aksi halde yml dosyasına dönülerek ayarlar kontrol edilmelidir.

Ardından gerekli grup ve kullanıcıların oluşturulması işlemine gelir. Bu işlemler için sırası ile aşağıdaki komutlar çalıştırılır. Komutlar ***/opt/ejabberd-16.06/bin*** dizini altında çalıştırılmalıdır.

	cd /opt/ejabberd-16.06/bin

ile ***bin*** dizini altına gidilir. ***Ejabberd Admin*** kullanıcısı oluşturmak için;

	./ejabberdctl register admin  #SERVICE_NAME #ejabberd_admin_pass
    
şeklinde #SERVICE_NAME (Örn: im.liderahenk.org)  bilgisi ve #ejabberd_admin_pass (Örn: SIFRE) bilgileri girilir.
Alınan cevap;

	User admin@#SERVICE_NAME successfully registered

şeklinde olmalıdır.
Admin kullanıcsından sonra birde KARAF tarafından kullanılacak lider_sunucu kullanıcısı oluşturulmalıdır. 

	./ejabberdctl register lider_sunucu #SERVICE_NAME #ejabberd_admin_pass
	./ejabberdctl restart

Bu şifreler daha sonra yapılandırma ayarlarında kullanılacak olduğu için unutulmamalıdır.

Ahenklerin  Lider sunucu ile mesajlaşması  için Ejaberd roster ayarları yapımalıdır. Bunun için;

	./ejabberdctl srg-create everyone #SERVICE_NAME "everyone" this_is_everyone everyone
	./ejabberdctl srg-user-add @all@ #SERVICE_NAME everyone #SERVICE_NAME
    
komutları çalıştırılmalıdır. Bu komutlardaki #SERVICE_NAME alanında yukarıda belirlenen servis adı girilmelidir.
	
```
NOT: Ejabberd sunucusu lider ve diğer sunuculardan bağımsız ayrı bir sunucu üzerinde çalıştırılacak ise, yukarıdaki konfigürasyon örneğinde yer alan portların dışarıdan ulaşılabilir olması için gerekli firewall ayarlarının yapılması gerekmektedir.
```

Xmpp sunucusunun son durumda hatasız kurulduğunun testlerinin yapılması için; 

	./ejabberdctl stop

servisi durduruyoruz.

	./ejabberdctl live

komutu ile ejabberd sunucusu çalıştırılır. Bu çalışma sırasında ejabberd herhangi bir hata alıp çıkmıyor ve açık kalıyorsa kurulumumuz doğru yapılmış demektir. Aksi durumda kurulum adımını tekrar kontrol ediniz. Bu adımdan sonra;

	Ctrl + C 

ile live çalışma modundan çılır ve;

	./ejabberdctl start

ile ejabberd sunucusu tekrar başlatılır. 



##Dosya Sunucu##

Eklentilerin üzerinde tutulacağı ve mesajlaşma ile yapılamayacak boyuttaki işlemlerin (ssh şeklinde)  dosya aktarımı için kullanıcılacak sunucudur. Herhangi bir ssh ile erişimi sağlanacak bilgisayar olabilir, tercihen lider sunucuyu kullanıyoruz. Aşağıdaki paketler dosya aktarımı ve iletişim için gereklidir;

	sudo apt install sshpass rsync -y

komutu ile kurulum tamamlanır. Kurulan bu dosya sunucu bilgileri **Lider Sunucu** konfigurasyonunda gereklidir. Dosya sunucu lider sunucudan farklı bir makine olacaksa;

	mkdir /home/kullanici_adi/plugins && touch /home/kullanici_adi/sample-agreement.txt

	mkdir -p /home/kullanici_adi/agent-files/{0}
    
komutları ile lider sunucu adımlarında kullanılacak dosya-dizinler oluşturulur. Bu dosya sunucunun ip adresi ve kullanıcı adı ve yukarıda oluşturulan dosya-dizin yolları lider sunucu konfigürasyonunda kullanılacaktır.

##Lider Sunucu##

Lider Sunucu, liderahenk uygulamasının merkezinde yer alır.  Xmpp ile bütün ahenklerin yönetimi bu sunucu üzerinden yapılır. Bunun yanında üzerindeki rest servisler ile Lider-Console  ( LiderAhenk arayüz uygulaması ) ile iletişim sağlayarak arayüzden yönetime olanak sağlar. Bir kez kurulur.

###Lider Sunucu Java Ayarları###
```
Pardus 17 üzerinde java kurulu olarak geldiği için bu adıma gerek yoktur. Lider Sunucu Pardus Sunucu sürümü üzerine kurulacaksa aşağıdaki adımlar uygulanmalıdır.

JAVA_HOME çevresel değişkeni sisteme tanımlanmalıdır. Bunun için;

	update-alternatives --config java

komutu ile sistemde kurulu java sürümü ve yolu görüntülenir. eğerbir java sürümü yoksa;

	sudo apt install openjdk-8-jre

komutu ile Openjdk-8-jre sisteme yüklenir.
Not: Farklı bir sürüm kullanılacaksa java sürümü ve yolu ona göre tanımlanmalıdır.

	sudo pico ~/.bashrc

ile açılan dosyanın en atına;

	export JAVA_HOME=”/usr/lib/jvm/{sdk ev dizini}”

ve

	PATH=”$PATH:/usr/lib/jvm/{sdk ev dizini}/bin”

Burada {sdk ev dizini} ile belirtilen yere sdk ev dizini adı gelir. Bu adımdan sonra

	source ~/.bashrc

ile yeni çevresel değişkenler sistem tarafından tanınmış hale gelir. (Bu adımda makinenin yeniden başlatılması önerilir. )
Bu işlemin testi için;

    echo $JAVA_HOME

ekrana oracle sdk ev dizini yolunu ekrana çıktı olarak veriyorsa işlem doğru yapılmış demektir.
```

**Lider Sunucu**;

	sudo apt install lider-server

komutu ile depodan kurulumu sağlanır. Lider-sunucu yapılandırma dosyasının düzenlenmesi için;

	sudo pico /usr/share/lider-server/etc/tr.org.liderahenk.cfg

ile bu dosya düzenlenmek için açılır;

    ldap.server = ip_adresi
    ldap.port = 389
    ldap.username = cn=admin,dc=liderahenk,dc=org
    ldap.password = SIFRE!
    ldap.root.dn = dc=liderahenk,dc=org

**ip_adresi** bu alana tanımlanmalıdır. Ldap **admin** şifresi ve dn bilgileri tanımlanır.

    xmpp.host = ip_adresi
    xmpp.port = 5222
    xmpp.username = lider_sunucu
    xmpp.password = SIFRE
    xmpp.resource = Smack
    xmpp.service.name = im.liderahenk.org

**ip_adresi** bu alana tanımlanmalıdır. Ejabberd da oluşturulan lider_sunucu ve host bilgileri yukarıdaki şekilde tanımlanır.

Ahenklerin hangi ou altında görüleceği bilgisi aşağıdaki gibi tanımlanır. Bu bilgi daha önce Ldap kurulumunda oluşturulan Ahenkler gurubudur.

	agent.ldap.base.dn = ou=Ahenkler,dc=liderahenk,dc=org

Ldap base dn bilgisi tanımlanır.

    user.ldap.base.dn = dc=liderahenk,dc=org

Dosya sunucu kullanıcı adı, şifre bilgieri tanımlanır. Lider sunucudan farklı bir makine dosya sunucu olarak kullanılacaksa **ip_adresi** değeri yerine ip bilgisi tanımlanmalı ve o makinede ssh portu açık, kullanıcının erişm bilgileri doğru tanımlanmalıdır.

    file.server.protocol = ssh
    file.server.host = ip_adresi
    file.server.port = 22
    file.server.username = lider
    file.server.password = PP123456
    file.server.plugin.path = /home/kullanici_adi/plugins/ahenk-{0}_{1}_amd64.deb
    file.server.agreement.path = /home/kullanici_adi/sample-agreement.txt
    file.server.agent.file.path = /home/kullanici_adi/agent-files/{0}/

**/home/kullanici_adi/plugins**, **/home/kullanici_adi/sample-agreement.txt**, **/home/kullanici_adi/agent-files/{0}** dosyaları dosya sunucu adımlarında oluşturulan ayarlar tanımlanır.

```
Not: Lider sunucu aynı zamanda dosya sunucu olarakta kullanılacak ise konsolda;

	mkdir /home/kullanici_adi/plugins && touch /home/kullanici_adi/sample-agreement.txt

	mkdir -p /home/kullanici_adi/agent-files/{0}

komutları ile (**kullanici_adi** dosya sunucudaki kullanıcını home dizinidir) oluşturulmalı ve yukarıdaki dosya sunucu konfigürasyonuna tanımlanmalıdır.
``` 

Daha sonra

	sudo pico /usr/share/lider-server/etc/tr.org.liderahenk.datasource.cfg

dosyasında;

    db.server = localhost:3306
    db.database = liderdb
    db.username = root
    db.password = SIFRE

veritabanı konfigürasyonu yapılır. **localhost** alanına ip bilgisi,port, veritabanına erişimi olan kullanıcı ve şifre bilgisi tanımlanır.

Lider sunucu;

	systemctl start lider.service

komutu ile yeniden başlatılarak  kurulum tamamlanır. Lider servisinin başladığından emin olmak için 

	systemctl status lider.service

alternatif olarak

	ps -ef | grep lider

komutu çıktısına bakılır.  Eğer “start” durumda değilse alternatif olarak;

	/etc/init.d/lider start

komutu ile karaf çalıştırılır. Lider servis olarak çalıştırılmışsa;

	lider-client
    
ile giriş yapılır;

```
Not: Alternatif olarak;
    
    ssh -p 8101 karaf@localhost

şifre “karaf” ile de lider sunucuya giriş yapılabilir.
``` 

Hatalı bir durum kontrolu için lider konsolda;

	log:tail

yazılarak loglar izlenir. Lider servislerinin aktif olmadığını görmek için lider konsolda;

	list

komutu çalışıtırılmalıdır.
