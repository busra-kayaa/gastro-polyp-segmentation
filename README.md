# 🧬 Gastrointestinal Polip Segmentasyonu: Geliştirilmiş U-Net Yaklaşımı

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

> **⚠️ ÖNEMLİ NOT:** GitHub, büyük `.ipynb` dosyalarını görüntülerken bazen hata verebilir ("Unable to render code block"). Eğer notebook dosyasını görüntüleyemiyorsanız, lütfen aşağıdaki butona tıklayarak **nbviewer** üzerinden sorunsuz bir şekilde inceleyin:
>
> [![nbviewer](https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg)](https://nbviewer.org/github/busra-kayaa/gastro-polyp-segmentation/blob/main/segmentasyon.ipynb)

---

## 📋 Proje Hakkında

Kolorektal kanser, erken teşhis edildiğinde önlenebilen ve tedavi edilebilen bir hastalıktır. Polip tespiti bu sürecin en kritik parçasıdır. Bu proje, **Kvasir-SEG** veri setini kullanarak endoskopi görüntülerinden gastrointestinal polipleri otomatik olarak tespit etmek ve segmente etmek (sınırlarını çizmek) amacıyla geliştirilmiştir.

Çalışmada, klasik U-Net mimarisi **Batch Normalization** ve **Dropout** katmanları ile güçlendirilmiş, veri setindeki sınıf dengesizliği sorunu ise **Dice Loss** fonksiyonu kullanılarak çözülmüştür.

---

## 💾 Veri Seti

Bu projede kullanılan veri seti açık kaynaklıdır ve aşağıdaki bağlantılardan erişilebilir:

* **Veri Seti Adı:** Kvasir-SEG
* **İndirme Linki (Kaggle):** [Kvasir-SEG: A Segmented Polyp Dataset](https://www.kaggle.com/datasets/debeshjha1/kvasirseg)
* **İçerik:** 1000 adet endoskopi görüntüsü ve bunlara karşılık gelen uzman maskeleri.

---

## 🚀 Kullanılan Teknikler ve Yöntemler

Bu projede yüksek doğruluk elde etmek için aşağıdaki stratejiler izlenmiştir:

* **Model Mimarisi:** Geliştirilmiş U-Net (Encoder-Decoder yapısı, Skip Connections, Batch Norm, Dropout).
* **Kayıp Fonksiyonu (Loss Function):** Sınıf dengesizliğini (Arka plan >> Polip) yönetmek için **Dice Loss** tercih edilmiştir.
* **Gelişmiş Ön İşleme (Preprocessing):**
    * **CLAHE:** Görüntü kontrastını artırmak için.
    * **Gamma Düzeltmesi:** Karanlık bölgeleri aydınlatmak için.
    * **Gürültü Giderme:** `FastNlMeansDenoising` ile görüntü temizliği.
    * **Normalizasyon:** Piksel değerlerinin [0, 1] aralığına çekilmesi.

---

## 📊 Performans Sonuçları

Model, eğitim sürecinde hiç görmediği **Test Seti (150 Görüntü)** üzerinde aşağıdaki performansı sergilemiştir:

| Performans Metriği | Başarı Skoru | Açıklama |
| :--- | :--- | :--- |
| **Dice Katsayısı (F1)** | **0.7770** | Segmentasyon başarısının temel ölçütü. |
| **Specificity** | **0.9739** | Sağlıklı dokuyu ayırt etme başarısı (Çok Yüksek). |
| **Sensitivity (Recall)** | **0.7914** | Mevcut polipleri tespit etme oranı. |
| **IoU (Jaccard)** | **0.6874** | Tahmin ile gerçeğin örtüşme oranı. |
| **Accuracy** | **0.9389** | Genel piksel doğruluğu. |



## 🛠️ Kurulum ve Çalıştırma

Projeyi yerel bilgisayarınızda çalıştırmak için aşağıdaki adımları izleyebilirsiniz:

1.  **Repository'yi klonlayın:**
    ```bash
    git clone [https://github.com/busra-kayaa/gastro-polyp-segmentation.git](https://github.com/busra-kayaa/gastro-polyp-segmentation.git)
    cd gastro-polyp-segmentation
    ```

2.  **Gerekli kütüphaneleri yükleyin:**
    ```bash
    pip install tensorflow opencv-python matplotlib pandas seaborn albumentations
    ```

3.  **Projeyi Çalıştırın:**
    `segmentasyon.ipynb` dosyasını Jupyter Notebook veya Google Colab ile açarak tüm hücreleri sırasıyla çalıştırabilirsiniz.

---
