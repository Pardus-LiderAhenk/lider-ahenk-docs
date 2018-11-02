Kurulum adımları;

* Veritabanı Sunucusu(MariaDB)
* LDAP(slapd)
* XMPP(Ejabberd)
* Dosya Sunucu
* KARAF(Lider)


bileşenlerinden oluşmaktadır. Bu adımlar Pardus 17 üzerinde test edilmiştir.

##LiderAhenk Depo Adresini Ekleme

LiderAhenk kurulumu için gerekli paketler "repo.liderahenk.org" deposunda bulunmaktadır. Deponun sisteminize tanımlanması için uçbirim(konsol)da;

	sudo wget http://repo.liderahenk.org/liderahenk-archive-keyring.asc && sudo apt-key add liderahenk-archive-keyring.asc &&  rm liderahenk-archive-keyring.asc

komutları ile "liderahenk-archive-keyring.asc" key dosyası indirilerek sisteme yüklenmelidir. Ardından;

	sudo printf  "deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main" | sudo tee -a /etc/apt/sources.list

komutu ile depo adresi "/etc/apt/sources.list" dosyasına eklenir. 

```
Not: Yukarıdaki komutlarda problem yaşanırsa aşağıda anlatılan şekilde elle tanımlama yapabilirsiniz.
Uçbirimde bir metin editörü(vi,nano) yardımı ile ;

	deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main

satırını "/etc/apt/sources.list" dosyasına elinizle de tanımlayabilirsiniz.
``` 

Daha sonra;

	sudo apt update

komutu ile güncel paket listesi alınarak kurulumlara başlanmalıdır.

##Veritabanı Sunucusu Kurulum Adımları##

Veritabanı olarak  MariaDB kullanılmaktadır. Veritabanları birbirleriyle ilişkili bilgilerin depolandığı alanlardır. Lider Sunucu veritabanıdır. Bir kez kurulur.

	sudo apt install mariadb-server -y

Kurulum işlemleri aşamasında mariadb-server root parolası ekrana gelir.

![MariaDB Şifre-1](images/mariadb-sifre-1.png)

Bu örnekte root parolası **SIFRE**  olarak ayarlanmıştır. 

```
Farklı bir parola verilir ise **SIFRE** ifadesinin geçtiği yerlerde o parola tanımlanmalıdır.
```

![MariaDB Şifre-1](images/mariadb-sifre-2.png)

Aynı parola tekrar girilip **enter** tuşu ile kurulum işlemine devam edilir. Kurulum işlemi başarı ile gerçekleştikten sonra artık **mariadb-server** kurulumu tamamlanmış demektir.

###Veritabanı Oluşturma###

Kurulum başarı ile sonlandıktan sonra LiderAhenk sistemi için utf8 karakter setini kullanan **liderdb** adında bir veritabanı oluşturulması gerekiyor. Bu işlemi tamamlamak için konsol(Uçbirim) da aşağıdaki komutun çalıştırılması yeterli olacaktır;

	sudo mysql -uroot -pSIFRE -e "CREATE DATABASE liderdb DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci"
   
####Veritabanın Kontrolü####

Bunun için;

	sudo mysql -uroot -pSIFRE

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


```
Not: Eğer mariadb-server kurulu sunucu, lider kurulumu yapılacak sunucudan bağımsız bir sunucu olacak ise, mariadb konfigürasyon dosyasında (/etc/mysql/my.cnf ) yer alan bind-address parametresi satırının önüne **#** simgesi yazılmalıdır, bunun için konsolda;

	sudo nano /etc/mysql/my.cnf
    
ile açılan ekranda;

	#bind-address	 = 127.0.0.1

şeklinde bu satır kapatılabilir(yorum haline getirilir, bu konfigurason sonucunda veritabanına sadece o makineden erişim sağlanabilir) veya;

	bind-address	 = 0.0.0.0

şeklinde yazılabilir(Bu sayede servis başka sunucuların erişimine açılmış olacaktır) veya;

	bind-address	 = lider-sunucu-ip

lider-sunucu-ip adresi yazılabilir(Bu sayede servis sadece lider sunucunun erişimine açılmış olacaktır). 

Bu ayarı nasıl bir yapı kurulacaksa ona göre şekillendirilmelidir. Tek bir sunucuda tüm lider bileşenleri olacaksa bu alana lider-sunucu-ip adresi yazılarak ilerlenebilir.
```
###Veritabanı Grant Yetkileri###
Lider sunucunun veritabanı sunucusundaki veritabanına ulaşması için **liderdb** database grant yetkilerinin verilmesi gerekir. Bunun için;

	sudo mysql -uroot -pSIFRE

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

