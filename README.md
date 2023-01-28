# K-Means Clustering
## Kümeleme (Clustering) Nedir?
Kümeleme, makine öğrenmesinde veri setinde gruplama veya kümeleme işlemi yapar. Verilerin birbirlerine ne kadar benzer olduğunu bulmak ve benzer verileri gruplandırmak temel amaçtır. Bu bize hangi verilerin birbirleriyle daha yakınlık gösterdiğine, birbirleriyle arasında olan bağına dair bilgileri bulmamıza yarar.

Kümeleme algoritmaları, denetimsiz öğrenme (unsupervised learning) methodunu izlerler. Denetimsiz öürenmede verilerin çıktıları elimizde yoktur ve amacımız bu çıktıları bulmaktır. Verilerı etiketlememiz gerekmez. Denetimsiz öğrenme methodları etiketleri bulmaya çalışır.

## K-Means Clustering
$k$ tane küme $D$-boyutlu uzayda rastgele noktalara atanır. Bu seçilen noktaların her birine ortalama, initial cluster veya centroid diyebiliriz. Centroid'ler kümelerin ortalamasıdır. Bu centroid'lerden $k$ tane seçilir ve $n$ tane $x$ verilerinin her biri bu hangi centroid'e daha yakınsa o centroid'in temsil ettiği kümeye atanır. Bu işlem artık hiçbir $x$ veri noktası küme değiştirmeyinceye veya iterasyonu bitirmediğimiz müddetçe devam eder.

Elimizde X = ($x_1, x_2, ..., x_n$) şeklinde veri setimiz olsun ve her bir $x_i (i =1,2,...,n)$ değeri $D$-boyutlu uzayda bir noktayı temsil etsin.

Aynı zamanda elimizde C = ($\mu_1, \mu_2, ..., \mu_k$) tane kümemiz olsun.

$k$ oluşturmak istediğimiz küme sayısını gösterir ve bizim belirlediğimiz bir değerdir.
İstediğimiz çıktı, her $x_i (i =1,2,...,n)$ değerinin benzerliklerine göre farklı $\mu_j (j =1,2,...,k)$ kümelerine atanmasıdır. 

K-Means Clustering algoritması bu benzerlikler $D$-boyutlu uzayda veri noktalarının birbirlerine yakınlıklarını hesaplayıp ortalamaya (centroid'lere) ne kadar uzak olduklarını hesaplayarak yapar.

Uzaklık ölçütü için genellikle Euclidean uzaklık fonksiyonu kullanılır fakat zorunlu değildir. Euclidean uzaklığı aşağıdaki formül ile hasaplanır. Örneğin $D$-boyutlu uzayda $p$ ve $q$ noktaları arasındaki uzaklığı hesaplamak için

dist($p$, $q$) = $\sqrt{(p_1 - q_1)^2 + (p_2 - q_2)^2 + ... + (p_n - q_n)^2}$

formülü kullanılır.

## K-Means Clustering Adımları
X = ($x_1, x_2, ..., x_n$) veri setini $k$ tane kümeye ayırmak istendiğinde yapmamız gereken adımlar şunlardır:

Rastgele $k$ tane veri noktası seçilir. Bu veri noktaları başlangıç ortalamalarıdır (initial centroids). Başlangıç ortalamalarını da C = ($\mu_1, \mu_2, ..., \mu_k$) olarak gösterelim.

1) Her $x_i$ veri noktası için $c_j$ kümesine olan uzaklığı hesaplanır ve en yakın $c_j$ kümesine atanır.

    $$c_i = \arg \min_{j=1}^{k} |x_i - \mu_j|^2
    = \arg \min_{j=1}^{k} dist(x_i, \mu_j)$$


2) Her bir $j = 1, 2, ..., k$ kümesi için 2. adımda $c_j$ kümesine atanan bütün $x_i$ noktaları için yeni ortalamalar hesaplanır. Başka deyişle de kümelenmiş veri noktalarından yeni centroid'i bulmak için aşağıdaki formül kullanılır. Burada $n_j$ j. kümeye atanan bütün noktaların sayısını ifade eder.

$$\mu_j = \frac{1}{n_j} \sum_{i=1}^{n} x_i$$

Yukarıdaki 2 adım bir daha hiçbir $x_i$ verisi değişmeyene kadar devam eder.

K-Means Clustering algoritması başlangıç ortalamalarına (initial clusters) çok duyarlıdır. Başlangıç ortalamaları rastgele atandığı için bazen K-Means Clustering algoritması istenemeyen sonuçlar verebilir. Bu yüzden Bu algoritma en baştan tekrar tekrar çalıştırılır ve en iyi kümeleme sonucunu gösterir. Bunu uygulamak zorunda değildir ancak uygulandığı zaman çok daha güvenilir sonuç verir.

