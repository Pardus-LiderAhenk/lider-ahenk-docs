# Paket Yönetimi Eklentisi

Paket Yönetimi eklentisi bir görev eklentisidir. Eklenti, Ahenk makinelerinde paket kontrolü, paket yükleme-kaldırma, depo ekleme gibi paket işlemleri ile ilgili temel görevleri yerine getirmektedir. Çalıştırılan görevler doğrultusunda edinilen bilgi ile oluşturulan dört rapor da eklenti bünyesindedir.

**Paket  Yönetimi Eklentisi**'ne  herhangi bir Ahenk makinesine sağ tıklanılarak **"Görev- Çalıştır"** menüsünün **"Paket Yöneticisi"** alt menüsünden ulaşılmaktadır.

## Paket Kontrolü

Adı ve (isteğe bağlı olarak) sürüm bilgisi belirtilen paketin seçilmiş olan Ahenk/ler içerisinde yüklü olup olmadığı bilgisini tabloda kullanıcıya sunar. 

![Package Manager Filter](images/package-manager-filter.png)

Paket kontrolü görevi aynı anda birçok makine üzerinde işlem yapılabilen bir görevdir. Tabloda gösterilen bilgiler üzerinde çeşitli filtrelemeler yapılabilir, arama grupları oluşturulabilmektedir (Yüklü olan makineler seçilsin, istenilen bir paket versiyonu yüklü olan makineler seçilsin, yüklü olmayan makineler seçilsin özellikleri yanında manuel olarak da seçim yapılarak arama grubu oluşturulabilmektedir.).

## Paket Arşivi

Bir Ahenk makine için çalışan bu görev, **"Paket Adı"** bölümüne girilen paket ismini içeren paketlerin yüklenme,  güncellenme, kurulum zamanı bilgilerini kullanıcıya sunar. Kullanıcının önceki bir sürümü seçmesi ve **"Sürüme Dön"** butonuna tıklaması halinde Ahenk makine ilgili paketin seçilen versiyonuna geri döner.

![Package Manager Arsiv](images/package-manager-arsiv.png)

## Paket Depoları

Bir Ahenk makine için çalışan bu görev, makinede bulunan tüm depoların listelenmesini sağlamaktadır.

![Package Manager Depolar](images/package-manager-depolar.png)

Kullanıcı buradan seçtiği depoyu çıkarabilmekte ve **"Ekle"** butonuna tıklayarak açılan- pencereye yeni bir depo URL’i girebilmektedir. **"Çalıştır"** butonuna tıklandığı takdirde yeni eklenen depolar Ahenk makineye eklenecek; çıkarılan depolar ise Ahenk makineden çıkarılacaktır.

## Paket Kur/Kaldır

Bir Ahenk makine için çalışan bu görev, makinedeki tüm paketleri yüklü olup olmadığı bilgisiyle kullanıcıya sunar.

![Package List](images/package-list.png)

Kulanıcı buradan istenen durum bilgisini değiştirerek her bir paket için yükleme ve kaldırma işlemi yapabilmektedir.

![Package Uninstall](images/package-uninstall-1.png)

İstenen durum bilgisini değiştirmek için ilgili kolun tıklanılmalı ve açılan menüden **"Yükle"** veya **"Kaldır"** seçeneklerinden biri seçilmelidir. Aynı anda birden çok paket işlemi yapılabilmektedir. Paket sorgulandığında kaldırıldığı görülebilir.

![Package Uninstall-2](images/package-uninstall-2.png)

## Uygulama Çalıştırma İstatistikleri

Birçok Ahenk makinede aynı anda çalışabilen bu görev, belirli bir kullanıcı ya da komut için kac kere işletildiği bilgisi, işletim tarihleri, işletim süreleri gibi bilgileri tabloda sunan ve aynı zamanda ileride raporunu alabilmek adına bu bilgileri, eş zamanlı olarak, veri tabanına kaydeden görevdir. Sadece komut ve kullanıcı alanları dolu iken seçilen kullanıcı veya komut bilgileri tabloya gelirken **"Yalnız bu kullanıcı için işlem yap"** butonu tıklandığında sadece girilen kullanıcı ismiyle giriş yapan ve girilen komutu çalıştıran kullanıcıların verileri getirilir.

![Package Uninstall-2](images/package-istatistik.png)

## Paket ve Depo Yönetimi

Birçok Ahenk makinede aynı anda çalışabilen bu görev, belirtilen bir ya da daha fazla deponun içeriğindeki paketleri listeler.

![Paket ve Depo Yonetimi](images/paket-ve-depo-yonetimi.png)

Listelenen bu paketler arasından bir ya da daha çok paket şeçilip yükleme/kaldırma işlemleri yapılabilir.

![Paket ve Depo Yonetimi Yukle](images/paket-ve-depo-yonetimi-yukle.png)