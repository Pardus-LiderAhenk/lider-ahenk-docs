# 5. Lider Console

Lider Konsol; yönetim sisteminin sistem yöneticileri tarafından kullanılan arayüz uygulamasıdır.

Sistem yöneticileri kullanıcı ve sistemler üzerindeki görev ve politikaları bu uygulama aracılığı ile gerçekleştirirler. Bu uygulama bir Eclipse RCP uygulaması olarak geliştirilmiştir. 

Lider Konsol, Apache  LDAP  Directory  ağacı  üzerinden  sistemlere  ve  kullanıcılara  erişir.  Lider  Konsol uygulaması yönetimsel tüm iletişimi HTTP(s) protokolü ile REST servisler aracılığı ile  Lider üzerinden gerçekleştirmektedir.

Lider Konsol uygulaması da diğer LiderAhenk uygulamaları gibi bir çok modülden oluşan bir çekirdek ve her geliştirilen eklenti için bileşenlerden (bundle) oluşur.

Lider  Konsol  uygulaması  XMPP sunucudan hangi  sistemlerin  çevrimiçi  (online)  olduğu bilgisini kontrol etmek için bağlanmaktadır. Ayrıca; LDAP ağacı üzerinden işlem yaptığın LDAP istemcisidir. LDAP işlemleri Apache Directory üzerinden gerçekleştirilir. Lider ile temel iletişimi JSON  nesneler  yardımıyla  REST  servisler  üzerinden gerçekleştirilir. Ancak,  Lider  sisteminin kullandığı Veritabanı sistemine doğrudan bir iletişimi kesinlikle yoktur. Lider veritabanı sadece ve  sadece  Lider  Sunucusu  (Apache  Karaf)  tarafından  sorgulanabilir  ve  erişilebilir  olması yeterlidir.

Lider Konsol uygulaması üzerinden kullanıcı ve sistemlere görevler gönderilip,  bu görevlere ilişkin  sonuçlar  toplanabilir.  Bu  sonuçlar  merkezi  veritabanında  saklanır,  istenildiğinde gruplama,  raporlama  amaçları  ile  sorgulanabilirler.  

Sistemde  yapılan  tüm  işlemlerin  bir  izi muhakkak  veritabanı  üzerinde  tutulmaktadır.  Bazı  eklentiler    tasarımları  gereği  kendilerine özgü  verileri  de  veritabanında  ayrıca  tutmasına  olanak  sağlanmıştır.  Lider  Konsol  aralığı  ile sadece  görevler  değil  kullanıcı  yönetimine  ilişkin  politikalar  da  yönetilir.  Örneğin;  kullanıcı gruplarının  masaüstü  mesajları  ve  ekran  koruyucu  ayarları  yapılabilir,  tarayıcı  ev  sayfaları değiştirilebilir. Tüm kullanıcı profilleri ve profil tanımları, hangi kullanıcılara uygulandıkları da veritabanı üzerinde saklanır.

Bu  saklanan  veriler  üzeriden  dinamik  raporlama  bileşeni  ile  farklı  gereksinimlere  ilişkin raporlamalar tasarlanıp, sisteme eklenir  ve  çalıştırılır. Lider Ahenk sisteminin geneline ilişkin raporlar tasarlanabileceği gibi kimi eklentilere özgü raporlar da tasarlanabilir. Lider sistemi ilk kurulum  ile  temel  raporlama  ihtiyaçlarına  yönelik  kimi  rapor  tanımlarını  kullanıcı  için  hazır şekilde sunar. Her eklenti kendi ihtiyaçları çerçevesinde yeni rapor şablonlarını otomatik olarak sisteme ekleyebilir.

## Task ve Policy İçin GUI Oluşturma Adımları

lider-console-EKLENTI_ISMI, lider-Eclipse RCP IDE’sini açınız. Menüden File -> Import -> Maven -> Existing Maven Projects seçeneklerini  takip  ederek  açılan  pencerede  kendi  eklentinizin  bulunduğu  dizini  seçin  ve Finish  butonuna  tıklayın. Artık  Lider,  Lider-Console  ve Ahenk  eklentiniz  Eclipse’e  eklenmiş durumdadır.