### En İyi Kümelenmiş Sonucu Seçmek
K-Means Clustering algoritması farklı başlangıç ortalamalarıyla tekrar tekrar algoritmayı çalıştırıp her $x$ veri noktasının kendi kümesinin ortalamasına uzaklığının karesi hesaplanır ve toplanır. Bu her küme için yapılır ve $k$ tane kümenin ortalamaya olan uzaklıklarının karesi toplanır. Bu toplamların en küçük olduğu gruplandırma döngüsü daha doğru kümelenmiş olarak kabul edilir.

 Hataların Karelerinin Toplamı (Sum of Squares Errors): Her bir veri için, kendisinin bulunduğu küme ortalamasına olan uzaklıkların karelerinin toplamı alınır. Bu işlem her küme için yapılır ve sonucunda her kümenin hataların karelerinin toplamı toplanır.

$$
SSE=\sum_{C_j}^{C_k}(\sum_{x_i \in C_j}^{x_m} dist(x_i, C_j))
$$


___
## Uygulamalar
Veriler:
|    |   x_1 |   x_2 |
|---:|------:|------:|
|  0 |     2 |     1 |
|  1 |    -3 |     8 |
|  2 |    -0 |    10 |
|  3 |     3 |     2 |
|  4 |    -3 |     9 |
|  5 |     3 |    -0 |
|  6 |     5 |    -0 |
|  7 |    -2 |     6 |
|  8 |    -3 |    10 |
|  9 |     7 |     2 |

başlangıç ortalamaları (initial clusters)
|    |   x_1 |   x_2 |
|---:|------:|------:|
|  0 |     0 |     3 |
|  1 |     4 |     8 |

___
1. iterasyon:
___
$$x = (2.0, 1.0)$$
$$dist((2.0, 1.0), (0, 3)) = \sqrt{(2.0 - 0)^2 + ( 1.0 - 3)^2} = 2.83$$
$$dist((2.0, 1.0), (4, 8)) = \sqrt{(2.0 - 4)^2 + ( 1.0 - 8)^2} = 7.28$$
En Yakın Uzaklik: 2.83

En Yakın Ortalama: [0 3]

Cluster: 0
___
$$x = (-3.0, 8.0)$$
$$dist((-3.0, 8.0), (0, 3)) = \sqrt{(-3.0 - 0)^2 + ( 8.0 - 3)^2} = 5.83$$
$$dist((-3.0, 8.0), (4, 8)) = \sqrt{(-3.0 - 4)^2 + ( 8.0 - 8)^2} = 7.0$$
En Yakın Uzaklik: 5.83

En Yakın Ortalama: [0 3]

Cluster: 0
___
$$x = (-0.0, 10.0)$$
$$dist((-0.0, 10.0), (0, 3)) = \sqrt{(-0.0 - 0)^2 + ( 10.0 - 3)^2} = 7.0$$
$$dist((-0.0, 10.0), (4, 8)) = \sqrt{(-0.0 - 4)^2 + ( 10.0 - 8)^2} = 4.47$$
En Yakın Uzaklik: 4.47

En Yakın Ortalama: [4 8]

Cluster: 1
___
$$x = (3.0, 2.0)$$
$$dist((3.0, 2.0), (0, 3)) = \sqrt{(3.0 - 0)^2 + ( 2.0 - 3)^2} = 3.16$$
$$dist((3.0, 2.0), (4, 8)) = \sqrt{(3.0 - 4)^2 + ( 2.0 - 8)^2} = 6.08$$
En Yakın Uzaklik: 3.16

En Yakın Ortalama: [0 3]

Cluster: 0
___
$$x = (-3.0, 9.0)$$
$$dist((-3.0, 9.0), (0, 3)) = \sqrt{(-3.0 - 0)^2 + ( 9.0 - 3)^2} = 6.71$$
$$dist((-3.0, 9.0), (4, 8)) = \sqrt{(-3.0 - 4)^2 + ( 9.0 - 8)^2} = 7.07$$
En Yakın Uzaklik: 6.71

En Yakın Ortalama: [0 3]

Cluster: 0
___
$$x = (3.0, -0.0)$$
$$dist((3.0, -0.0), (0, 3)) = \sqrt{(3.0 - 0)^2 + ( -0.0 - 3)^2} = 4.24$$
$$dist((3.0, -0.0), (4, 8)) = \sqrt{(3.0 - 4)^2 + ( -0.0 - 8)^2} = 8.06$$
En Yakın Uzaklik: 4.24

En Yakın Ortalama: [0 3]

Cluster: 0
___
$$x = (5.0, -0.0)$$
$$dist((5.0, -0.0), (0, 3)) = \sqrt{(5.0 - 0)^2 + ( -0.0 - 3)^2} = 5.83$$
$$dist((5.0, -0.0), (4, 8)) = \sqrt{(5.0 - 4)^2 + ( -0.0 - 8)^2} = 8.06$$
En Yakın Uzaklik: 5.83

En Yakın Ortalama: [0 3]

Cluster: 0
___
$$x = (-2.0, 6.0)$$
$$dist((-2.0, 6.0), (0, 3)) = \sqrt{(-2.0 - 0)^2 + ( 6.0 - 3)^2} = 3.61$$
$$dist((-2.0, 6.0), (4, 8)) = \sqrt{(-2.0 - 4)^2 + ( 6.0 - 8)^2} = 6.32$$
En Yakın Uzaklik: 3.61