komutu ile 41 karakter hexadecimal parola üretilir. Daha sonra 

	grant all privileges on * to root@' %' identified by 'hexadecimal_karakterler' ;

komutu ile grant yetkisi verilir.

	exit

komutu ile mariadb'den  çıkılır.


	sudo systemctl restart mysql.service

Yapılan düzenlemerin geçerli olması için yukarıdaki komut çalıştırılarak  mariadb servisi yeniden başlatılır.

##LDAP Sunucu##

LDAP bileşeni için bu örnekte OpenLDAP kullanılacaktır. LiderAhenk, kullanıcı ve makine yönetimi için LDAP'a ihtiyaç duymaktadır. Kullanıcı ve makine bilgileri LDAP üzerinde tutulur ve Lider-Console (LiderAhenk arayüz uygulaması) 'dan bu ldap'a bağlanarak politika yönetimi yapılır. Bir kez kurulur.

###OpenLDAP Kurulum###

Konsolda;

	sudo apt install slapd ldap-utils -y

komutu ile kurulum başlatılır.

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

Slapd konfigure edilirken tekrar parola ister, bir önceki adımda verilen parola **SIFRE** verilir.

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

değerleri girilmiştir.

###Admin Kullanıcısının Test Edilmesi###

Yukarıda girilen bilgiler sonrasında OpenLdap'ta **admin** kullanıcısı oluşmalıdır. Kontrol için;

	sudo ldapsearch -H ldap://localhost -x -LLL -b "dc=liderahenk,dc=org" "(objectClass=simpleSecurityObject)"
    
komutu çalıştırılır. Örnek çıktı;

```
dn: cn=admin,dc=liderahenk,dc=org
objectClass: simpleSecurityObject
objectClass: organizationalRole
cn: admin
description: LDAP administrator
```
şeklinde dönmelidir. Kurulum yapılan cihaz uzakta ise **localhost** alanında OpenLdap'ın kurulu olduğu **sunucu adresi** yazılmalıdır.

###Yapılandırma Kullanıcısı(Config) İşlemleri###

LDAP sunucunuzun yapılandırma erişimi için(**config** kullanıcına) bir şifre belileyin ve bunu LDAP şifre satırı haline getirin. Bunun için;

	sudo slappasswd

Komutu ile “yapılandırma(konfigürasyon) kullanıcısı” şifresi  girmenizi isteyecektir. Bu şifre LDAP sunucunuzun yapılandırma erişimi için gerekmektedir.

	New Password: <şifrenizi giriniz>
	Re-enter new password: <şifrenizi tekrar giriniz>
	{SSHA}KopyalayacağınızŞifreSatırı

ekranda beliren şifreyi kopyalayınız ve bu şifreyi;

	sudo nano /etc/ldap/slapd.d/cn=config/olcDatabase={0}config.ldif 

dosyanın içerisindeki olcRootDN: satırının altına

	olcRootPW: {SSHA}KopyalayacağınızŞifreSatırı

şeklinde kopyalayın, OpenLDAP sunucunuzu durdurun ve bunun için aşağıdaki komutu çalıştırın.

	sudo systemctl stop slapd.service

OpenLDAP sunucunuzu aşağıdaki komut ile  yeniden başlatabilirsiniz.

	sudo systemctl start slapd

###LiderAhenk Şemalarının OpenLDAP'a Yüklenmesi###

Burada yapılandırma(konfigürasyon) yöneticisi kullanıcı adı **“cn=admin,cn=config”** dir.  Şimdi lider ahenk şemalarını ldap'a yükleyelim. Bu şemelar ldap düğümleri oluşturma adında, düğümlere 

	- parduAccount
	- pardusLiderAhenkConfig
	- pardusLider

