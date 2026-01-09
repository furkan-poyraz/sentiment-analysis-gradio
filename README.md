# 🤖 Türkçe Duygu Analizi - BERTurk

Türkçe metinlerde olumlu/olumsuz duygu sınıflandırması yapan BERT tabanlı model.

## 📊 Hızlı Bilgi

- **Model:** BERTurk & XLM-RoBERTa
- **En İyi Performans:** XLM-RoBERTa (%92.6 accuracy)
- **Veri:** Türkçe Twitter yorumları
- **Arayüz:** Gradio

## 🚀 Kullanım

1. Google Colab'da aç
2. Runtime > GPU (T4) seç
3. Hücreleri sırayla çalıştır
4. Gradio arayüzünde test et

## 📈 Sonuçlar

| Model | Accuracy | F1-Score |
|-------|----------|----------|
| BERTurk | %85.5 | %85.5 |
| XLM-RoBERTa | %92.6 | %92.6 |

## 💬 Örnek Kullanım

**Olumlu:**
```
Bu ürünü gerçekten çok beğendim, harika bir deneyimdi!
```

**Olumsuz:**
```
Kargo rezaletti, bir daha asla alışveriş yapmam.
```

## 🔧 Özellikler

✅ Türkçe metin temizleme  
✅ İki model karşılaştırması  
✅ GPU desteği  
✅ Canlı tahmin arayüzü  
✅ Hazır örnek cümleler  

## 📦 Gereksinimler

Tüm kütüphaneler notebook içinde otomatik yüklenir:
```
transformers, datasets, torch, gradio, scikit-learn
```

---

**Not:** Google Colab + GPU kullanımı önerilir.
