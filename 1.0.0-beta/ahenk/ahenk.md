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

## Süreçler ve servisler,yapılandırma dosyası

Ahenk; Lider'den gelen görevleri/politikaları bulunduğu bilgisayar üzerinde çalıştırıp sonuçlarını yine Lider'e  döndüren  bir  servistir.  Yetenekleri  eklentilerle  genişletilebilir.  Sistem  üzerindeki  olaylardan veya Liderden gelen mesajlar ile iç süreçleri tetiklenir. Bu süreçleri şöyle listeleyebiliriz:

### Süreçler ve Servisler

#### Ahenk Servisinin Çalışmaya Başlaması

Ahenk  base  scripti  olan  ahenkd.py,  python  Daemon  olarak  çalışmaya  başlar.  İlk  olarak  bir  scope

oluşturur. Scope, oluşturulacak servislerin tutulduğu global bir sepet olarak düşünülebilir. Ardından

Ahenk/ Ahenk  eklentilerinin  kullanabileceği  ve  Scope’a  atılacak  servisler  oluşturulur.  Bu  servisler

şunlardır:

**Config Manager**: Yapılandırma dosyasının okunması, değiştirilmesi, yazılmasını sağlar.

**Logger**:  Farklı  seviyelerde  log  dosyasına  kayıt  düşmek  için  kullanılır.  Kaydedilen  loglar **/var/ahenk/log/ahenk.log**  dosyasına  kaydedilir.  Ahenk’in  baştan  başlatılması  ile  kayıtlar  silinmez.

Genel kayıt mesajı standardı şöyledir:  logger.debug(‘[ExecutionManager]  Politika  işlemeyebaşlandı’), logger.error(‘[PLUGINA-INIT]  A  işlemi  gerçekleştirilirken  hata  ile  karşılaşıldı.  Hata Mesajı: {0}’.format(str(e)))

**Event  Manager**: Event-Function eşleştirilmesini sağlar. Böylece uygulamanın herhangi bir yerinden fırlatılan  event  ile  önceden  tanımlanmış  event-actionlar  sayesinde  fonksiyon  tetiklenir. Ahenk  Db

**Service**: Ahenk’in kullandığı sqlite için temel veritabanı işlemlerini gerçekleştirmek için kullanılır.

**Message Manager**: Temel işleyişleri gerçekleştirmek için kullanılan json mesajlarını oluşturmak için

kullanılır. Örneğin message = scope.getMessageManager().policy_request_msg(‘user_name’)

**Plugin Manager**:  Eklentilerin Ahenk  sistemine  yüklenip  kendi  threadlerinin  başlatılmasını  sağlar. Böylece  eklentiye  gelen  bir  görev  ya  da  profil  bu  thread  içinde  işlevini  gerçekleştirebilir.  Ayrıca eklentiyi Ahenk’ten kaldırıp,  yeniden yüklemeye de izin verir. Eklentiler  yüklendikten  sonra yüklü eklentilerin init.py betikleri çalıştırılır.

**Scheduler**:  Zamanlı  görevlerin  kontrolünü  ve  çalıştırılmasını  sağlar.  Kendi  custom  cron mekanizmasını barındırır.

**Task  Manager**:  Görev  ve  politikalar  üzerinde  kaydetmek,  eklemek,  silmek  gibi  temel  işlemleri gerçekleştirir. Görevi  kaydettikten sonra çalıştırılmasını sağlar.

**Registration**: Ahenk uygulaması çalışmaya başladığında lider tarafından sağlar.  Doğrulanmamışsa  ya  da  ilk  defa  çalıştırılıyorsa  kendisini  doğrulaması  için  lider  ile  gerekli protokolü başlatır.

**ExecutionManager**:  Ahenk  ve  Lider  çekirdeği  arasında  belirlenen  protokolleri  ve  iletişim şablonlarını  tanımlar  ve  EventManager  kullanarak  bu  mesaj  şablonlarının  doğrulanmasını gerçekleştirir.

**Messager**: İletişim yöntemlerini tanımlar ve gerçekleştirir. XMPP bağlantısı açıp kapatılabilir. Bir çeşit XMPP Client’ıdır. Gelen mesajın tipinden Event Manager üzerinden  Event’i tetikler.