En Yakın Ortalama: [0 3]

Cluster: 0
___
$$x = (-3.0, 10.0)$$
$$dist((-3.0, 10.0), (0, 3)) = \sqrt{(-3.0 - 0)^2 + ( 10.0 - 3)^2} = 7.62$$
$$dist((-3.0, 10.0), (4, 8)) = \sqrt{(-3.0 - 4)^2 + ( 10.0 - 8)^2} = 7.28$$
En Yakın Uzaklik: 7.28

En Yakın Ortalama: [4 8]

Cluster: 1
___
$$x = (7.0, 2.0)$$
$$dist((7.0, 2.0), (0, 3)) = \sqrt{(7.0 - 0)^2 + ( 2.0 - 3)^2} = 7.07$$
$$dist((7.0, 2.0), (4, 8)) = \sqrt{(7.0 - 4)^2 + ( 2.0 - 8)^2} = 6.71$$
En Yakın Uzaklik: 6.71

En Yakın Ortalama: [4 8]

Cluster: 1
___
Verilerin kümelenmiş halleri:
|    |   x_1 |   x_2 |   cluster |
|---:|------:|------:|----------:|
|  0 |     2 |     1 |         0 |
|  1 |    -3 |     8 |         0 |
|  2 |    -0 |    10 |         1 |
|  3 |     3 |     2 |         0 |
|  4 |    -3 |     9 |         0 |
|  5 |     3 |    -0 |         0 |
|  6 |     5 |    -0 |         0 |
|  7 |    -2 |     6 |         0 |
|  8 |    -3 |    10 |         1 |
|  9 |     7 |     2 |         1 |

___

* 0. küme için ortalama hesabı:
$$x_1=\frac{2-3+3-3+3+5-2}{7} = \frac{5}{7} = 0.71$$
$$x_2=\frac{1+8+2+9-0-0+6}{7} = \frac{26}{7} = 3.71$$

* 1. küme için ortalama hesabı:
$$x_1=\frac{-0-3+7}{3} = \frac{4}{3} = 1.33$$
$$x_2=\frac{10+10+2}{3} = \frac{22}{3} = 7.33$$ 

Her kümenin ortalamasını kayıt ediyorum. Artık yeni ortalamalarımız aşağıdaki gibidir:
|    |   x_1 |   x_2 |
|---:|------:|------:|
|  0 |  0.71 |  3.71 |
|  1 |  1.33 |  7.33 |
___
2. iterasyon
___
$$x = (2.0, 1.0)$$
$$dist((2.0, 1.0), (0.71, 3.71)) = \sqrt{(2.0 - 0.71)^2 + ( 1.0 - 3.71)^2} = 3.0$$
$$dist((2.0, 1.0), (1.33, 7.33)) = \sqrt{(2.0 - 1.33)^2 + ( 1.0 - 7.33)^2} = 6.37$$
En Yakın Uzaklik: 3.0

En Yakın Ortalama: [0.71 3.71]

Cluster: 0
___
$$x = (-3.0, 8.0)$$
$$dist((-3.0, 8.0), (0.71, 3.71)) = \sqrt{(-3.0 - 0.71)^2 + ( 8.0 - 3.71)^2} = 5.67$$
$$dist((-3.0, 8.0), (1.33, 7.33)) = \sqrt{(-3.0 - 1.33)^2 + ( 8.0 - 7.33)^2} = 4.38$$
En Yakın Uzaklik: 4.38

En Yakın Ortalama: [1.33 7.33]

Cluster: 1
___
$$x = (-0.0, 10.0)$$
$$dist((-0.0, 10.0), (0.71, 3.71)) = \sqrt{(-0.0 - 0.71)^2 + ( 10.0 - 3.71)^2} = 6.33$$
$$dist((-0.0, 10.0), (1.33, 7.33)) = \sqrt{(-0.0 - 1.33)^2 + ( 10.0 - 7.33)^2} = 2.98$$
En Yakın Uzaklik: 2.98

En Yakın Ortalama: [1.33 7.33]

Cluster: 1
___
$$x = (3.0, 2.0)$$
$$dist((3.0, 2.0), (0.71, 3.71)) = \sqrt{(3.0 - 0.71)^2 + ( 2.0 - 3.71)^2} = 2.86$$
$$dist((3.0, 2.0), (1.33, 7.33)) = \sqrt{(3.0 - 1.33)^2 + ( 2.0 - 7.33)^2} = 5.59$$
En Yakın Uzaklik: 2.86

En Yakın Ortalama: [0.71 3.71]

Cluster: 0
___
$$x = (-3.0, 9.0)$$
$$dist((-3.0, 9.0), (0.71, 3.71)) = \sqrt{(-3.0 - 0.71)^2 + ( 9.0 - 3.71)^2} = 6.46$$
$$dist((-3.0, 9.0), (1.33, 7.33)) = \sqrt{(-3.0 - 1.33)^2 + ( 9.0 - 7.33)^2} = 4.64$$
En Yakın Uzaklik: 4.64

