HyperLogLog Implementation in Java

Bu proje, büyük veri setlerinde **benzersiz eleman sayısını (cardinality estimation)** çok düşük bellek kullanımıyla tahmin etmeye yarayan **HyperLogLog (HLL)** algoritmasının Java uygulamasını içerir.



  Proje Hakkında
HyperLogLog, milyarlarca veriyi %1 civarında bir hata payıyla, Gigabaytlar yerine sadece birkaç Kilobayt RAM kullanarak saymamızı sağlayan olasılıksal bir algoritmadır.

 Kullanılan Teknolojiler ve Araçlar
* **Dil:** Java 8+
* **IDE:** [Buraya kullandığın IDE'yi yaz, örn: IntelliJ IDEA]
* **Yapay Zeka Desteği:** Algoritma analizi, optimizasyon ve dokümantasyon sürecinde **Google Gemini** modeli asistan olarak kullanılmıştır.

---

 HLL Ne İşe Yarar?
Geleneksel yöntemlerde (HashSet gibi), her benzersiz öğeyi hafızada tutmanız gerekir. Bu da $O(N)$ alan karmaşıklığı demektir. **HLL** ise:
* Veriyi saklamaz, verinin hash değerindeki bit dağılımını analiz eder.
* Alan karmaşıklığını $O(\log(\log N))$ seviyesine indirir.
* **Kullanım Alanları:** Web sitesi tekil ziyaretçi sayısı, veritabanı sorgu optimizasyonu, büyük ölçekli veri analitiği.

---

 Algoritma Analizi
Algoritmanın performansı hem teorik hem de deneysel (ampirik) olarak doğrulanmıştır:

| Parametre | Değer / Karmaşıklık |
| :--- | :--- |
| **Zaman Karmaşıklığı (Ekleme)** | $O(1)$ |
| **Alan Karmaşıklığı** | $O(m)$ (Sabit ve düşük) |
| **Hata Payı Formülü** | $\sigma \approx 1.04 / \sqrt{m}$ |
| **Hash Fonksiyonu** | MurmurHash3 & FNV-1a |

 Kodun Çıktı Analizi
Program çalıştırıldığında şu senaryoları test eder:
1. **Küçük Veri Seti:** "Linear Counting" ile düşük sayılarda tam sonuç.
2. **Büyük Veri (100.000):** %0.81 teorik hata sınırının altında gerçekleşen başarılı tahminler.
3. **Merge (Birleştirme):** İki farklı HLL nesnesinin veriyi kaybetmeden birleşimi.
4. **Hata/Bellek Dengesi:** Farklı $b$ değerleri için hata oranlarının karşılaştırmalı analizi.