nesne sınıflarını oluşturmayı sağlar. 

Daha sonra liderahenk.ldif dosyası konsolda 

	sudo wget https://raw.githubusercontent.com/Pardus-LiderAhenk/lider-ahenk-installer/master/src/conf/liderahenk.ldif && sudo cp liderahenk.ldif /tmp

adresinden indirilerek **/tmp** klasörü altına kopyalanır. Lider ahenk şemaları varolan ldap'a yüklenmelidir. Bunun için ;

	sudo ldapadd -x -f /tmp/liderahenk.ldif -D "cn=admin,cn=config" -w $config_admin_pwd

komutu ile ldif ldap'a yüklenir. Burada **cn=admin,cn=config** config kullanıcısı,  **$config_admin_pwd** yapılandırma(konfigürasyon) kullanıcısı şifresidir. Bir önceki adımda belirlenmiştir. Örneğin;

	sudo ldapadd -x -f /tmp/liderahenk.ldif -D "cn=admin,cn=config" -w SIFRE

şeklinde olmalıdır.

Bu dosya herhangi bir ldap arayüzü ile ldap'a bağlanarakta sisteme yüklenebilir. Bu yüklemeden sonra ldap yeniden başlatılmalıdır. Bunun için aşağıdaki komutu çalıştırın.

	sudo systemctl restart slapd.service

```
NOT : Ldap yeniden başlatılmaz ise lider nesne sınıfları ldap düğümleri oluşturulurken görüntülenmeyecektir.
```

###OpenLDAP'a Yetkili Grup Ekleme(Sudoers)###

OpenLDAP üzerinde roller oluşturarak ldap kullanıcılarına merkezi yetkilendirme yapmak için aşağıdaki adımlar uygulanmalıdır. Konsolda;

	sudo wget https://raw.githubusercontent.com/Pardus-LiderAhenk/lider-ahenk-installer/master/src/conf/sudo.ldif && sudo cp sudo.ldif /tmp

komutu ile ldif indirilir. Daha sonra;

	sudo ldapadd -f /tmp/sudo.ldif -D "cn=admin,cn=config" -w SIFRE

komutu sonrası OpenLDAP admin kullanıcı şifresi girilere ldap'a eklenir. Ardından;

	sudo nano roles.ldif

komutu ile açılan ekrana aşağıdaki bilgiler kopyalanır; 

    dn: ou=Roles,base_dn
    objectclass:organizationalunit
    objectclass:top
    ou: Roles
    description: Roles groups

bu ldif dosyasında **base_dn** alanına  yukarıda tanımlanan base_dn bilgisi girilir. 

Örnek roles.ldif:

	dn: ou=Roles,dc=liderahenk,dc=org
    objectclass:organizationalunit
    objectclass:top
    ou: Roles
    description: Roles groups

Daha sonra;

	sudo ldapadd -x -W -D "cn=admin,dc=liderahenk,dc=org" -f roles.ldif

komutu ile ldap'a Roles grubu eklenir. Bu komut sonrasında alınacak yanıt;

    Enter LDAP Password:

    adding new entry "ou=Roles,dc=liderahenk,dc=org"

şeklinde olmalıdır. Daha sonra;

	sudo systemctl restart slapd.service

komutu ile OpenLDAP yeniden başlatılır. OpenLdap'ta oluşan Roles grubu altına roller tanımlanır.

####Örnek Rol Tanımlama####

Basit bir anlatımla bu grup altına bir rol tanımlayalım. Aşağıda satırları;

    dn: cn=role1,ou=Roles,base_dn
    objectClass: sudoRole
    objectClass: top
    cn: role1
    sudoUser: pardus
    sudoHost: ALL
    sudoCommand: ALL

şeklinde örnek bir rolü;

	nano ornek_role.ldif

ile açılan ekrana yapıştırarak **role1** alanına tanımlamak istediğiniz rolün ismini, **base_dn** kısmına ldap base_dn (Örn: dc=liderahenk,dc=org) tanımlaması yapın.