En Yakın Ortalama: [1.33 7.33]

Cluster: 1
___
$$x = (3.0, -0.0)$$
$$dist((3.0, -0.0), (0.71, 3.71)) = \sqrt{(3.0 - 0.71)^2 + ( -0.0 - 3.71)^2} = 4.36$$
$$dist((3.0, -0.0), (1.33, 7.33)) = \sqrt{(3.0 - 1.33)^2 + ( -0.0 - 7.33)^2} = 7.52$$
En Yakın Uzaklik: 4.36

En Yakın Ortalama: [0.71 3.71]

Cluster: 0
___
$$x = (5.0, -0.0)$$
$$dist((5.0, -0.0), (0.71, 3.71)) = \sqrt{(5.0 - 0.71)^2 + ( -0.0 - 3.71)^2} = 5.67$$
$$dist((5.0, -0.0), (1.33, 7.33)) = \sqrt{(5.0 - 1.33)^2 + ( -0.0 - 7.33)^2} = 8.2$$
En Yakın Uzaklik: 5.67

En Yakın Ortalama: [0.71 3.71]

Cluster: 0
___
$$x = (-2.0, 6.0)$$
$$dist((-2.0, 6.0), (0.71, 3.71)) = \sqrt{(-2.0 - 0.71)^2 + ( 6.0 - 3.71)^2} = 3.55$$
$$dist((-2.0, 6.0), (1.33, 7.33)) = \sqrt{(-2.0 - 1.33)^2 + ( 6.0 - 7.33)^2} = 3.59$$
En Yakın Uzaklik: 3.55

En Yakın Ortalama: [0.71 3.71]

Cluster: 0
___
$$x = (-3.0, 10.0)$$
$$dist((-3.0, 10.0), (0.71, 3.71)) = \sqrt{(-3.0 - 0.71)^2 + ( 10.0 - 3.71)^2} = 7.3$$
$$dist((-3.0, 10.0), (1.33, 7.33)) = \sqrt{(-3.0 - 1.33)^2 + ( 10.0 - 7.33)^2} = 5.09$$
En Yakın Uzaklik: 5.09

En Yakın Ortalama: [1.33 7.33]

Cluster: 1
___
$$x = (7.0, 2.0)$$
$$dist((7.0, 2.0), (0.71, 3.71)) = \sqrt{(7.0 - 0.71)^2 + ( 2.0 - 3.71)^2} = 6.52$$
$$dist((7.0, 2.0), (1.33, 7.33)) = \sqrt{(7.0 - 1.33)^2 + ( 2.0 - 7.33)^2} = 7.78$$
En Yakın Uzaklik: 6.52

En Yakın Ortalama: [0.71 3.71]

Cluster: 0
___
Kümelerin güncellenmiş halleri:
|    |   x_1 |   x_2 |   cluster |
|---:|------:|------:|----------:|
|  0 |     2 |     1 |         0 |
|  1 |    -3 |     8 |         1 |
|  2 |    -0 |    10 |         1 |
|  3 |     3 |     2 |         0 |
|  4 |    -3 |     9 |         1 |
|  5 |     3 |    -0 |         0 |
|  6 |     5 |    -0 |         0 |
|  7 |    -2 |     6 |         0 |
|  8 |    -3 |    10 |         1 |
|  9 |     7 |     2 |         0 |
___
* 0. küme için ortalama hesabı:
$$x_1=\frac{2+3+3+5-2+7}{6} = \frac{18}{6} = 3$$
$$x_2=\frac{1+2-0-0+6+2}{6} = \frac{11}{6} = 1.83$$

* 1. küme için ortalama hesabı:
$$x_1=\frac{-3-0-3-3}{4} = \frac{-9}{4} = -2.25$$
$$x_2=\frac{8+10+9+10}{4} = \frac{37}{4} = 9.25$$
___
Yeni ortalamalarım:
|    |   x_1 |   x_2 |
|---:|------:|------:|
|  0 |  3    |  1.83 |
|  1 | -2.25 |  9.25 
___
3. iterasyon
___
$$x = (2.0, 1.0)$$
$$dist((2.0, 1.0), (3.0, 1.83)) = \sqrt{(2.0 - 3.0)^2 + ( 1.0 - 1.83)^2} = 1.3$$
$$dist((2.0, 1.0), (-2.25, 9.25)) = \sqrt{(2.0 - -2.25)^2 + ( 1.0 - 9.25)^2} = 9.28$$
En Yakın Uzaklik: 1.3

En Yakın Ortalama: [3.   1.83]

Cluster: 0
___
$$x = (-3.0, 8.0)$$
$$dist((-3.0, 8.0), (3.0, 1.83)) = \sqrt{(-3.0 - 3.0)^2 + ( 8.0 - 1.83)^2} = 8.61$$
$$dist((-3.0, 8.0), (-2.25, 9.25)) = \sqrt{(-3.0 - -2.25)^2 + ( 8.0 - 9.25)^2} = 1.46$$
En Yakın Uzaklik: 1.46

