# Akbank Derin Öğrenme Bootcamp-Brain-Tumor-MR-Classification
Ilgın Kaya Akbank Derin Öğrenme Bootcamp Brain Tumor MR Classification Proje Reposu
# Brain Tumor MRI Classification — CNN & Transfer Learning

Bu proje, **Akbank Derin Öğrenme Bootcamp** kapsamında geliştirilmiştir.  
Amaç: MRI görüntülerinden beyin tümörlerini sınıflandırmaktıe.  

## Veri Seti
- Kullanılan veri seti: [Brain Tumor MRI Dataset](https://www.kaggle.com/datasets)  
- Sınıflar:
  - **Glioma**
  - **Meningioma**
  - **Pituitary**
  - **No Tumor**

Veri seti `Training/` ve `Testing/` klasörlerine ayrılmıştır. Eğitim setinden %15 oranında doğrulama (validation) ayrılmıştır.



##  Yöntemler
Projede iki farklı yaklaşım uygulanmıştır:

1. **Baseline CNN**  
   - 3 adet Conv2D + MaxPooling blok  
   - Dense (128) + Dropout(0.4) + Softmax  
   - Amaç: Referans doğruluk elde etmek  

2. **Transfer Learning (EfficientNetB0)**  
   - ImageNet ile önceden eğitilmiş EfficientNetB0  
   - İki aşamalı eğitim: *Freeze* ve *Fine-tune*  
   - Amaç: Daha yüksek doğruluk ve genellenebilirlik  



##  Metrikler ve Sonuçlar
- **Baseline CNN**
  - Test doğruluğu: ~%74  
  - Meningioma sınıfında düşük recall  
- **EfficientNetB0 (Fine-tuned)**
  - Test doğruluğu: ~%88  
  - ROC-AUC (macro): **0.9835**  
  - ROC-AUC (weighted): **0.984**  
  - En başarılı sınıflar: *No Tumor* ve *Pituitary*  
  - En zayıf sınıf: *Meningioma* (recall düşük)  

Model değerlendirmelerinde kullanılan metrikler:
- Accuracy & Loss grafikleri  
- Confusion Matrix  
- Classification Report  
- ROC-AUC skorları  
- Grad-CAM görselleştirmeleri  



##  Hata Analizi
- **Meningioma sınıfında** model hataları belirgin.  
- Çoğunlukla *pituitary* veya *no_tumor* sınıfları ile karışıyor.  
- Çözüm önerileri:  
  - Daha fazla meningioma verisi eklemek  
  - Kontrast/brightness odaklı augmentasyonlar  
  - Daha uzun fine-tuning  



##  Ekler
- **TensorBoard** entegrasyonu ile eğitim süreci izlendi.  
- Hiperparametre denemeleri (dropout, dense units, kernel size, optimizer, batch size) yapıldı.  
- Bonus: Grad-CAM ile modelin odaklandığı bölgeler görselleştirildi.  



##  Sonuç ve Gelecek Çalışmalar
Bu proje sonucunda:  
- Baseline CNN → referans doğruluk  
- Transfer Learning → daha yüksek doğruluk, güçlü genelleme  
- ROC-AUC skorları → modelin sınıfları ayırt etmede başarılı olduğunu doğruladı  

**Gelecek çalışmalar için:**  
- Veri artırma (data augmentation) yöntemlerini çeşitlendirmek  
- Daha farklı transfer learning modelleri denemek (ResNet, DenseNet)  
- Modeli bir arayüz ile deploy etmek (ör. Streamlit, Gradio)  
- Gerçek zamanlı MRI verisi üzerinde denemeler yapmak  



##  Linkler
- [Kaggle Notebook — Brain Tumor MRI Classification](https://www.kaggle.com/code/username/brain-tumor-mri-classification)  
- [Kaggle Dataset](https://www.kaggle.com/datasets)  


