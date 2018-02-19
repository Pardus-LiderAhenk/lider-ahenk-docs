### Ahenk

Ahenk; kendine iletilen görevleri yerine getirmek, politikaları uygulamak ve sonuçlarını Lidere iletmekten sorumlu servis yazılımıdır. Ahenk yönetilen sistemlerde tam yetkili (super user) olarak çalışmaktadır. Verilen görevleri yerine getirmek, yerine getirdiği görevlerin sonuçlarını Lider’e iletmekten sorumludur.

Ahenkler  kullanıcılara  ve  sistemlere  uygulanmış  politikaları  da  ele  alıp  sistemler  üzerinde düzenlemeler  yaparlar.  Ahenk  uygulaması  çekirdek  modüllere  eklenen  eklentiler  şeklinde tasarlanmıştır. Çekirdek; içinde servis yapısı, iletişim, veritabanı, günce yönetimi ve dosya transfer modülleri  başlıca  modüllerdir. Ahenkler python ile geliştirilmiştir. Python güvenilir yapısı,  geniş kütüphane desteği nedeniyle tercih edilmiştir.

Ahenk  ile  Lider  arasındaki  iletişim  tamamen  JSON  kalıpları  şeklinde  XMPP  protokolü  ile gerçekleştirilmiştir.  Her Ahenk  sadece  Lidere  bağlı  XMPP  sunucu  ile  iletişime  geçmesi  yeterlidir.

Ahenk sistemler kendilerini XMPP sunucuya otomatik olarak kayıt edecek  şekilde tasarlanmışlardır.

Bu iletişim dilenirse SSL ile güvenlik seviyesi artırılabilir. Lider Ahenk arasındaki iletişimde kullanılan

JSON yapılarının detayları için aşağıdaki belgeyi inceleyebilirsiniz.