En Yakın Ortalama: [-2.25  9.25]

Cluster: 1
___
$$x = (-0.0, 10.0)$$
$$dist((-0.0, 10.0), (3.0, 1.83)) = \sqrt{(-0.0 - 3.0)^2 + ( 10.0 - 1.83)^2} = 8.7$$
$$dist((-0.0, 10.0), (-2.25, 9.25)) = \sqrt{(-0.0 - -2.25)^2 + ( 10.0 - 9.25)^2} = 2.37$$
En Yakın Uzaklik: 2.37

En Yakın Ortalama: [-2.25  9.25]

Cluster: 1
___
$$x = (3.0, 2.0)$$
$$dist((3.0, 2.0), (3.0, 1.83)) = \sqrt{(3.0 - 3.0)^2 + ( 2.0 - 1.83)^2} = 0.17$$
$$dist((3.0, 2.0), (-2.25, 9.25)) = \sqrt{(3.0 - -2.25)^2 + ( 2.0 - 9.25)^2} = 8.95$$
En Yakın Uzaklik: 0.17

En Yakın Ortalama: [3.   1.83]

Cluster: 0
___
$$x = (-3.0, 9.0)$$
$$dist((-3.0, 9.0), (3.0, 1.83)) = \sqrt{(-3.0 - 3.0)^2 + ( 9.0 - 1.83)^2} = 9.35$$
$$dist((-3.0, 9.0), (-2.25, 9.25)) = \sqrt{(-3.0 - -2.25)^2 + ( 9.0 - 9.25)^2} = 0.79$$
En Yakın Uzaklik: 0.79

En Yakın Ortalama: [-2.25  9.25]

Cluster: 1
___
$$x = (3.0, -0.0)$$
$$dist((3.0, -0.0), (3.0, 1.83)) = \sqrt{(3.0 - 3.0)^2 + ( -0.0 - 1.83)^2} = 1.83$$
$$dist((3.0, -0.0), (-2.25, 9.25)) = \sqrt{(3.0 - -2.25)^2 + ( -0.0 - 9.25)^2} = 10.64$$
En Yakın Uzaklik: 1.83

En Yakın Ortalama: [3.   1.83]

Cluster: 0
___
$$x = (5.0, -0.0)$$
$$dist((5.0, -0.0), (3.0, 1.83)) = \sqrt{(5.0 - 3.0)^2 + ( -0.0 - 1.83)^2} = 2.71$$
$$dist((5.0, -0.0), (-2.25, 9.25)) = \sqrt{(5.0 - -2.25)^2 + ( -0.0 - 9.25)^2} = 11.75$$
En Yakın Uzaklik: 2.71

En Yakın Ortalama: [3.   1.83]

Cluster: 0
___
$$x = (-2.0, 6.0)$$
$$dist((-2.0, 6.0), (3.0, 1.83)) = \sqrt{(-2.0 - 3.0)^2 + ( 6.0 - 1.83)^2} = 6.51$$
$$dist((-2.0, 6.0), (-2.25, 9.25)) = \sqrt{(-2.0 - -2.25)^2 + ( 6.0 - 9.25)^2} = 3.26$$
En Yakın Uzaklik: 3.26

En Yakın Ortalama: [-2.25  9.25]

Cluster: 1
___
$$x = (-3.0, 10.0)$$
$$dist((-3.0, 10.0), (3.0, 1.83)) = \sqrt{(-3.0 - 3.0)^2 + ( 10.0 - 1.83)^2} = 10.14$$
$$dist((-3.0, 10.0), (-2.25, 9.25)) = \sqrt{(-3.0 - -2.25)^2 + ( 10.0 - 9.25)^2} = 1.06$$
En Yakın Uzaklik: 1.06

En Yakın Ortalama: [-2.25  9.25]

Cluster: 1
___
$$x = (7.0, 2.0)$$
$$dist((7.0, 2.0), (3.0, 1.83)) = \sqrt{(7.0 - 3.0)^2 + ( 2.0 - 1.83)^2} = 4.0$$
$$dist((7.0, 2.0), (-2.25, 9.25)) = \sqrt{(7.0 - -2.25)^2 + ( 2.0 - 9.25)^2} = 11.75$$
En Yakın Uzaklik: 4.0

En Yakın Ortalama: [3.   1.83]

Cluster: 0
___
Kümelerin güncellenmiş halleri:
|    |   x_1 |   x_2 |   cluster |
|---:|------:|------:|----------:|
|  0 |     2 |     1 |         0 |
|  1 |    -3 |     8 |         1 |
|  2 |    -0 |    10 |         1 |
|  3 |     3 |     2 |         0 |
|  4 |    -3 |     9 |         1 |
|  5 |     3 |    -0 |         0 |
|  6 |     5 |    -0 |         0 |
|  7 |    -2 |     6 |         1 |
|  8 |    -3 |    10 |         1 |
|  9 |     7 |     2 |         0 |
___
* 0. küme için ortalama hesabı:
$$x_1=\frac{2+3+3+5+7}{5} = \frac{20}{5} = 4$$
$$x_2=\frac{1+2-0-0+2}{5} = \frac{5}{5} = 1$$