**Eklenti  geliştirme  üç  aşamadan  oluşmaktadır:**

EKLENTI_ISMI ve ahenk-EKLENTI_ISMI lider-console-EKLENTI_ISMI:  Burada  eklentinizin  Lider-Console  tarafındaki  bileşenlerini diyaloglar ve diğer SWT bileşenleri yardımıyla düzenleyebilir, kullanıcıdan gerekli inputları bu bileşenler yardımıyla alabilirsiniz. Bunun için src/ klasörü altında bulunan, tr.org.liderahenk.EKLENTI_ISMI.constants  paketinin  altına  eklentide  kullanılan  sabitlerin bulunduğu  sınıflar  tanımlanmalıdır.  (Archetype  ile  hali  hazırda  örnek  bir  constant  sınıfı  bu paketin altında gelmektedir.)

tr.org.liderahenk.EKLENTI_ISMI.dialogs  paketinin  altına  eklentide  kullanılan  ekranların betimlendiği sınıflar tanımlanmalıdır. Eğer eklenti bir politika eklentisi ise açılacak olan profil ekranı üzerindeki değişiklikler eklentiye ait  ProfileDialog sınıfı üzerinden yapılır. Eğer eklenti bir görev eklentisi ise TaskDialog sınıfı kullanılır.

ProfileDialog sınıfında bulunan metodlarda aşağıdaki işlemler gerçekleştirilir.

**init:** Başlangıçta yapılacak işlemler burada tanımlanır.

**createDialogArea:** Profil ekranının bütün SWT bileşenleriyle oluşturulduğu metodburasıdır.

**getProfileData:**  Ekran  üzerindeki  verilerin  bir  Map’e  eklendiği  yerdir.  Bu  metodsayesinde veriler Ahenk’e kadar ulaştırılacaktır.

**validateBeforeSave:**  Profil  kaydedilmeden  önceki  son  kontroller  bu  metodüzerinden  yapılmaktadır.  Örneğin  doldurulması  zorunlu  bir Text  varsa Text’in  boşolma durumundaki ValidationException buradan fırlatılır.

TaskDialog sınıfında bulunan metodlarda ise aşağıdaki işlemler gerçekleştirilir.

**createTitle:** Dialog ekranının başlığı burada belirtilir.

**createTaskDialogArea:** Görev ekranının bütün  SWT bileşenleriyle oluşturulduğumetod burasıdır.

**validateBeforeExecution:** Görev çalıştırılmadan önceki son kontroller bu metodüzerinden  yapılmaktadır.  Örneğin  doldurulması  zorunlu  bir Text  varsa Text’in  boşolma durumundaki ValidationException buradan fırlatılır.

**getParameterMap:** Ekran üzerindeki verilerin bir Map’e eklendiği yerdir. Bu metodsayesinde veriler Ahenk’e kadar ulaştırılacaktır.

**getCommandId:** Çalıştırılacak göreve ait id bilgisi bu metod üzerinden döndürülür.getPluginName: Çalıştırılacak görevin ismi bu metod üzerinden döndürülür.

**getPluginVersion:**  Çalıştırılacak  görevin  versiyonu  bu  metod  üzerindendöndürülür. tr.org.liderahenk.EKLENTI_ISMI.handlers  paketinin  altında  dialog  paketi  altındaki  dialog sınıflarını ele alan ve bu dialog ekranlarını açan sınıflar bulunmaktadır. Buradaki ProfileHandler eklentinin profil ekranını ele alırken TaskHandler ise eklentinin görev ekranını ele alır. tr.org.liderahenk.EKLENTI_ISMI.i18n paketi altında ise halihazırda bir sınıf ve iki tane metin belgesi  bulunmaktadır.  Bu  metin  belgelerinden  messages_tr.properties  belgesine  eklentide kullanılan string ifadelerin Türkçe karşılıkları yazılırken messages.properties belgesine ise bu ifadelerin İngilizce karşılıkları yazılmaktadır.

## Task ve Policy için Lider-Console Süreci