#### Ahenk Servisinin İlk Defa Çalışmaya Başlaması

Ahenk'in  çalışmasından  farklı  olarak  ilk  defa  çalışmada  registration  işlemi  gerçekleştirilir.  Ahenk kendisini  kaydetmesi  için,  Lider'e  içinde  üzerinde  çalıştığı  makinenin  bilgileri  ile  birlikte  bir  bilgi mesajını Anonim  olarak  gönderir  ve  kayıt  işleminin  gerçekleştirildiğine  dair  bir  cevap  bekler.  Bu işlemler  ilk  olarak  registration  servisindeki  generate_uuid  metodunda  mac  adresine  göre  uuid yaratılmasıyla  başlar. Ardından  register  metodu  üzerinden  registration parametreleri  oluşturulur. **registration_request**  metodunda istekte  bulunulur.  Son  olarakanonymous_messenger  betiği içeriğindeki AnonymousMessenger  sınıfı  üzerinden  XMPPReceiver  parametleri oluşturulur,  uzantılar  eklenir  ve  sunucuya  bağlanılır.  Beklenen  cevap yapılandırılma dosyasında belirlenmiş bekleme süresi içinde gelmezse Ahenk servisi kendini kapatır.

Eğer olumlu bir cevap dönerse Anonim bağlantı kapatılıp Lider tarafından onaylanan kalıcı hesap üzerinden iletişime devam eder. Kayıt için olumlu cevap dönmezse, makinenin sahip olduğu network adresinin  3  katı  kadar  daha  farklı  jid  bilgileriyle  registration  denemesi  yapılır.  Bunların  hiçbirinde başarılı olunmazsa Ahenk servisi kapatılır. 

#### Kullanıcının İlk Defa Ahenk Çalıştıran Bilgisayarda Oturum Açması

Ahenk  çalıştıran  bilgisayarda  bir  kullanıcı  ilk  defa  oturum  açtığında  kullanıcı  sözleşmesini  kabul etmesi beklenir. Yapılandırma dosyasında tanımlanmış bekleme süresinde olumlu cevap verilmezse kullanıcı oturumu kapatılır. Kullanıcı sözleşmeyi kabul edene kadar bu süreç devam eder. Eğer Lider yapılandırmasında  herhangi  bir  sözleşme  tanımlanmadıysa  varsayılan  Ahenk  Sözleşmesi  metni kullanıcıya  gösteirilir.  Sözleşme  metinleri  her Ahenk  servisi  başlatıldığında  Lider'den  istenilir.  Bir öncekinden farklı bir sözleşme Lider'den gönderildiğinde, kullanıcı eski sözleşmeyi kabul etmiş olsa bile yeni sözleme bir sonraki oturum açma sırasında tekrar sorulur.

#### Görev Gönderilmesi

Görev tipinde bir mesaj messenger servisine geldiğinde, recv_direct_message metodu üzerinden event manager servisi kullanılarak execution servisinde tanımlı execution manager kısmına mesaj parametresi  ile  gönderilir.  Burada  execute_task  metodu  üzerinden  task  manager  servisine gönderilen nesneye dönüştürülmüş json görevi saveTask metodu yardımıyla veritabanına kaydedilir.

Bu  sırada  görevi  çalıştıracak  eklentinin  yüklü  olup  olmadığı  plugin  manager  servisindeki process_task  metodu  üzerinden  kontrol  edilir.  Eğer  yüklü  değil  ise  Lider'e  ilgili  eklentinin  eksik olduğuna dair bir mesaj gönderilir ve eklenti kurulana kadar görev saklanır. Eklenti ile ilgili kurulum bilgileri  geldiğinde  eklenti  paketi  uzaktan  alınıp  kurulur  (execution  manager  servisi  üzerindeki install_plugin  metoduyla)    ve Ahenk  servisine  yüklenir.  Saklanan  görev  aktif  hale  getirilir.  Bu  bir zamanlı  görev  ise  scheduler  servisine  gönderilir,  değilse  plugin manager  servisine  gönderilerek çalıştırılır.

#### Kullanıcının Oturum Açması ve Politika Çalıştırılması