* 1. küme için ortalama hesabı:
$$x_1=\frac{-3-0-3-2-3}{5} = \frac{-11}{5} = -2.2$$
$$x_2=\frac{8+10+9+6+10}{5} = \frac{43}{5} = 8.6$$

___
Yeni ortalamalarım:
|    |   x_1 |   x_2 |
|---:|------:|------:|
|  0 |   4   |   1   |
|  1 |  -2.2 |   8.6 |
___
4. iterasyon
___
$$x = (2.0, 1.0)$$
$$dist((2.0, 1.0), (4.0, 1.0)) = \sqrt{(2.0 - 4.0)^2 + ( 1.0 - 1.0)^2} = 2.0$$
$$dist((2.0, 1.0), (-2.2, 8.6)) = \sqrt{(2.0 - -2.2)^2 + ( 1.0 - 8.6)^2} = 8.68$$
En Yakın Uzaklik: 2.0

En Yakın Ortalama: [4. 1.]

Cluster: 0
___
$$x = (-3.0, 8.0)$$
$$dist((-3.0, 8.0), (4.0, 1.0)) = \sqrt{(-3.0 - 4.0)^2 + ( 8.0 - 1.0)^2} = 9.9$$
$$dist((-3.0, 8.0), (-2.2, 8.6)) = \sqrt{(-3.0 - -2.2)^2 + ( 8.0 - 8.6)^2} = 1.0$$
En Yakın Uzaklik: 1.0

En Yakın Ortalama: [-2.2  8.6]

Cluster: 1
___
$$x = (-0.0, 10.0)$$
$$dist((-0.0, 10.0), (4.0, 1.0)) = \sqrt{(-0.0 - 4.0)^2 + ( 10.0 - 1.0)^2} = 9.85$$
$$dist((-0.0, 10.0), (-2.2, 8.6)) = \sqrt{(-0.0 - -2.2)^2 + ( 10.0 - 8.6)^2} = 2.61$$
En Yakın Uzaklik: 2.61

En Yakın Ortalama: [-2.2  8.6]

Cluster: 1
___
$$x = (3.0, 2.0)$$
$$dist((3.0, 2.0), (4.0, 1.0)) = \sqrt{(3.0 - 4.0)^2 + ( 2.0 - 1.0)^2} = 1.41$$
$$dist((3.0, 2.0), (-2.2, 8.6)) = \sqrt{(3.0 - -2.2)^2 + ( 2.0 - 8.6)^2} = 8.4$$
En Yakın Uzaklik: 1.41

En Yakın Ortalama: [4. 1.]

Cluster: 0
___
$$x = (-3.0, 9.0)$$
$$dist((-3.0, 9.0), (4.0, 1.0)) = \sqrt{(-3.0 - 4.0)^2 + ( 9.0 - 1.0)^2} = 10.63$$
$$dist((-3.0, 9.0), (-2.2, 8.6)) = \sqrt{(-3.0 - -2.2)^2 + ( 9.0 - 8.6)^2} = 0.89$$
En Yakın Uzaklik: 0.89

En Yakın Ortalama: [-2.2  8.6]

Cluster: 1
___
$$x = (3.0, -0.0)$$
$$dist((3.0, -0.0), (4.0, 1.0)) = \sqrt{(3.0 - 4.0)^2 + ( -0.0 - 1.0)^2} = 1.41$$
$$dist((3.0, -0.0), (-2.2, 8.6)) = \sqrt{(3.0 - -2.2)^2 + ( -0.0 - 8.6)^2} = 10.05$$
En Yakın Uzaklik: 1.41

En Yakın Ortalama: [4. 1.]

Cluster: 0
___
$$x = (5.0, -0.0)$$
$$dist((5.0, -0.0), (4.0, 1.0)) = \sqrt{(5.0 - 4.0)^2 + ( -0.0 - 1.0)^2} = 1.41$$
$$dist((5.0, -0.0), (-2.2, 8.6)) = \sqrt{(5.0 - -2.2)^2 + ( -0.0 - 8.6)^2} = 11.22$$
En Yakın Uzaklik: 1.41

En Yakın Ortalama: [4. 1.]

Cluster: 0
___
$$x = (-2.0, 6.0)$$
$$dist((-2.0, 6.0), (4.0, 1.0)) = \sqrt{(-2.0 - 4.0)^2 + ( 6.0 - 1.0)^2} = 7.81$$
$$dist((-2.0, 6.0), (-2.2, 8.6)) = \sqrt{(-2.0 - -2.2)^2 + ( 6.0 - 8.6)^2} = 2.61$$
En Yakın Uzaklik: 2.61

En Yakın Ortalama: [-2.2  8.6]

Cluster: 1
___
$$x = (-3.0, 10.0)$$
$$dist((-3.0, 10.0), (4.0, 1.0)) = \sqrt{(-3.0 - 4.0)^2 + ( 10.0 - 1.0)^2} = 11.4$$
$$dist((-3.0, 10.0), (-2.2, 8.6)) = \sqrt{(-3.0 - -2.2)^2 + ( 10.0 - 8.6)^2} = 1.61$$
En Yakın Uzaklik: 1.61