Örnek ornek_role.ldif :

    dn: cn=role1,ou=Roles,dc=ldierahenk,dc=org
    objectClass: sudoRole
    objectClass: top
    cn: role1
    sudoUser: pardus
    sudoHost: ALL
    sudoCommand: ALL

Daha sonra;

	sudo ldapadd -x -W -D "cn=admin,base_dn" -f ornek_role.ldif
    
komutu ile base_dn yazılarak yukarıdaki örnek rol sisteme eklenir. Örnekler için [https://linux.die.net](https://linux.die.net/man/5/sudoers.ldap) adresini ziyaret edebilirsiniz.

###OpenLDAP Üzerinde Gerekli Düğümlerin Oluşturulması###

OpenLDAP'ta;

	* liderAhenkConfig Düğümü
	* lider_console Kullanıcısı
	* Ahenkler, Kullanıcılar Gurubu

düğümleri oluşturulmalıdır. Bunun için;

```
dn: ou=Ahenkler,base_dn
objectclass:organizationalunit
objectclass:top
ou: Ahenkler
description: pardusDeviceGroup

dn: cn=lider_console,base_dn
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
objectClass: pardusLider
objectClass: pardusAccount
cn: lider_console
sn: lider_console
uid: lider_console
userPassword: lider_console_parola
liderPrivilege: [TASK:base_dn:ALL]
liderPrivilege: [REPORT:ALL]

dn: cn=liderAhenkConfig,base_dn
objectClass: pardusLiderAhenkConfig
cn: liderAhenkConfig
liderServiceAddress: http://lider.liderahenk.org:8181
```

bilgileri;

	nano lider_dugumler.ldif

ile açılan ekrana yapıştırılır. 

Örnek lider_dugumler.ldif;

```
dn: ou=Ahenkler,dc=liderahenk,dc=org
objectclass:organizationalunit
objectclass:top
ou: Ahenkler
description: pardusDeviceGroup

dn: cn=lider_console,dc=liderahenk,dc=org
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
objectClass: pardusLider
objectClass: pardusAccount
cn: lider_console
sn: lider_console
uid: lider_console
userPassword: SIFRE
liderPrivilege: [TASK:dc=liderahenk,dc=org:ALL]
liderPrivilege: [REPORT:ALL]

dn: cn=liderAhenkConfig,dc=liderahenk,dc=org
objectClass: pardusLiderAhenkConfig
cn: liderAhenkConfig
liderServiceAddress: http://lider.liderahenk.org:8181
```

* Bu bilgilerden **'base_dn'** geçen alanlara slapd kurulumunda verilen ldap temel ağacı bilgisi girilmelidir ( Örneğin: dc=liderahenk,dc=org )

* **userPassword** değeri karşısındaki **'lider_console_parola'** yerine **lider_console** kullanıcısı için parolası tanımlanmalıdır.

* **liderServiceAddress** değeri karşısına Lider Sunucu adresi tanımlanır. Bu değer **http://lider.liderahenk.org:8181** örneğinde olduğu gibi **lider.liderahenk.org** lider sunucu adresi ve **8181** portu yazılarak tanımlanmalıdır.

Dosya kaydedilerek çıkılır. Daha sonra;

	sudo ldapadd -x -W -D "cn=admin,base_dn" -f lider_dugumler.ldif

şeklinde base_dn bilgisi yazılır, komut sonrasında **admin** parolası girilerek OpenLDAP'a eklenir.

##XMPP Sunucu##

Bütün ahenklerin bağlandığı bileşendir. Lider Sunucu ve ahenkler bu bu bileşen üzerinden haberleşirler. Bir kez kurulur. Xmpp (Ejabberd)  "Genişletilebilir Mesajlaşma ve Varlık Protokolü" olarak adlandırılır.

###Ejabberd Paketinin Kurulumu###

Komut satırında;

    sudo apt install ejabberd=16.06-0 -y

komutu ile kurulur. 

Ejabberd konfigürasyonlarının tutulduğu ejabberd.yml dosyası çok hassas bir yapıya sahip olduğundan ayarlarının bozulmaması için;

	sudo apt-mark hold ejabberd
    
ile paketinin güncellenmesi engellenmelidir. 

```
Uyarı: Ejabberd paketinin güncellenmesi gerektiğinde;
	
    sudo apt-mark unhold ejabberd
    
komutu yeterlidir.
```

###Ejabberd.yml Dosyasının Düzenlenmesi###

Kurulum sonrası konfigurasyon için konsolda;

	sudo wget https://raw.githubusercontent.com/Pardus-LiderAhenk/lider-ahenk-installer-console/master/lider-installer/conf/ejabberd.yml

adresinde  bulunan  ***ejabberd.yml***  dosyasını;

	sudo cp ejabberd.yml /opt/ejabberd-16.06/conf/

***/opt/ejabberd-16.06/conf/ejabberd.yml*** dosyasının yerine kopyalayınız. Kopyalama işleminden sonra gerekli konfigürasyon için aşağıdaki yolları izleyiniz.

Not: Bu konfigürasyon  **“ejabberd ejabberd-16.06”** versiyonuna göre **ejabberd.yml** dosyasında yapılmıştır. Farklı bir sürümde yml dosyası değiştiği için bu yml için belirlenen ayarlar değişkenlik gösterebilir. Bu nedenle sürüm ve yml dosyalarının yukarıda kurulan sürümlerle aynı olmasına dikkat ediniz.

**ejabberd.yml** dosyasını konsolda bir editör ile açınız;

	sudo nano /opt/ejabberd-16.06/conf/ejabberd.yml

Açılan dosyada aşağıdaki satırlara gerekli bilgiler tanımlanır.

	ldap_servers:
   		- "#LDAP_SERVER"

***ldap server*** farklı bir bilgisayarda ise ip, lider sunucu ile aynı bilgisayar ise ***localhost*** satırı açık kalmalıdır.

	ldap_rootdn: #LDAP_ROOT_DN"

***ldap rootdn***(Örn:"cn=admin,dc=liderahenk,dc=org") tanımlaması değiştirilir.

	ldap_password: "#LDAP_ROOT_PWD"

***ldap password*** (Örn: "SIFRE" ) admin parolası buraya tanımlanır.

	ldap_base: "#LDAP_BASE_DN"

***ldap base dn*** (Örn: "dc=liderahenk,dc=org" ) bilgisi girilir.

	
```
Not: Ejabberd.yml dosyası çok hassas bir dosyadır, herhangi boşluk veya karakter hatasında çalışmayabilir. Bu nedenle konfigurasyon dosyasında mümkün olduğu kadar varolan ayaların üzerinde değişiklik yapılarak gidilmelidir. Yeni satır eklemek veya başka bir yerden veri kopyalamak hataya neden olabilmektedir.
```

***Ejabberd.yml*** konfigürasyon dosyası düzenlendikten sonra ejabberd sunucusu aşağıdaki komutlar yardımı ile yeniden başlatılır.

	cd /opt/ejabberd-16.06/bin
    sudo ./ejabberdctl start

daha sonra

	sudo ./ejabberdctl status

komutu ile alınan çıktıda;

    The node ejabberd@localhost is started with status: started
    ejabberd 16.06 is running in that node

cevabı alınmış olmalıdır. Aksi halde yml dosyasına dönülerek ayarlar kontrol edilmelidir.

### Grup ve Kullanıcıları Oluşturma###

Bu işlemler için sırası ile aşağıdaki komutlar çalıştırılır. Komutlar ***/opt/ejabberd-16.06/bin*** dizini altında çalıştırılmalıdır.

	cd /opt/ejabberd-16.06/bin

ile ***bin*** dizini altına gidilir. ***Ejabberd Admin*** kullanıcısı oluşturmak için;

	sudo ./ejabberdctl register admin  im.liderahenk.org #ejabberd_admin_pass
    
şeklinde  #ejabberd_admin_pass (Örn: SIFRE) bilgileri girilir.
Alınan cevap;

	User admin@im.liderahenk.org successfully registered

şeklinde olmalıdır.
Admin kullanıcsından sonra birde KARAF tarafından kullanılacak lider_sunucu kullanıcısı oluşturulmalıdır. 

	sudo ./ejabberdctl register lider_sunucu im.liderahenk.org #ejabberd_admin_pass
	sudo ./ejabberdctl restart

Bu parolalar daha sonra yapılandırma ayarlarında kullanılacak olduğu için unutulmamalıdır.

###Ejabberd Roster Ayarları###

Ahenklerin  Lider sunucu ile mesajlaşması  için Ejaberd roster ayarları yapımalıdır. Bunun için;

	cd /opt/ejabberd-16.06/bin
	sudo ./ejabberdctl srg-create everyone im.liderahenk.org "everyone" this_is_everyone everyone
	sudo ./ejabberdctl srg-user-add @all@ im.liderahenk.org everyone im.liderahenk.org
    
komutları çalıştırılmalıdır. Bu komutlardaki #SERVICE_NAME alanında yukarıda belirlenen servis adı girilmelidir.
	
Xmpp sunucusunun son durumda hatasız kurulduğunun testlerinin yapılması için; 

	sudo ./ejabberdctl stop

servisi durduruyoruz.

	sudo ./ejabberdctl live

komutu ile ejabberd sunucusu çalıştırılır. Bu çalışma sırasında ejabberd herhangi bir hata alıp çıkmıyor ve açık kalıyorsa kurulumumuz doğru yapılmış demektir. Aksi durumda kurulum adımını tekrar kontrol ediniz. Bu adımdan sonra;

	Ctrl + C 

ile live çalışma modundan çılır ve;

	sudo ./ejabberdctl start

ile ejabberd sunucusu tekrar başlatılır. 

```
NOT: Ejabberd sunucusu lider ve diğer sunuculardan bağımsız ayrı bir sunucu üzerinde çalıştırılacak ise, yukarıdaki konfigürasyon örneğinde yer alan portların dışarıdan ulaşılabilir olması için gerekli firewall ayarlarının yapılması gerekmektedir.
```

##Dosya Sunucu##

Eklentilerin üzerinde tutulacağı ve mesajlaşma ile yapılamayacak boyuttaki işlemlerin (ssh şeklinde)  dosya aktarımı için kullanıcılacak sunucudur. Herhangi bir ssh ile erişimi sağlanacak bilgisayar olabilir, tercihen lider sunucuyu kullanıyoruz. Aşağıdaki paketler dosya aktarımı ve iletişim için gereklidir;

	sudo apt install sshpass rsync -y

komutu ile kurulum tamamlanır. Kurulan bu dosya sunucu bilgileri **Lider Sunucu** konfigurasyonunda gereklidir. Dosya sunucu lider sunucudan farklı bir makine olacaksa;

	mkdir /home/kullanici_adi/plugins && touch /home/kullanici_adi/sample-agreement.txt
	mkdir -p /home/kullanici_adi/agent-files/
    
komutları ile lider sunucu adımlarında kullanılacak dosya-dizinler oluşturulur. Bu dosya sunucunun ip adresi ve kullanıcı adı ve yukarıda oluşturulan dosya-dizin yolları **lider sunucu konfigürasyonunda** kullanılacaktır.

##Lider Sunucu##

Lider Sunucu, liderahenk uygulamasının merkezinde yer alır.  Xmpp ile bütün ahenklerin yönetimi bu sunucu üzerinden yapılır. Bunun yanında üzerindeki rest servisler ile Lider-Console  ( LiderAhenk arayüz uygulaması ) ile iletişim sağlayarak arayüzden yönetime olanak sağlar. Bir kez kurulur.

###Lider Sunucu Java Ayarları###

Pardus 17 sürümlerinde java kurulu olarak geldiği için bu adıma gerek yoktur. Lider Sunucu Pardus Sunucu sürümü üzerine kurulacaksa aşağıdaki adımlar uygulanmalıdır.

JAVA_HOME çevresel değişkeni sisteme tanımlanmalıdır. Bunun için;

	update-alternatives --config java

komutu ile sistemde kurulu java sürümü ve yolu görüntülenir. Eğer bir java sürümü yoksa;

	sudo apt install openjdk-8-jre

komutu ile Openjdk-8-jre sisteme yüklenir.
Not: Farklı bir sürüm kullanılacaksa java sürümü ve yolu ona göre tanımlanmalıdır.

	sudo nano ~/.bashrc

ile açılan dosyanın en atına;

	export JAVA_HOME=”/usr/lib/jvm/{sdk ev dizini}”

ve

	PATH=”$PATH:/usr/lib/jvm/{sdk ev dizini}/bin”

Burada {sdk ev dizini} ile belirtilen yere sdk ev dizini adı gelir. Bu adımdan sonra

	sudo source ~/.bashrc

ile yeni çevresel değişkenler sistem tarafından tanınmış hale gelir. (Bu adımda makinenin yeniden başlatılması önerilir. )
Bu işlemin testi için;

    echo $JAVA_HOME

ekrana oracle sdk ev dizini yolunu ekrana çıktı olarak veriyorsa işlem doğru yapılmış demektir.

###Lider Sunucu Kurulum Adımları###

Lider Sunucu;

	sudo apt install lider-server ssh -y

komutu ile depodan kurulumu sağlanır. Daha sonra -;

	sudo systemctl start lider.service
    
ile servis aktif edilir.

###Lider Sunucu Konfigurasyon Dosyası###

Bu adımda OpenLdap, XMPP ve Dosya sunucu ayarlarının lider sunucuya tanımlanması yapılır. Bu konfigurasyonlar sonucunda (veritabanı hariç) bileşenler birbirleri ile haberleşirler. Lider-sunucu yapılandırma dosyasının düzenlenmesi için;

	sudo nano /usr/share/lider-server/etc/tr.org.liderahenk.cfg

ile bu dosya düzenlenmek için açılır;

    ldap.server = ip_adresi
    ldap.port = 389
    ldap.username = cn=admin,dc=liderahenk,dc=org
    ldap.password = SIFRE
    ldap.root.dn = dc=liderahenk,dc=org

**ip_adresi** bu alana tanımlanmalıdır. Ldap **admin** şifresi ve dn bilgileri örnekte olduğu şekilde tanımlanır.

    xmpp.host = ip_adresi
    xmpp.port = 5222
    xmpp.username = lider_sunucu
    xmpp.password = SIFRE
    xmpp.resource = Smack
    xmpp.service.name = im.liderahenk.org

**ip_adresi** bu alana tanımlanmalıdır. Ejabberd da oluşturulan lider_sunucu ve host bilgileri yukarıdaki şekilde tanımlanır.
```
NOT :Lider sunucu cluster yapıda kurulacaksa xmpp.resource değeri 2 sunucuda ayrı ayrı tanımlanmalıdır. Örneğin, 1.ci sunucuya Smack, 2.ci sunucuya Smack1 olarak yazılmalıdır.
```

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

	mkdir -p /home/kullanici_adi/agent-files/

komutları ile (**kullanici_adi** dosya sunucudaki kullanıcını home dizinidir) oluşturulmalı ve yukarıdaki dosya sunucu konfigürasyonuna tanımlanmalıdır.
``` 

Daha sonra

	sudo nano /usr/share/lider-server/etc/tr.org.liderahenk.datasource.cfg

dosyasında;

    db.server = db_ip:3306
    db.database = liderdb
    db.username = root
    db.password = SIFRE

veritabanı konfigürasyonu yapılır. **db_ip** alanına veritabanı sunucusu ip bilgisi,port, veritabanına erişimi olan kullanıcı ve şifre bilgisi tanımlanır. 

```
Not: Veritabanı sunucusu ile lider sunucu aynı makinede ise ip yerine "localhost" yazılmalıdır.
```

###Lider Sunucu Servis Adımları###

Lider sunucu;

	sudo systemctl start lider.service

komutu ile yeniden başlatılarak  kurulum tamamlanır. Lider servisinin başladığından emin olmak için 

	sudo systemctl status lider.service

alternatif olarak

	ps -ef | grep lider

komutu çıktısına bakılır.  Eğer “start” durumda değilse alternatif olarak;

	sudo /etc/init.d/lider start

komutu ile karaf çalıştırılır. 

####Lider Sunucuya Bağlanma####

Lider servis olarak çalıştırılmışsa;

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

komutu çalışıtırılmalıdır. Lider sunucudan çıkmak için karaf konsolda iken;

	logout
    
komutu kullanılır.
