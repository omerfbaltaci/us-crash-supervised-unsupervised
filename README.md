# ABD Kaza Şiddeti Tahmini - Gözetimli ve Gözetimsiz Öğrenme

Bu proje, ABD'deki trafik kazalarının şiddetini hem gözetimli hem de gözetimsiz makine öğrenme tekniklerini kullanarak tahmin etmeyi amaçlamaktadır. Kullanılan veri seti, kazalarla ilgili çeşitli özellikler içermekte olup, her bir kazanın şiddetini (1'den 4'e kadar) sınıflandırmak hedeflenmiştir.

## İçindekiler
- [Genel Bakış](#genel-bakış)
- [Veri Seti](#veri-seti)
- [Proje Yapısı](#proje-yapısı)
- [Yöntem](#yöntem)
- [Sonuçlar](#sonuçlar)
- [Proje Nasıl Çalıştırılır?](#proje-nasıl-çalıştırılır)
- [Gereksinimler](#gereksinimler)
- [Sonuç ve Değerlendirme](#sonuç-ve-değerlendirme)
- [Gelecek Çalışmalar](#gelecek-çalışmalar)

## Genel Bakış
ABD'deki trafik kazalarının şiddetini anlamak, yol güvenliğini artırmada kritik öneme sahiptir. Bu proje, kaza verilerine dayalı olarak kaza şiddetini tahmin etmek için makine öğrenimi tekniklerini uygular. Çalışmada iki ana yaklaşım kullanılmaktadır:
1. **Gözetimli Öğrenme**: Etiketli verilerle kaza şiddetini sınıflandırma.
2. **Gözetimsiz Öğrenme**: Önceden tanımlanmamış etiketlerle benzer kazaları kümelere ayırma.

## Veri Seti
Projede kullanılan veri seti, [US Accidents Dataset](https://www.kaggle.com/sobhanmoosavi/us-accidents) olarak bilinen ABD kaza verilerinden oluşmaktadır. 

### Ana Özellikler:
- `Start_Lat`, `Start_Lng`: Kazanın gerçekleştiği enlem ve boylam bilgisi. (Projeye dahil değil)
- `Severity`: Kazanın şiddeti (1 ile 4 arasında değişen değerler).
- `Distance(mi)`: Kazanın kapsadığı mesafe.
- `Weather_Condition`: Kazanın olduğu sıradaki hava durumu. (Projeye dahil değil)
- `Start_Time`, `End_Time`: Kazanın başlama ve bitiş zamanı.

### Hedef Değişken:
- `Severity`: Kazanın şiddetini belirten, 1 ila 4 arasında değişen kategorik bir değişken.

## Proje Yapısı
Proje aşağıdaki temel dosya ve klasörlerden oluşmaktadır:
- **us-crash-supervised-unsupervised.ipynb**: Verilerin işlenmesi, keşifsel veri analizi (EDA), model oluşturma (hem gözetimli hem gözetimsiz) ve değerlendirme adımlarını içeren Jupyter not defteri.
- **README.md**: Proje dokümantasyonu.
- **data/**: (İsteğe bağlı) Veri setinin yer aldığı klasör.

## Yöntem
### Gözetimli Öğrenme:
Gözetimli yaklaşımda, kaza şiddetini tahmin etmek için çeşitli sınıflandırma algoritmaları uygulanmıştır. Kullanılan yöntemler şunlardır:
- kNN (K-En Yakın Komşu) Algoritması
- Decision Tree (Karar Ağacı) Algoritması

### Gözetimsiz Öğrenme:
Verideki gizli desenleri keşfetmek için gözetimsiz kümelenme teknikleri uygulanmıştır. Bu yöntemler, kaza şiddeti etiketleri olmadan benzer kazaların gruplandırılmasını sağlar.
- **K-means**: K-ortalama kümeleme ya da K-means kümeleme yöntemi N adet veri nesnesinden oluşan bir veri kümesini giriş parametresi olarak verilen K adet kümeye bölümlemektir.
- **MiniBatch KMeans**: Geleneksel k-means algoritmasının daha hızlı bir versiyonu.

## Sonuçlar
- **Gözetimli Öğrenme**: Decision Tree (Karar Ağacı), kaza şiddetini tahmin etmede en iyi performansı göstermiştir ve yaklaşık %60 doğruluk elde edilmiştir. Modelin performansı karışıklık matrisi ve sınıflandırma raporu ile değerlendirilmiştir.

- EDIT;
Model içerisindeki kNN algoritmasını bütün satırlarla (nrows kullanmadan) ve n_neighbors=2, test_size=0.4 olarak çalıştırdığımda aşağıda görünen sonucu aldım. Proje yükleme gününde bu işlem çok uzun sürdüğünden yetiştirememiştim, sonradan tekrar modeli daha büyük bir hacimle test etmek istedim. Başarı oranı kayda değer miktarda arttı. Aşağıya görseli bırakıyorum.

<img width="785" alt="image" src="https://github.com/user-attachments/assets/879c76d9-8f9b-4751-a63a-511a04cf556c">
  
- **Gözetimsiz Öğrenme**: Veri setini gözetimsiz öğrenme algoritmalarıyla pek uyumlu çalıştırmayı başaramadım, kendi uyguladığım prosedürler sonucu alabildiğim en yüksek başarı oranı 0.04 ile MiniBatch algoritmasına ait.

## Proje Nasıl Çalıştırılır?
1. Bu repoyu klonlayın:
   ```bash
   git clone https://github.com/omerfbaltaci/us-crash-supervised-unsupervised
   cd us-crash-supervised-unsupervised