En Yakın Ortalama: [-2.2  8.6]

Cluster: 1
___
$$x = (7.0, 2.0)$$
$$dist((7.0, 2.0), (4.0, 1.0)) = \sqrt{(7.0 - 4.0)^2 + ( 2.0 - 1.0)^2} = 3.16$$
$$dist((7.0, 2.0), (-2.2, 8.6)) = \sqrt{(7.0 - -2.2)^2 + ( 2.0 - 8.6)^2} = 11.32$$
En Yakın Uzaklik: 3.16

En Yakın Ortalama: [4. 1.]

Cluster: 0
___
Kümelerin tablosu fakat bir öncekisiyle aynı:
|    |   x_1 |   x_2 |   cluster |
|---:|------:|------:|----------:|
|  0 |     2 |     1 |         0 |
|  1 |    -3 |     8 |         1 |
|  2 |    -0 |    10 |         1 |
|  3 |     3 |     2 |         0 |
|  4 |    -3 |     9 |         1 |
|  5 |     3 |    -0 |         0 |
|  6 |     5 |    -0 |         0 |
|  7 |    -2 |     6 |         1 |
|  8 |    -3 |    10 |         1 |
|  9 |     7 |     2 |         0 |
___
* 0. küme için ortalama hesabı:

$$x_1=\frac{2+3+3+5+7}{5} = \frac{20}{5} = 4$$
$$x_2=\frac{1+2-0-0+2}{5} = \frac{5}{5} = 1$$

* 1. küme için ortalama hesabı:
$$x_1=\frac{-3-0-3-2-3}{5} = \frac{-11}{5} = -2.2$$
$$x_2=\frac{8+10+9+6+10}{5} = \frac{43}{5} = 8.6$$
___
Ortalamalarım (bir öncekisi ile aynı):
|    |   x_1 |   x_2 |
|---:|------:|------:|
|  0 |   4   |   1   |
|  1 |  -2.2 |   8.6 |

Bu noktadan sonra iterasyon durur. Veriler artık değişmediği için K-Means Clustering algoritması kümeleme sonucunu yukarıdaki elde ettiğimiz son tablo olarak gösterir ve kümelerimizin son ortalamaları yine son bulduğumuz tablodadır.
___

## Varsayımlar
* Veriler mutlaka nicel olmak zorundadır. Kategorik değişkenler $D$-boyutlu uzayda bir noktayı temsil etmediği için centroid'lere olan uzaklıkları hesaplanamaz. Bu yüzden veriler nicel (sayısal) olmak zorundadır.

* Algoritmanın anlamlı olabilmesi için $k > 1$ olmalıdır.

## Optimal $k$ Değeri
Optimal $k$ değeri verilerin nasıl olduğuna göre ve kaça ayırmak istenildiğine göre değişebilir. Deterministik olarak optimal bir $k$ değeri seçmek diye bir durum yoktur. Verinin, kaç kümeye ayrılması isteniyorsa seçilmesi gereken $k$ değeri odur. Ancak eğer verinin kaç kümeye ayrılması gerektiği hakkında bilgi sahibi olunmadığı durumda, verileri en tutarlı şekilde kümelemek için izlenilen methodlar vardır. 

### Elbow Method
Elbow Method'u K-Means Clustering algoritması için kullanılacak en uygun küme sayısını belirlemek için yaygın olarak kullanılır. 

İki boyutlu uzayda yatay eksen kümelerin sayısını simgeleyen doğal sayılar ile numaralandırılır: $k = 1, 2, ..., n$. Dikey eksen uzaklık mesafesini simgeleyen eksendir. 

İlk olarak $k=1$ için hataların karelerinin toplamı maximumdur çünkü sadece 1 küme vardır ve bütün $x$ değerleri o kümenin elemanıdır. $k=n$ ($n$ verilerin sayısı olmak üzere) için ise hataların karelerin toplamı 0'a doğru gider fakat hataların karelerinin toplamını minimum yapmak için $n$ tane küme almak herbir verinin kendi kümesi olması anlamına gelmektedir ve anlamı yoktur. Bu sebeple amaç hataların hem karelerinin toplamının hem de küme sayısının ($k$) optimal olacak şekilde belirlenmesidir. İki değerinde anlamlı olacak şekilde en az değeri alması optimal noktadır. Bu nokta çoğu zaman 2-boyutlu uzayda çizilen grafikte bir kırılma olarak görülür. Bu kırılma noktası bir dirseği anımsatır. Bu yüzden yöntemin ismi Elbow verilmiştir.

## Dikkat Edilmesi Gereken Durumlar
### Uç Değerlere Sahip Olan Veri Setini Kümeleme
Uç değerler, veri setindeki diğer verilerden çok farklı olan veri noktalarıdır. K-Means Clustering algoritması uç değerlere duyarlı bir algoritmadır ve performansı olumsuz etkileyebilir. 

