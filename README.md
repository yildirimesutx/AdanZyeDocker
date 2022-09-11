# Docker

- Docker CLI (Command Line Interface)

`docker version` komutu ile client ve server Docker engine kontrol ediliyor, bu komutu powershell(windowsda, mac de terminal) ile calistirdik, asagıda belirtilen ekran gelmeli

```
Client:
 Cloud integration: v1.0.28
 Version:           20.10.17
 API version:       1.41
 Go version:        go1.17.11
 Git commit:        100c701
 Built:             Mon Jun  6 23:09:02 2022
 OS/Arch:           windows/amd64
 Context:           default
 Experimental:      true

Server: Docker Desktop 4.11.1 (84025)
 Engine:
  Version:          20.10.17
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.17.11
  Git commit:       a89b842
  Built:            Mon Jun  6 23:01:23 2022
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.6
  GitCommit:        10c12954828e7c7c9b6e0ea9b0c02b01407d3ae1
 runc:
  Version:          1.1.2
  GitCommit:        v1.1.2-0-ga916309
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

client o isletim sistemini baz alarak kuruluyor, server ise linux isletim sistemli sanal makine kurularak deamen buraya kuruluyor.

client win da deamon ise linuxda calisiyor.

`docker info` komutu ile de sistemde docker ile ilgili temel bilgilere ulaşıyoruz. 


`docker` komutu ile de docker komutlarını gorebiliriz.

- bu komutlar 3 ana baslik altında toplanmistir. Options, Managment Commands, Commands 

- 2017 yilinda itibaren <docker "yönetilmek istenilen bolum" "komut"> seklinde komutlari yaziyoruz  

örnek => `docker container run hello-word` 

örnek => `docker image --help` yazarsak image ile ilgili yazabilcegimiz komutlar gelmektedir.

---

**Container Temelleri-1**


`docker container create` ile container oluşturuluyor, `start` ile baslatılıyor,
bu islemleri tek seferde yapabilmek icin `docker container run` kullanılıyor

- komut ile cagrilan image localde yoksa docker hub tan cagrilir.

`docker container ls -a` komutu ile tüm calisan kapatilmis containerları gorüyoruz.


- Her container imajında, o imajdan bir container yarattıgımiz zaman varsayılan olarak calısması icin ayarlanmıs bir uygulama vardır.

- bu uygulama calıştigi sürece container ayakta kalır

- uygulama calismayi biraktiginda container da kapatilir.

**Container Temelleri-2**

 soru-1: Docker imajlarında sadece tek bir uygulama mı vardır?

 Hayır. Docker imajında birden fazla uygulama olabilir. Tek bir uygulama içermesi kural değildir.

 soru-2: Docker, imajlarından container yaratıldığında çalışması için birden fazla uygulama atanabilir mi?

 Hayır. Docker container başlatıldığı zaman otomatik çalışması için tek bir uygulamanın ayarlanmasına izin verir.

soru-3 : Docker container içerisinde sadece tek bir uygulama mı çalıştırılabilir?

Hayır. Docker container başlatıldığı zaman otomatik çalışması için tek bir uygulamanın ayarlanmasına izin verir fakat container içerisinde daha sonra bu uygulamanın yanında başka uygulamaklar da çalıştırılabilir.

soru- 4: Docker image inda varsayılan olarak çalıştırılması için ayarlanan uygulama terine başka uygulama ile container başlatabiliyor muyuz?

Evet. Container yaratılırken hangi uygulamayı çalıştırılmasını belirtebiliriz.



```
docker container run --name deneme -d -p 80:80 ozgurozturknet/adanzyedocker
docker container run -p 80:80 dizin/imagename  
# 80:80 potunu acıp ilgili image baslattı container oluştu
# containerlar için uniq id üretilir

docker container ls
#bize calisan containerları gösterir

docker container run --name denemecon dizin/imagename java app1
# bu komut ile containeri default isim yerine kendi yazdigimiz ismi verdik, ayrıca baslatilan uygulama yerine son kısımda yazdığımız uygulayı baslattik.

docker container run -d -p 80:80 dizin/imagename
# bu komut ile arka planda container calisiyor, bizim shell mizi baglamadi.

docker container ls -a => docker ps -a
#calisan calismayan tüm containerlari gösterir

docker container rm idnumarasi
# containeri siler, calisan containeri silemez, fakat rm -f idnumra ile zorla silme yapabiliyoruz.

docker container stop f43
# calisan containeri durdurur. sondaki uc karakter id numarası basi

```


**Container Temelleri-3**

```
docker container run --name websunucu -p 80:80 -d ozgurozturknet/adanzyedocker

 docker container exec -it websunucu sh
# containeri bağlanma komutu, websunucu bizim proje ismi 

 ls -l  içindeki uygulamaları gördük ve isimlerini yazarak uygulamayı calıştirdik

 container a baglantı kurulduktandan sonra ps ile container içinde yüklü  appleri görüntüledik


docker container run --name websunucu2 -p 80:80 -d ozgurozturknet/adanzyedocker 
# bir containerdan aynı image kullanarak milyonlarca container oluşturulabiliyor

```


docker container prune # calısmayan tüm containerları siliyor
docker image ls # image gösteriyor
docker image prune -a # image siliyor
docker image pull alpine #

**Docker Katmanlı Dosya Yapısı**

- Docker Union File System (birlesik dosya sistemi)

<img src="notes/katman.png">

- aynı image ile birçok container uretilebilir. Yapilan bu degisikler ayri bir katman olarak tutulur. Bu degisiklikten diger containerlar etkilenmez.

- ayri katmanlardan olusan container ls komutu ile tek bir dosya yapısında gibi görünür. Bu yapıya Union file system denir.

- Copy on Write

   - container içinde yapilan degisiklik image file icindeyse bu degisiklik yazılabilir katmana R/W Layer tasinir. 

<img src="notes/copy_on_write.png">


- Not : İmage katmanli yapisi mevcut, docker aynı katmanlı olanları tek bir sefer hafizaya aliyor.