Kullanıcı oturum açtığında command runner servisinde, belirtilen kullanıcı adıyla birlikte oturum açıldığı bilgisi run_command_from_fifo metoduna gelir.  Kullanıcının son güncel sözleşmeyi kabul edip etmediğinin kontrolü Agreement sınıfındaki check_agreement metoduyla yapılır.

Ardından Lider'den bu kullanıcı ve çalışan makineye ait politika istenir. Eklentilerin safe ve login scriptleri varsa, plugin manager servisinden safe modu aktif hale getirilerek (process_mode) çalıştırılır (find_module). (Bu scriptlere hangi kullanıcının oturum açtığı bilgisi gönderilir)

Yapılandırma dosyasında belirtilen sürede Lider politika bilgilerini Ahenk'e göndermezse Ahenk veritabanından bu kullanıcı ve makine için çalıştırılmış en güncel politikayı çeker ve çalıştırır.

Politikaların çalıştırılması görevin çalıştırılması ile aynı mekaniği izlemektedir. Ancak bazı profil tabanlı eklentiler hem kullanıcı hem makine üzerine uygulanmış olabilir. Aynı eklentinin çalıştırabileceği 2 profile geldi ise (hem kullanıcı üzerine atanmış profil hem makine üzerine atanmış profil), makine üzerine atanmış profilin ezilebilir olup olmadığı kontrol edilir. Makine profili ezilebilir ise sadece kullanıcının profili, değilse sadece makine profili çalıştırılır.

#### Sonuçların döndürülmesi

Bir görev ya da profil çalıştırıldığında işlemin başarılı ya da başarısız olduğuna dair varsa ek bilgileri ile sonuç dönmesi beklenir. Bu sonuç, plugin servisindeki run metodu içindeki Response nesnesidir. Eklentinin döndürdüğü response nesnesi, belirlenmiş json formatına dönüştürülür.

Varsa data ve content type bilgilerine bakılır. Eğer content type, json değilse ve data da oluşturulmuş bir dosyanın md5 bilgisini barındırıyorsa bu dosya Lider'in gösterdiği uzak makinedeki dizine gönderilir ve sonuç mesajı Lider'e iletilir. Policy Status ile Task Status mesajlarının farkı Task

Status'te taskId bulunması, Policy Status'te commandExecutionId ve policyVersion bulunmasıdır.

#### Kullanıcının Oturum Kapatması

Kullanıcı oturum kapattığında command runner servisinde, belirtilen kullanıcı adıyla birlikte oturum kapatıldığı  bilgisi  run_command_from_fifo  metoduna  gelir.  Eklentilerin  safe  ve  logout  scriptleri varsa,  plugin  manager  servisinden  safe  ve  logout  modu  aktif  hale  getirilerek  (process_mode) çalıştırılır (find_module). Lider'e hangi kullanıcının oturumu kapattığına dair mesaj atılır.

#### Ahenk Servisinin Kapanması (Bilgisayarın Kapanması)

Ahenk  servisi  kapatılırken  eklentilerin  shutdown.py  betikleri  çalıştırılır.  Eğer  herhangi  bir  eklenti çalışmaya devam ediyorsa işlemini bitirmesi beklenir.

### Yapılandırma Dosyası

**[BASE]**

logconfigurationfilepath = /etc/ahenk/log.conf

dbpath = /etc/ahenk/ahenk.db

**[PLUGIN]**

pluginfolderpath = /opt/ahenk/plugins/

mainmodulename = main

**[CONNECTION]**

uid = 1111111-2222-33333-4444-555555

35/82password = aaaaa-bbbbb-ccccc-ddd-eeeeeeee

host = XXX.XXX.XXX.XXX

port = 5222

use_tls = false

receiverjid = lider_sunucu

receiverresource = Smack

servicename = im.liderahenk.org

receivefileparam = /tmp/

**[SESSION]**

agreement_timeout = 30

registration_timeout = 30

get_policy_timeout = 30

**[MACHINE]**

type = default

**[MAIL]**

smtp_host = smtp.mail_server_name.com

smtp_port = 587

from_username = username_mail

from_password = password_mail

to_address = target_mail_address@mail_server.com

36/82ayarlarını  barındıran  dosyanın  yoludur.BASE

