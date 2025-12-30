# 🤖 Türkçe Duygu Analizi Projesi - BERTurk & XLM-RoBERTa

Bu proje, Türkçe Twitter yorumları üzerinde duygu analizi (sentiment analysis) yapmak için geliştirilmiş bir deep learning uygulamasıdır. BERTurk ve XLM-RoBERTa gibi transformer tabanlı modeller kullanılarak olumlu ve olumsuz duyguların sınıflandırılması gerçekleştirilmiştir.

## 📊 Proje Özeti

- **Görev:** İkili Duygu Sınıflandırması (Olumlu/Olumsuz)
- **Veri Seti:** Türkçe Twitter yorumları
- **Modeller:** BERTurk, XLM-RoBERTa
- **En İyi Performans:** XLM-RoBERTa (%92.6 accuracy)
- **Uygulama:** Gradio tabanlı web arayüzü

## 🎯 Özellikler

✅ Türkçe metinler için özel ön işleme (preprocessing)  
✅ İki farklı BERT modelinin karşılaştırmalı analizi  
✅ GPU desteği (Google Colab T4)  
✅ Gerçek zamanlı tahmin için Gradio arayüzü  
✅ Detaylı model değerlendirme metrikleri  
✅ Confusion matrix ve görselleştirmeler  

## 🚀 Hızlı Başlangıç

### Google Colab'da Çalıştırma

1. Bu notebook'u Google Colab'a yükleyin
2. Runtime > Change runtime type > GPU (T4) seçin
3. Hücreleri sırayla çalıştırın

### Gereksinimler

```python
transformers
datasets
torch
scikit-learn
nltk
matplotlib
seaborn
TurkishStemmer
sentencepiece
gradio
```

*Not: Tüm gerekli kütüphaneler notebook içinde otomatik olarak yüklenir.*

## 📁 Proje Yapısı

### 1. Kurulum ve Veri Yükleme
- Gerekli kütüphanelerin kurulumu
- Twitter veri setinin yüklenmesi
- NLTK stopwords ve punkt indirilmesi

### 2. Veri Ön İşleme
```python
def veri_temizleme(metin):
    # Küçük harfe çevirme
    # @kullanici etiketlerini temizleme
    # URL'leri temizleme
    # Sayıları ve özel karakterleri temizleme
    # Fazladan boşlukları düzenleme
```

**Önemli:** Stopwords ve stemming işlemleri bilerek uygulanmamıştır, çünkü BERT modelleri kontekst tabanlı çalışır.

### 3. Model Eğitimi

#### BERTurk
- Model: `dbmdz/bert-base-turkish-cased`
- Batch size: 16
- Epochs: 3
- Learning rate: 2e-5
- Max length: 256

#### XLM-RoBERTa
- Model: `xlm-roberta-base`
- Çoklu dil desteği
- Daha yüksek performans

### 4. Model Değerlendirmesi

| Metrik | BERTurk | XLM-RoBERTa |
|--------|---------|-------------|
| Accuracy | %85.5 | %92.6 |
| F1-Score | %85.5 | %92.6 |

### 5. Gradio Arayüzü

Eğitilmiş model ile gerçek zamanlı tahmin yapabileceğiniz interaktif bir web arayüzü.

**Özellikler:**
- Metin girişi
- Olasılık skorları
- Hazır örnek cümleler
- 72 saat geçerli paylaşım linki (share=True)

## 💻 Kullanım

### Model ile Tahmin Yapma

```python
# Model yükleme
tokenizer = AutoTokenizer.from_pretrained("./best_bert_model")
model = AutoModelForSequenceClassification.from_pretrained("./best_bert_model")

# Tahmin
metin = "Bu ürünü çok beğendim!"
inputs = tokenizer(metin, return_tensors="pt", truncation=True, max_length=256)
outputs = model(**inputs)
```

### Gradio Arayüzü

```python
# Arayüzü başlatma
demo.launch(share=True, debug=True)
```

Gradio arayüzü otomatik olarak bir web sayfası açar ve 72 saatlik geçici bir paylaşım linki sağlar.

## 📈 Örnek Sonuçlar

**Olumlu Örnekler:**
- "Bu ürünü gerçekten çok beğendim, harika bir deneyimdi!"
- "Mükemmel bir film, oyunculuklar şahaneydi."

**Olumsuz Örnekler:**
- "Kargo rezaletti, ürün elime paramparça ulaştı."
- "Hizmet çok yavaştı, yemekler soğuk geldi."

## ⚙️ Teknik Detaylar

### Veri Temizleme Adımları
1. Küçük harfe dönüştürme
2. Kullanıcı etiketlerini (@username) kaldırma
3. URL'leri temizleme (http, https, www)
4. Sayıları kaldırma
5. Noktalama işaretlerini ve özel karakterleri temizleme
6. Türkçe karakterleri koruma (çğıöşü)
7. Fazladan boşlukları düzenleme

### Hiperparametreler

```python
TrainingArguments(
    output_dir="./results",
    evaluation_strategy="epoch",
    save_strategy="epoch",
    learning_rate=2e-5,
    per_device_train_batch_size=16,
    per_device_eval_batch_size=16,
    num_train_epochs=3,
    weight_decay=0.01,
    load_best_model_at_end=True,
    metric_for_best_model="accuracy"
)
```

## 🔧 Sistem Gereksinimleri

- **GPU:** NVIDIA T4 (Google Colab) veya üzeri önerilir
- **RAM:** En az 12 GB (Colab high-memory runtime)
- **Python:** 3.7+
- **CUDA:** GPU kullanımı için gerekli

## 📊 Model Karşılaştırması

XLM-RoBERTa, BERTurk'e göre %7.1 daha yüksek accuracy ile daha iyi performans göstermiştir. Bu, XLM-RoBERTa'nın çok dilli öğrenme yeteneklerinin Türkçe metinlerde de etkili olduğunu göstermektedir.

## 🎓 Öğrenme Kaynakları

- [Hugging Face Transformers](https://huggingface.co/docs/transformers/)
- [BERTurk Model Card](https://huggingface.co/dbmdz/bert-base-turkish-cased)
- [XLM-RoBERTa Paper](https://arxiv.org/abs/1911.02116)

## ⚠️ Notlar

- Model eğitimi için GPU kullanımı şiddetle tavsiye edilir
- Veri seti otomatik olarak Hugging Face'den indirilir
- W&B entegrasyonu kapatılmıştır (`WANDB_DISABLED=true`)
- Gradio share linki 72 saat geçerlidir

## 📝 Lisans

Bu proje eğitim amaçlı geliştirilmiştir.

## 🤝 Katkıda Bulunma

Önerileriniz ve geliştirmeleriniz için pull request gönderebilirsiniz.

---

**Not:** Bu notebook Google Colab ortamında çalışacak şekilde optimize edilmiştir. Lokal ortamda çalıştırmak için GPU ve CUDA kurulumu gerekebilir.
