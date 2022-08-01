**Kayıt Şablonları**

Şablonda belirtilen metinle başlayan istemcilerin domaine sadece şablonda belirtilen gruba üye olan 
kullanıcılar tarafından alınmasını sağlayıp bu kullanıcıların şablonda verilen Organizasyon Birimi altında 
oluşturulmasını sağlar. Örneğin şablon adı: 

>'pardus-01-'

yetkili grup DN'i 

>'cn=adminGroups,ou=User,ou=Groups,dc=liderahenk,dc=org'

ve istemcilerin dahil edileceği Organizsayon Birimi ise: 

>'ou=ANKARA,ou=Agents,dc=liderahenk,dc=org'

olsun. 

Bu kayıt şablonundan sonra istemci adı: 
'pardus-01-' ile başlayan tüm kullanıcılar sadece: 

>'cn=adminGroups,ou=User,ou=Groups,dc=liderahenk,dc=org'

grubunda yer alan yetkili kullanıcılar tarafından domaine alınabilir ve domaine alınan istemciler 

>'ou=ANKARA,ou=Agents,dc=liderahenk,dc=org' 

Organizsayon Birimi altında oluşturulur.

[![Kayıt Şablonları](../images/registirationTemplate/registirationTemplate.png)](../images/registirationTemplate/registirationTemplate.png)

2 çeşit kayıt şablonu oluşturulabilmektedir.

1) IP Adresi
[![Kayıt Şablonları](../images/registirationTemplate/registirationTemplateAddIp.png)](../images/registirationTemplate/registirationTemplateAddIp.png)

Belirtilen IP Adresi ile IP alan istemcilerin domaine alınırken doğru dizin ve doğru yetki grubuna dahil edilmesi için
IP Adresinin kullanıldığı yöntemdir.

2) Bilgisayar Adı
[![Kayıt Şablonları](../images/registirationTemplate/registirationTemplateAddName.png)](../images/registirationTemplate/registirationTemplateAddName.png)

Belirtilen metinle başlayan istemcilerin domaine alınırken doğru dizin ve doğru yetki grubuna dahil edilmesi için
Bilgisayar Adının kullanıldığı yöntemdir. 

<link href=/lider3.0/assets/style.css rel=stylesheet></link>
