### 3. Lider

Lider;  merkezde  toplanan  verilerin  saklanması,  tanımlanan  politikaların  ve  verilen  görevlerin Ahenklere  dağıtılmasından  sorumlu  sistemin  temel  bileşenidir.  Lider;  kendine  ait  bir  ilişkisel veritabanına,kullanıcı ve ahenk sistemlerinin tanımlı olduğu LDAP sistemine ve ayrıca iletişim için kullanılan Jabber sunucu ile çalışır.

İlişkisel  veritabanı  ahenk  sistemlerinin  özelliklerini,  verilen  görevleri,  bu  görevlerin  ahenklere uygulanma kayıtlarını, bu görevlerin sonuçlarını, tanımlanan politika bilgilerini ve bu politikaların hangi kullanıcı ve sistemlere  uygulanacağını  saklar.  Geliştirme ve test süreçlerinde ilişkisel veritabanı yönetim sistemi olarak MariaDB kullanımasına karşın, Lider herhangi bir ilişkisel veritabanı ile çalışabilecek şekilde kodlanmıştır. Veriatabanı  işlemleri OpenJPA kütüphanesi ile sağlanmaktadır.  Sistem  tamamen  JPQL  (Java  Persistence  Query  Language)  ile  çalışmaktadır.

Sistem üzerindeki dinamik raporlama sistemi de bu yapıya uygun ve tutarlı şekilde JPQL kullanacak şekilde tasarlanmıştır.

Yönetim sisteminde, Ahenk kurulu sistemler ve bu sistemleri kullanan kullanıcılar LDAP sistemler üzerinde tanımlanır. Lider Ahenk sistemindeki dinamik kayıt özellikleri kullanılarak, Ahenk sistemleri kurulum sırasında belirlenebilen bir ağaç yapısında LDAP’a eklenirler. Kullanıcı giriş ve yetkilendirme işlemleri LDAP üzerinden yapılabildiği gibi yerel kullanıcılarda  yönetilebilmektedir.

LDAP geliştirimi olarak OpenLDAP ile çalışılmış olmasına karşın; Lider, diğer LDAP varyantları ile uyumludur.

Yönetim sistemi Lider ile Ahenk sistemler arasındaki iletişim güncel olarak yoğun kullanılan Jabber(XMPP) protokolü üzerinden gerçekleştirmektedir.

Bu protokol temel olarak milyonlarca kullanıcının yoğun olarak kullandığı asenkron mesajlaşma  için geliştirilmiştir. Yoğun çok uçlu sistemlerin haberleşmesinde uygun, sağlam ve güçlü yapısı nedeniyle tercih edilmiştir.

(https://xmpp.org/uses/instant-messaging.html)

Mesajlama  sistemini  yönetimi  ejabberd  sunucu(lar)  ile  sağlanmaktadır.  Uzun  süreli  geliştirme geçmişi,  yaygınlığı,  sağlamlılığı  ve  güvenirliliği  nedeniyle  ejabberd  tercih  edilmiştir.  LiderAhenk sistemi herhangi bir XMPP sunucusu ile çalışabilecek şekilde geliştirilmiştir. XMPP sunucu, sistem veri akışını yönettiğinden en kritik unsurdur.

Lider  sistemi  bileşen  (bundle)  tabanlı  bir  OSGI  uygulamasıdır.  Yazılan  bileşenler  Apache  Karaf üzerinde koşmaktadır. Çekirdek Lider yapısıda değişik görevleri yerine getirmek için bileşenler şeklinde  geliştirilmiştir. Örneğin; İlişkisel veritabanı bağlantısı ve yönetimi için bir bileşen, XMMP mesajlaşma alt yapısı için başka bir bileşen yazılmıştır. Bu bileşenler birbirlerine hizmet sağlayabilmektedirler. Bileşenler çalışma zamanında değiştirilebilmekte, yüklenebilmekte ve çıkartılabilmektedir. Ayrıca her sistem eklentisi de yine bileşen olarak geliştirilmektedir.  Örneğin; USB  yetkilerini  düzenleyen  eklenti  bir  Karaf  bileşeni  şeklinde  tasarlanır  ve  geliştirilir.  Bu  sayede sistem kurumların özelliklerine ve ihtiyaçlarına göre uyarlanabilmektedir.

Apache Karaf sisteminin kullanımı için bu belgeden faydalanabilirsiniz.

(https://karaf.apache.org/manual/latest/quick-start.html)