(http://docs.liderahenk.org/lider-ahenk-docs/general/mesaj_formatlari/)

Kimi  eklentiler, dosya transferlerine ihtiyaç duyabileceği düşünüldüğünde SSH üzerinden bir “Dosya Sunucu” ön görülmüş ve gerekli alt yapı Ahenk çekirdeği içine eklenmiştir. Örneğin; ekran görüntüsü uygulaması aldığı ekran görüntüsü resmini “Dosya Sunucu” üzerine SSH ile aktarır ve bu dosyayı ve aktardığı yolu (path) Lider’e cevap olarak döner.

Ahenkler  iletişim  alt  yapısının  sağlam  ve  ayakta  kalabilmesi  için  çeşitli  önlemler  alınmıştır.  Her kullanıcının  benzer  zamanlarda  sistemleri  kullanmaya  başlaması  gibi  nedenler  ile  büyük    politika kurallarının sürekli ve tekrartekrar aktarılması nedeniyle oluşabilecek ağ daralmalarını politikaların güncel  son  sürümlerini  kendilerinde  yedekler  (cache)  ve  değişim  olmadığı  sürece  yedekten kullanırlar.  Bu  özellik  sayesinde  Lider’e  erişim  olmadığı  durumlarda  da  son  uygulanan  politikalar geçerli olacaktır. Bu yedekleme için Ahenkler ufak birer veritabanı kullanırlar.

Ahenk sistemleri değişik özellikteki sistemlerde sistem karmaşasını artırmadan çözüm üretebilmek için bir yapı da sağlar. Örneğin; kimi ince istemci çözümlerinde (LTSP, X2Go, ...) bazı eklentilerin tümüyle farklı çalışması gerekebilmektedir. Bu durumda sadece ilgili eklentilerin ilgili görev politika kesimleri ele alınarak çözüm sağlanabilmektedir.

(http://docs.liderahenk.org/lider-ahenk-docs/developers/ahenk/ahenk_calisma_mekanigi/)

Ahenk çekirdeği ve eklentiler sistemlere ayrı ayrı paketler olarak kurulabilmektedir. Ahenk, kendisine iletilen bir göreve veya politikaya ilişkin eklenti kurulu değil ise “Dosya  Sunucu” üzerinden ilgili eklenti paketini otomatik kurabilmektedir.


#####Ahenk Yapılandırma Dosyası
    
    [BASE]
    logconfigurationfilepath = /etc/ahenk/log.conf
    dbpath = /etc/ahenk/ahenk.db

    [PLUGIN]
    pluginfolderpath = /usr/share/ahenk/plugins/
    mainmodulename = main

    [CONNECTION]
    uid = 
    password = 
    host = 
    port = 5222
    use_tls = false
    receiverjid = 
    receiverresource =
    servicename = 
    receivefileparam = /tmp/

    [SESSION]
    agreement_timeout = 30
    registration_timeout = 30
    get_policy_timeout = 30

    [MACHINE]
    type = default
    agreement = 1 
    
###BASE

**logconfigurationfilepath:**  log yapılandırma ayarlarını barındıran dosyanın yoludur. Varsayılan değer `/etc/ahenk/log.conf`'tur.
**dbpath:** Ahenk çekirdeğinin operasyonlarında kullandığı veritabanının yoludur. Varsayılan değer `/etc/ahenk/ahenk.db`'dir.

###PLUGIN

**pluginfolderpath:** Ahenk eklentilerinin bulunduğu dizin yoludur. Varsayılan değer `/usr/share/ahenk/plugins/`'dir.
**mainmodulname:** Eklentiler Ahenk' e yüklenmesinde kullanılan temel py dosyasının adıdır. Varsayılan değer `main` 'dir

###CONNECTION

**uid:**Ahenk'in kendisini kaydetmek ve XMPP Sunucusuna bağlanmak için kullandığı biricik id numarasıdır. Bu alan Ahenk tarafından doldurulacaktır.

**password:** XMPP Sunucusuna bağlanırken kullanmak üzere oluşturulan şifredir. Bu alan Ahenk tarafından doldurulacaktır.

**host:** XMPP sunucusu ip adresidir.Aktif XMPP sunucusunun geçerli ve erişilebilir bir ip adresi girilmelidir.

**port:** XMPP sunucusuna erişim için kullanılacak port numarasıdır. Port numarası varsayılan değer olarak **5222**'dir. 5222 genelde TLS'i destekleyen yapılandırmalar için  kullanılır. Bu değerin yanısıra standartlaşmış diğer port numaraları da bulunmaktadır. Bu numaraları kullanırken XMPP Sunucunuzun yapılandırma ayarlarına dikkat etmeniz gerekmektedir. Ejabberd XMPP Sunucusu için  ilgili detaya [link üzerinden](https://docs.ejabberd.im/admin/guide/security/) erişebilirsiniz.

**use_tls:** XMPP sunucusu tls bağlantıları destekliyorsa bu alan *true* olarak doldurulmalı, aksi takdirde *false* olmalı.

**receiverjid:** Lider uygulamasına XMPP Sunucu üzerinden erişmek için gerekli olan kullanıcı adıdır.

**receiverresource:** Lider uygulamasına XMPP Sunucu üzerinden erişmek için gerekli olan [kaynak](https://wiki.xmpp.org/web/Jabber_Resources) adıdır. Eğer cluster yapıda bir Lider kullnıyorsanız bu alanı boş bırakınız.

**servicename:** XMPP Sunucusunun sağladığı sanal servis adıdır. Ahenk ve Lider hesapları bu servis üzerinde tanımlı olmalıdır. Aktif XMPP sunucusunun geçerli ve erişilebilir servis adı girilmelidir.

**receivefileparam:** Ahenk'e gelen dosyaların kaydedileceği dizin yoludur.

###SESSION

**agreement_timeout:** Kullanıcı sözleşmesinin kabulu için süre kısıtının saniye türünden değeri 

**registration_timeout:** Ahenk'in Lider'e kayıt işlemi için beklenecek azami süre değeri (saniye türünden)

**get_policy_timeout:** Kullanıcı oturum açtıktan sonra, Ahenk'in Lider'den güncel politikaları almak için beklediği azami süre (saniye türünden)

###MACHINE
**type:** Yaygın olmayan makine tiplerini saklamak ya da özel durumlarda kullanmak üzere makinelere verilebilecek değiştirilebilir alan
**agreement:**  Kullanıcı sözleşmesinin sorulup sorulmadığı ile ilgili değer. Varsayılan olaran bu değer 1 olarak gelmektedir. Ahenk kurulduktan sonra agreement değerinin 1 olması kullanıcı sözleşmesinin onaya sunuculacağı anlamına gelmektedir. Bu değerin örneğin 2 olması kullanıcı sözleşmesinin onaya sunulmayacağı anlamına gelmektedir.

### Ahenk Kayıt

Ahenk paketi "repo.liderahenk.org" adresinde sunulmaktadır. Pardus bilgisayarlarda bu adres tanımlanarak ahenk paketi depodan yüklenebilmektedir. Bu deponun sisteminize tanımlanması için uçbirim(konsol)da;

	sudo wget http://repo.liderahenk.org/liderahenk-archive-keyring.asc && sudo apt-key add liderahenk-archive-keyring.asc &&  rm liderahenk-archive-keyring.asc

komutları ile "liderahenk-archive-keyring.asc" key dosyası indirilerek sisteme yüklenmelidir. Ardından;

	sudo add-apt-repository 'deb [arch=amd64] http://repo.liderahenk.org stable main'

komutu ile depo adresi "/etc/apt/sources.list" dosyasına eklenir. Bu adımı uçbirimde bir metin editörü(vi,nano,pico) yardımı ile ;

	deb [arch=amd64] http://repo.liderahenk.org stable main

satırını "/etc/apt/sources.list" dosyasına elinizle de tanımlayabilirsiniz. Daha sonra;

	sudo apt update

komutu ile güncel paket listesini alınmalıdır.

	sudo apt install ahenk

komutu ile güncel ahenk paketi kurulumu yapıldıktan sonra yapılandırma dosyasından;

    host = 
    receiverjid = 
    receiverresource = 
    servicename =

alanları girilerek yapılandırma dosyası kaydedilerek çıkılır. Örneğin ahenk yapılandırma dosyası **sudo nano /etc/ahenk/ahenk.conf  ** ile açılarak şu şekilde düzenlenirse;

    [BASE]
    logconfigurationfilepath = /etc/ahenk/log.conf
    dbpath = /etc/ahenk/ahenk.db

    [PLUGIN]
    pluginfolderpath = /usr/share/ahenk/plugins/
    mainmodulename = main

    [CONNECTION]
    uid = 
    password = 
    host =  192.168.56.1
    port = 5222
    use_tls = false
    receiverjid = lider_sunucu
    receiverresource = Smack
    servicename = im.liderahenk.org
    receivefileparam = /tmp/

    [SESSION]
    agreement_timeout = 30
    registration_timeout = 30
    get_policy_timeout = 30

    [MACHINE]
    type = default
    agreement = 1 
    
Düzenleme işlemi tamamlandıktan sonra **sudo systemctl restart ahenk.service** komutu ahenk servisi tekrar başlatılarak, ahenk'in kayıt olması sağlanır.