Uç değerler, verinin alt yapısını temsil etmeyen kümeler üretmesine ve yanlış veya optimal olmayan sonuçlara yol açabilir. Bu sonuçları kümelerin ortalamasını (centroid'leri) istenmeyen yerlere çekerek yapar. 

K-Means Clustering algoritması için verilerin ağırlıkları yoktur. Her veri aynı şekilde değerlendirilir. Bu yüzden bazı verilerin kümenin diğer elemanlarından uç noktalarda olması, küme ortalamasını etkiler.

### Verilerin Ölçeklendirilmesi
Ölçeklendirme veri setindeki değişkenlerin birbirlerine oranının değiştirilmesiyle olur. Verilerin birbirlerine oranı değişirken dağılımı değişmez.

Bazen verilerin arasında anlamlı bir fark olmaz fakat $D$-boyutlu uzayda verilerin arasındaki fark önemli olarak görülür. Böyle durumlarda ölçeklendirme kullanılabilir.

### Kümelemek İstenilen Verilerin Doğrusal Olarak Kümelenememesi
Veriler doğrusal olarak kümelenmeye uygun değilse, K-Means Clustering algoritması istenilen sonuçları veremeyebilir.

### Boyut İndirgeme
K-Means Clustering algoritmasının boyut sınırı yoktur fakat gerek görülürse boyutları indirgenebilir. Veri kümesinin boyutlarını K-Means Clustering algoritmasını uygulamadan önce azaltmanın bazı faydaları şunlardır:
* Daha hızlı hesaplama süresi: Eğer veri kümemizdeki boyutlar azalırsa işlem yükümüz hafifleyeceğinden süreç hızlanır. Elimizde yüksek boyutlu ve büyük veriler varsa zamandan tasaruf etmek için kullanılması uygun olur.
* Bazı durumlarda veri setindeki kirlilik yaratan gürültüleri ortadan kaldırmamıza yardımcı olur. Bu sayede daha doğru kümeleme sonucu alabiliriz.
* Görselleştirme: Eğer verilerimiz 4. veya daha yüksek boyutlarda ise veya diğer bir söylemle 4 veya daha fazla bağımlı değişkene (features) sahipsek verileri görselleştirmemiz imkansızdır. Bu verilerin boyutunu 4. boyuttan aşağı çekerek görselleştirmemiz mümkün hale gelir.

## Avantajları ve Dezavantajları
K-Means Clustering algoritmasının avantajları basit ve hızlı olmasıdır. Büyük verilerde verimli bir şekilde çalışabilir. Veri noktalarının sırasına duyarlı değildir.

Dezavantajları ise başlangıç ortalamalarının bazen yanlış sonuçlar verebilecek şekilde alınmasıdır. Bu sorun K-Means Clustering algoritmasını birkaç kez çalıştırdığımızda büyük oranda ortadan kalkar. Diğer dezavantaj ise verilerin doğrusal olarak kümelenmemesi gereken veri setlerinde çok etkili değildir. Bu K-Means kullanım alanını, sadece doğrusal olarak ayrılabilen veri setleriyle kısıtlar. Ayrıca çok büyük verilerde (örneğin render işlemlerinde) bellek sınırına takılabilir.

# Kaynakça

Edouard Duchesnay, Tommy Löfstedt (May 16, 2019). Statistics and Machine Learning in
Python Release 0.2 (pp. 159-163)

Scikit learn, KMeans, https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html

"(ML 16.1) K-means clustering (part 1)". (Jul 10, 2011). mathematicalmonk. Youtube. Erişim tarihi: 1 Aralık 2022. https://www.youtube.com/watch?v=0MQEt10e4NM

"(ML 16.2) K-means clustering (part 2)". (Jul 11, 2011). mathematicalmonk. Youtube. Erişim tarihi: 1 Aralık 2022. https://www.youtube.com/watch?v=4shfFAArxSc

"K-means Clustering". (Jan 19, 2014). Victor Lavrenko. Youtube. Erişim tarihi: 29 Kasım 2022. https://www.youtube.com/watch?v=mHl5P-qlnCQ&list=PLBv09BD7ez_6cgkSUAqBXENXEhCkb_2wl

C. Piech, "K-Means Clustering", Stanford University. Erişim tarihi: 2022 Aralık 4. https://stanford.edu/~cpiech/cs221/handouts/kmeans.html

"Lecture 60 — The k Means Algorithm | Stanford University". (Apr 13, 2016). 
Artificial Intelligence - All in One. Youtube. Erişim tarihi: 28 Kasım 2022. https://www.youtube.com/watch?v=RD0nNK51Fp8&t=513s

"K-means & Image Segmentation - Computerphile". (Sep 14, 2016). K-means & Image Segmentation - Computerphile. https://www.youtube.com/watch?v=yR7k19YBqiw

Stavrey, Stefan. Machine Learning God. (2017), 11.1 (K-Means clustering) ve 12.1 (Principal component analysis (PCA)) bölümleri.

OpenAI. (2022). Assistant isimli makine öğrenmesi modeli. Erişim tarihi: 03 Aralık 2022.