logconfigurationfilepath: log yapılandırma

Varsayılan değer  /etc/ahenk/log.conf ‘tur.

dbpath:  Ahenk  çekirdeğinin  operasyonlarında  kullandığı  veritabanının  yoludur.  Varsayılan değer  **/etc/ahenk/ahenk.db** ‘dir.

### PLUGIN

pluginfolderpath:  Ahenk  eklentilerinin  bulunduğu  dizin  yoludur.  Varsayılan  değer

`/opt/ahenk/plugins/`'dir.

Mainmodulname:  Eklentiler Ahenk'  e  yüklenmesinde  kullanılan  temel  py dosyasının  adıdır.

Varsayılan değer `main` 'dir

### CONNECTION

**uid**: Ahenk'in kendisini kaydetmek ve XMPP Sunucusuna bağlanmak için kullandığı biricik id numarasıdır. Bu alan Ahenk tarafından doldurulacaktır.

**password**:  XMPP  Sunucusuna  bağlanırken  kullanmak  üzere  oluşturulan  şifredir.  Bu  alan Ahenk tarafından doldurulacaktır.

**host**: XMPP sunucusu ip adresidir.Aktif XMPP sunucusunun geçerli ve erişilebilir bir ip adresi girilmelidir.

**port**: XMPP sunucusuna erişim için kullanılacak port numarasıdır. Port numarası varsayılan değer  olarak  5222'dir.  5222  genelde  TLS'i  destekleyen  yapılandırmalar  için    kullanılır.  Bu değerin  yanısıra  standartlaşmış  diğer  port  numaraları  da  bulunmaktadır.  Bu  numaraları kullanırken  XMPP  Sunucunuzun  yapılandırma  ayarlarına  dikkat  etmeniz  gerekmektedir.

Ejabberd XMPP Sunucusu için  ilgili detaya link üzerinden erişebilirsiniz.

**use_tls**: XMPP sunucusu tls bağlantıları destekliyorsa bu alan true olarak doldurulmalı, aksi takdirde false olmalı.

**receiverjid**: Lider uygulamasına XMPP Sunucu üzerinden erişmek için gerekli olan kullanıcı adıdır.

**receiverresource**:  Lider  uygulamasına  XMPP  Sunucu  üzerinden  erişmek  için  gerekli  olan kaynak adıdır. Eğer cluster yapıda bir Lider kullnıyorsanız bu alanı boş bırakınız.

**servicename**: XMPP Sunucusunun sağladığı sanal servis adıdır. Ahenk ve Lider hesapları bu servis  üzerinde  tanımlı  olmalıdır.Aktif  XMPP  sunucusunun  geçerli  ve  erişilebilir  servis  adı girilmelidir.

**receivefileparam**: Ahenk'e gelen dosyaların kaydedileceği dizin yoludur.

### SESSION

**agreement_timeout**: Kullanıcı sözleşmesinin kabulu için süre kısıtının saniye türünden değeri

**registration_timeout**: Ahenk'in Lider'e kayıt işlemi için beklenecek azami süre değeri (saniye türünden)

**get_policy_timeout**:  Kullanıcı  oturum  açtıktan  sonra, Ahenk'in  Lider'den  güncel  politikaları almak için beklediği azami süre (saniye türünden)

### MACHINE

**type**:  Yaygın  olmayan  makine  tiplerini  saklamak  ya  da  özel  durumlarda  kullanmak  üzere makinelere verilebilecek değiştirilebilir alan

<table align="center">
    <tr align="center">
        <td>Lider – Ahenk Merkezi Yönetim Sistemi Altyapısının Geliştirilmesi ve İyileştirilmesi Projesi</td>
        <td rowspan=2></td>
    </tr>
    <tr align="center">
        <td>Lider Ahenk Tasarım ve Kod Analizi Dokümanı</td>
    </tr>
</table>

### MAIL

**smtp_host**: Mail servisin adresi (SMTP)

**smtp_port**: Mail servis kullanılabilir portu

**from_username** : Belirtilmiş mail sunucusunda tanımlı mail adresi

**from_password**: Yukardaki mail adresinin şifresi

**to_address**: Mailin gönderileceği hedef mail adresi