Eklentiler  Lider-Console  tarafından  bağımsız  olarak  oluşturulmaktadır.  Bu  nedenle  sadece Lider  sunucusuna  istekte  bulunurken  ve  görev  bildirimlerinin  dinlenmesinde  bazı  sınıflardan faydalanılır.  Lider  sunucusuna  görev,  profil  ve  politika  için  istekte  bulunulabilir.  Bu  amaçla kullanılan  sınıflar:  TaskRestUtils,  PolicyRestUtils  ve ProfileRestUtils’dir.  Görev  bildirimlerinin dinlenmesinde ileTaskStatusNotificationListener’dır.

**TaskRestUtils:** Lider sunucusuna görevle ilgili istek gönderen utility sınıfıdır.

**PolicyRestUtils:** Lider sunucusuna politika ile ilgili istek gönderen utility sınıfıdır.

**ProfileRestUtils:** Lider sunucusuna profil ile ilgili istek gönderen utility sınıfıdır.

**TaskNotificationListener:**  Görev  gönderimindeki  bildirimleri  dinler.  Bir  bildirim  alındığında görevle ilgili bir bildirim gösterilir ve eklentileri uyarmak için bir event fırlatılır.

**TaskStatusNotificationListener:** Ahenk’ten  cevap  olarak  dönen  görev  durum  bildirimlerini dinler. Bir bildirim alındığında görev durumuyla ilgili bir bildirim gösterilir ve eklentileri uyarmak için bir event fırlatılır. 


## Lider-Console Servis Sınıfları

**RestClient:** Lider sunucusuna request göndermek ve cevapları ele alabilmek için utility metodlarını kullanıma sunar.

**PolicyExecutionRequest:** Politika uygulandığı sırada kullanılan politikanın nereye uygulanacağını söyleyen sınıftır.

**PolicyRequest:** Politika CRUD işlemlerinde kullanılan sınıftır.

**ProfileRequest:** Profil CRUD işlemlerinde kullanılan sınıftır.

**ReportGenerationRequest:** Rapor üretildiği sırada kullanılan sınıftır.

**ReportTemplateRequest:** Geliştirici tarafından tanımlanan rapor sorgusu, rapor parametreleri vb içerir. Lider'de servis olarak tanımlanıp kullanılır.

**ReportViewRequest:**  Rapor tanımına ait CRUD işlemlerinde kullanılan sınıftır.

**TaskRequest:** Görev CRUD işlemlerinde kullanılan sınıftır.

**RestResponse:** Rest servisinden dönen cevap için kullanılan sınıftır.

**AgentRestUtils:** Lider sunucusuna ajan ile ilgili istek gönderen utility sınıfıdır.

**PluginRestUtils:** Lider sunucusuna eklenti ile ilgili istek gönderen utility sınıfıdır.

**PolicyRestUtils:** Lider sunucusuna politika ile ilgili istek gönderen utility sınıfıdır.

**ProfileRestUtils:** Lider sunucusuna profil ile ilgili istek gönderen utility sınıfıdır.

**ReportRestUtils:** Lider sunucusuna rapor ile ilgili istek gönderen utility sınıfıdır.

**SearchGroupRestUtils:** Lider sunucusuna arama grubu ile ilgili istek gönderen utility sınıfıdır.

**TaskRestUtils:** Lider sunucusuna görevle ilgili istek gönderen utility sınıfıdır.

**XMPPClient:** Online/Offline bilgisini okumak ve görev sonucunu almak için kullanılır.

**TaskNotificationListener:** Görev gönderimindeki bildirimleri dinler. Bir bildirim alındığında görevle ilgili bir bildirim gösterilir ve eklentileri uyarmak için bir event fırlatılır.

**TaskStatusNotificationListener:** Ahenk’ten cevap olarak dönen görev durum bildirimlerini dinler. Bir bildirim alındığında görev durumuyla ilgili bir bildirim gösterilir ve eklentileri uyarmak için bir event fırlatılır.

**TaskNotification:** Görev bildirimi CRUD işlemlerinde kullanılan sınıftır.

**TaskStatusNotification:** Görev durum bildirimi işlemlerinde kullanılan CRUD sınıfıdır.