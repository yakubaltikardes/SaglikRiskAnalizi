# Sağlık Risk Analizi

Bu proje, hastaların yaş, vücut kitle indeksi (BKİ) ve günlük adım sayısı gibi temel fiziksel özelliklerini kullanarak tansiyon kaynaklı **risk seviyelerini** tahmin eden bir makine öğrenmesi projesidir.

## Proje Özeti

Projenin temel amacı, ölçülmesi zaman veya cihaz gerektiren tansiyon değerlerini (Sistolik ve Diyastolik), kişilerin kolayca elde edilebilen günlük metrikleri (Yaş, BKİ, Adım Sayısı) üzerinden tahmin edebilmektir. 

Bu doğrultuda:
1. Hastaların tansiyon değerleri üzerinden sistolik ve diyastolik risk durumları hesaplanmıştır.
2. Bu iki risk toplanarak **Hedef Değişken (Risk Seviyesi: 0, 1 veya 2)** elde edilmiştir.
3. 10'dan fazla makine öğrenmesi algoritması eğitilmiş ve başarı oranları karşılaştırılmıştır.
4. En başarılı model üzerinde hiperparametre optimizasyonu (GridSearchCV) uygulanmıştır.

## Veri Seti (`Hastalar.csv`)

Veri seti 2000 hastaya ait sentetik/anonimleştirilmiş sağlık kayıtlarından oluşmaktadır. 

**Kullanılan Özellikler (Bağımsız Değişkenler - X):**
* `Yaş`: Hastanın yaşı
* `BKİ`: Vücut Kitle İndeksi
* `Günlük_Adım_Sayısı`: Hastanın günlük ortalama adım sayısı

**Risk Hesaplamasında Kullanılan Değişkenler:**
* `Sistolik_Tansiyon`: Büyük tansiyon (>120 ise riskli kabul edildi)
* `Diyastolik_Tansiyon`: Küçük tansiyon (>80 ise riskli kabul edildi)

##  Kullanılan Teknolojiler ve Kütüphaneler

* **Dil:** Python
* **Veri Manipülasyonu:** Pandas, NumPy
* **Veri Görselleştirme:** Seaborn, Matplotlib
* **Makine Öğrenmesi (Scikit-Learn):** KNN, Logistic Regression, SVC, MLP, Decision Tree, Random Forest, Gradient Boosting
* **Gelişmiş Algoritmalar:** XGBoost, LightGBM, CatBoost
* **Optimizasyon:** GridSearchCV, StandardScaler

##  Model Geliştirme Süreci

1. **Veri Ön İşleme:** Eksik veriler (`dropna`) temizlendi. Özellikler standartlaştırma (StandardScaler) işlemine tabi tutuldu.
2. **Model Eğitimi:** Veri %75 eğitim, %25 test seti olarak ayrıldı. 11 farklı sınıflandırma modeli standart parametreleriyle eğitildi.
3. **Değerlendirme:** Modellerin doğruluk (Accuracy) oranları hesaplandı ve Seaborn kullanılarak görselleştirildi.
4. **Optimizasyon:** Baz modeller arasında en yüksek doğruluğa ulaşan **Support Vector Classifier (SVC)** seçildi. GridSearchCV ile farklı `C` ve `kernel` parametreleri denenerek en iyi hiperparametreler (`C=100`, `kernel='linear'`) bulundu.

##  Sonuçlar

Yapılan hiperparametre optimizasyonu sonucunda, Support Vector Machine (SVC) modeli test verisi üzerinde **%74.8** doğruluk (accuracy) oranına ulaşmıştır. 

##  Nasıl Çalıştırılır?

Projeyi kendi bilgisayarınızda çalıştırmak için aşağıdaki adımları izleyebilirsiniz:

1. Repoyu Klonlayın
```bash
   git clone [https://github.com/yakubaltikardes/SaglikRiskAnalizi.git](https://github.com/yakubaltikardes/SaglikRiskAnalizi.git)
2. Gerekli kütüphaneleri yükleyin
       ```bash
       pip install numpy pandas seaborn matplotlib scikit-learn xgboost lightgbm catboost

3. Jupyter Notebook'u başlatın ve Model.ipynb dosyasını çalıştırın
        ```
        jupyter notebook
        
Not: Hastalar.csv dosyasının notebook ile aynı dizinde bulunduğundan emin olun.
