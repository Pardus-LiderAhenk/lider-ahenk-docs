**Kayıt Şablonları**

Şablonda belirtilen metinle başlayan istemcilerin domaine sadece şablonda belirtilen gruba üye olan 
kullanıcılar tarafından alınmasını sağlayıp bu kullanıcıların şablonda verilen grup altında 
oluşturulmasını sağlar.
Örneğin şablon adı 'pardus-01-', yetkili grup DN'i ya da kullanıcı DN'i 
'ou=Teknik,ou=Ankara,ou=People,dc=liderahenk,dc=org' ve istemcilerin dahil edileceği grup ise 
'ou=Yöneticiler,ou=Çankaya,ou=Ankara,ou=People,dc=liderahenk,dc=org' olsun.
Bu kayıt şablonundan sonra istemci adı 'pardus-01-' ile başlayan tüm kullanıcılar sadece 
'ou=Teknik,ou=Ankara,ou=People,dc=liderahenk,dc=org' grubunda yer alan yetkili kullanıcılar 
tarafından domaine alınabilir(yetkili gruba sadece bir kullanıcı DN'i de eklenebilir) ve 
domaine alınan istemciler 'ou=Yöneticiler,ou=Çankaya,ou=Ankara,ou=People,dc=liderahenk,dc=org' 
grubu altında oluşturulur.

![Anlık Mesaj](../images/kayitsablonlari/kayitsablonlari.png)<link href=/lider2.0/assets/style.css rel=stylesheet></link>
