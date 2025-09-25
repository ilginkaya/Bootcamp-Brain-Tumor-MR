# Akbank Derin Öğrenme Bootcamp-Brain-Tumor-MR-Classification
Ilgın Kaya Akbank Derin Öğrenme Bootcamp Brain Tumor MR Classification Proje Reposu
# Brain Tumor MRI Classification — CNN & Transfer Learning

Bu proje, **Akbank Derin Öğrenme Bootcamp** kapsamında geliştirilmiştir.  
Amaç: MRI görüntülerinden beyin tümörlerini sınıflandırmaktıe.  

##  Veri Seti
- Kullanılan veri seti: [Brain Tumor MRI Dataset](https://www.kaggle.com/datasets)  
- Dört sınıf içermektedir:  
  - **Glioma**  
  - **Meningioma**  
  - **Pituitary**  
  - **No Tumor**  

Veri seti `Training/` ve `Testing/` klasörlerine ayrılmıştır.  
Eğitim setinden %15 oranında **validation** ayrımı yapılmıştır (stratified). 




##  Yöntemler
Projede iki farklı yaklaşım denenmiştir:  

1. **Baseline CNN (Referans Model)**  
   - 3 blok: Conv2D → BatchNorm → ReLU → MaxPooling  
   - Dense(128) + Dropout(0.4) + Softmax  
   - Amaç: Basit bir CNN ile başlangıç doğruluğu elde etmek  

2. **Transfer Learning (EfficientNetB0)**  
   - ImageNet ile önceden eğitilmiş EfficientNetB0 tabanı  
   - İki aşamalı eğitim:  
     - *Freeze*: yalnız üst katmanlar eğitildi  
     - *Fine-tune*: taban açılarak düşük öğrenme oranıyla yeniden eğitildi  
   - Amaç: Daha yüksek doğruluk ve güçlü genelleme sağlamak  


##  Metrikler ve Sonuçlar
- **Baseline CNN**
  - Test doğruluğu: ~%74  
  - Meningioma sınıfında düşük recall (en zorlayıcı sınıf)  

- **EfficientNetB0 (Fine-tuned)**
  - Test doğruluğu: ~%88  
  - ROC-AUC (macro): **0.9835**  
  - ROC-AUC (weighted): **0.984**  
  - En başarılı sınıflar: *No Tumor* ve *Pituitary*  
  - Görece zayıf kalan sınıf: *Meningioma*  

Modelin değerlendirilmesinde:  
- Accuracy & Loss grafikleri  
- Confusion Matrix  
- Classification Report  
- ROC-AUC skorları  
- Grad-CAM görselleştirmeleri  
kullanılmıştır. 



##  Hata Analizi
- **Meningioma sınıfı**, diğer sınıflarla en çok karışan sınıftır.  
- Bazı örnekler *pituitary*, bazıları ise *no_tumor* olarak tahmin edilmiştir.  
- Olası çözüm yolları:  
  - Daha fazla meningioma verisi eklemek  
  - Kontrast/brightness odaklı augmentasyonlar  
  - Daha uzun fine-tuning veya farklı transfer learning modelleri denemek  




##  Ekler
- **TensorBoard entegrasyonu** ile eğitim süreci izlendi.  
- **Hiperparametre denemeleri** yapıldı (dropout, dense units, kernel size, optimizer, batch size).  
- **Grad-CAM** kullanılarak modelin karar verirken hangi bölgeleri dikkate aldığı görselleştirildi.  



##  Sonuç ve Gelecek Çalışmalar
- Baseline CNN → referans doğruluk sağladı (~%74).  
- Transfer Learning → doğruluk %88’e ulaştı, genelleme gücü arttı.  
- ROC-AUC skorları (~0.98) → modelin sınıfları ayırt etmede çok başarılı olduğunu gösterdi.

  
**Gelecek çalışmalar için:**  
- Veri artırma (data augmentation) yöntemlerini çeşitlendirmek  
- Alternatif transfer learning modelleri (ResNet, DenseNet) denemek  
- Basit bir arayüzle (Streamlit/Gradio) deploy etmek  
- Gerçek zamanlı MRI verileri üzerinde denemeler yapmak   



##  Linkler
- https://www.kaggle.com/code/ilgnkaya/bootcamp-brain-tumor-mr 


