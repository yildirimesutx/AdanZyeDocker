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



