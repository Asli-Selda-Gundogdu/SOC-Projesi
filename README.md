Proje Amacı
Bu projenin amacı, bilgisayar sistemlerinde indirilen dosyaların güvenliğini sağlamak ve kullanıcıları zararlı yazılımlara karşı uyarmak ve korumaktır. 
Gerçek zamanlı dosya izleme ve hash kontrol mekanizması ile sistemde yeni eklenen dosyaların güvenilirliği kontrol edilerek zararlı dosyaların erken tespiti hedeflenmektedir.

Projenin Kullandığı Araçlar ve Kütüphaneler
1. Programlama Dili
Programlama dili olarak Python kullanılmıştır ve Tkinter ile GUI (grafiksel kullanıcı arayüzü) geliştirilmiştir. 

2. Kütüphaneler
2.1. Dahili Python Kütüphaneleri
Python’un standart kütüphaneleri:

tkinter:
GUI(grafiksel kullanıcı arayüzü) elemanları pencere, buton gibi araçları oluşturmak ve kullanıcı etkileşimi sağlamak için kullanılmıştır.
Özellikler: Pencere oluşturma, düğmeler.

os:
İşletim sistemi seviyesinde dosya ve dizin kontrolü yapmak için kullanılmıştır.
Özellikler: Dosyanın var olup olmadığını kontrol etme (os.path.exists) ve dosya yolunu doğrulama (os.path.isfile).

hashlib:
SHA-256 gibi kriptografik hash algoritmalarını kullanmak için.
Özellikler: Dosyanın SHA-256 hash değerini hesaplamak için (hashlib.sha256()).

2.2. Harici Python Kütüphaneleri
Python’un standart kütüphanelerine ek olarak, “pip install” komutu ile yüklenmesi gereken kütüphaneler:

watchdog:
Dosya sistemindeki değişiklikleri izlemek için kullanılmıştır. Yeni dosya eklendiğinde veya değişiklik yapıldığında tetiklenen olaylarla çalışır.
Özellikler: Belirli bir klasördeki (örneğin, "Downloads" dizini) yeni dosya oluşturma veya değiştirme olaylarını izleme. İzlenen klasöre yeni bir dosya eklendiğinde olayı algılama

plyer:
Masaüstü bildirimleri göstermek için kullanılmıştır.
Özellikler: Kullanıcıyı bilgilendirmek için masaüstü uyarıları (örn. "Dosya zararlı olabilir!" bildirimi). Bildirimlerde başlık ve mesaj içeriği ekleme

queue: 
Çoklu iş parçacığı (thread) arasında güvenli iletişim sağlamak için kullanılmıştır.
Özellikler: Mesaj kuyruğu oluşturarak arayüz ve arka plandaki işlem arasında bilgi aktarımı sağlama

threading: 
Dosya hash kontrolü gibi uzun sürebilecek işlemleri ana arayüzün donmasını engellemek için ayrı bir iş parçacığında çalıştırmak için kullanılmıştır.
Özellikler: Arka planda çalışan bağımsız görevler oluşturma

3. Geliştirme Araçları
Projenizi çalıştırmak için Python 3.x gereklidir. Önerilen Sürüm: Python 3.8 veya daha üstü. Harici özellikleri yüklemek için ‘pip’ kullanılır. Kod geliştirme ve hata ayıklama için PyCharm, VS Code, veya Jupyter Notebook kullanılabilir.

4. Kaynak Dosyalar
dataset.txt:
Dosya hash kontrolü için kullanılan metin dosyası. Bu dosyaki her satır zararlı hash değerlerini içerir.
Amaç: Seçilen dosyanın hash değerinin güvenli olup olmadığını doğrulamak.


Projenin Çalışma Prensibi
Proje, bir dosyanın SHA256 hash değerini hesaplayarak bu değeri yüklenen veri kümesi ile karşılaştırır. Eğer yüklenen dosyanın hash değeri veri kümesindeki hash değeri ile uyuşuyorsa, kullanıcıya uyarı verir. Eğer uyuşmuyorsa dosya güvenlidir ve güvenli olduğunun bilgilendirme mesajı gösterilir.

Proje Çalışma Adımları
Kodun Çalıştırılması:
Kullanıcı kodu çalıştırır. Uygulama arka planda çalışır.

Klasör İzleme
Kullanıcı her dosya indirdiğinde ‘Watchdog’ kütüphanesi ile ‘İndirilenler’ dosyası izlenir.

Dosyanın Kontrol Edilmesi
3.1. SHA-256 Hash Hesaplama
Kullanıcı bir dosya seçtikten sonra, dosyanın SHA-256 hash değeri hesaplanır.
Hash Hesaplama İşlemi:
Dosya, 1024 baytlık bloklar halinde okunur.
Her blok, hashlib kullanılarak hash fonksiyonuna eklenir.
Tüm dosya okunduktan sonra hash değeri hesaplanır.

3.2. dataset.txt Dosyasını Kontrol Etme
Program, hash değerini dataset.txt dosyasındaki değerlerle karşılaştırır:
Eğer dosyada hash değeri bulunuyorsa, bu dosya zararlı olarak işaretlenir.
Eğer hash değeri bulunmuyorsa, dosya güvenli kabul edilir.

Kullanıcı Uyarısı
Eğer dosya zararlıysa:
Kırmızı bir uyarı penceresi ve masaüstü bildirimi gösterilir.

Eğer dosya güvenliyse:
Yeşil bir onay penceresi ve masaüstü bildirimi gösterilir.

Arayüzün Özellikleri
Mesaj Kutuları:
Uygulamada 300x150 piksel boyutunda özel bir mesaj kutusu tasarlanmıştır.
Renk ve İçerik: Mesaj kutusunun arka plan rengi mesajın türüne göre değişir:
Hata (Kırmızı): Dosya zararlı veya bir sorun oluştuğunda.
Bilgi (Yeşil): Dosya güvenli olduğunda.
