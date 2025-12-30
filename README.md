# 🔢 LSTM Sayı Tahmin Modeli

Bu proje, LSTM (Long Short-Term Memory) sinir ağı kullanarak ardışık sayıları öğrenen ve bir sonraki sayıyı tahmin eden basit bir derin öğrenme uygulamasıdır.

## 📊 Proje Özeti

- **Model:** LSTM (PyTorch)
- **Görev:** Ardışık sayı tahmini
- **Girdi:** 4 ardışık sayı
- **Çıktı:** 5. sayının tahmini
- **Arayüz:** Gradio web arayüzü

## 🎯 Nasıl Çalışır?

Model, 0'dan 999'a kadar olan sayıları kullanarak eğitilir. 4 ardışık sayı verdiğinizde, bu kalıbı öğrenerek bir sonraki sayıyı tahmin eder.

**Örnek:**
- Girdi: `50, 51, 52, 53`
- Tahmin: `54`

## 🚀 Hızlı Başlangıç

### Google Colab'da Çalıştırma

1. Notebook'u Google Colab'a yükleyin
2. Hücreleri sırayla çalıştırın
3. Gradio arayüzü otomatik olarak açılır

### Gereksinimler

```python
torch
numpy
gradio
```

*Not: Tüm kütüphaneler notebook içinde otomatik yüklenir.*

## 📁 Proje Yapısı

### 1. Model Tanımı

```python
class LSTMModelDemo(nn.Module):
    def __init__(self):
        super(LSTMModelDemo, self).__init__()
        self.lstm = nn.LSTM(input_size=1, hidden_size=50, batch_first=True)
        self.fc = nn.Linear(50, 1)
```

**Model Mimarisi:**
- Input Layer: 1 özellik (bir sayı)
- LSTM Layer: 50 hidden unit
- Output Layer: 1 çıktı (tahmin edilen sayı)

### 2. Veri Hazırlama

```python
data = np.arange(1000)  # 0-999 arası sayılar
seq_length = 4          # 4 sayı alıp 5. sayıyı tahmin et
```

**Eğitim Verisi:**
- 996 örnek (0-999 arasından 4'lü diziler)
- Her örnek: [i, i+1, i+2, i+3] → i+4

### 3. Eğitim

```python
epochs = 500
learning_rate = 0.01
optimizer = Adam
loss_function = MSELoss
```

## 💻 Kullanım

### Model ile Tahmin Yapma

Gradio arayüzünde:

1. 4 ardışık sayıyı virgülle ayırarak girin
2. "Submit" butonuna tıklayın
3. Model bir sonraki sayıyı tahmin eder

**Girdi Formatı:**
```
50,51,52,53
```

**Çıktı:**
```
Tahmin Edilen Sonraki Sayı: 54
```

### Kod ile Kullanım

```python
# Model yükleme
model = LSTMModelDemo()
model.load_state_dict(torch.load('lstm_model.pth'))
model.eval()

# Tahmin
test_seq = torch.tensor([[50, 51, 52, 53]], dtype=torch.float32).unsqueeze(-1)
with torch.no_grad():
    prediction = model(test_seq)
print(f"Tahmin: {round(prediction.item())}")
```

## 📈 Örnek Sonuçlar

| Girdi | Beklenen | Tahmin |
|-------|----------|--------|
| 50, 51, 52, 53 | 54 | ~54 |
| 100, 101, 102, 103 | 104 | ~104 |
| 200, 201, 202, 203 | 204 | ~204 |
| 500, 501, 502, 503 | 504 | ~504 |

## ⚙️ Teknik Detaylar

### Hiperparametreler

- **Sequence Length:** 4 (4 sayı ile tahmin)
- **Hidden Size:** 50 (LSTM gizli katman boyutu)
- **Learning Rate:** 0.01
- **Epochs:** 500
- **Optimizer:** Adam
- **Loss Function:** MSE (Mean Squared Error)

### Model Performansı

Model eğitim sırasında loss değerini şu şekilde düşürür:

```
Epoch 50:  Loss: 312898.5312
Epoch 100: Loss: 288857.0312
Epoch 150: Loss: 265865.2500
...
Epoch 500: Loss: 156077.5000
```

### LSTM Neden Kullanıldı?

LSTM, sıralı verilerde (time series) önceki bilgileri hatırlama yeteneği sayesinde ardışık sayı kalıplarını öğrenmede başarılıdır.

## 🎓 Öğrenme Potansiyeli

Bu proje temel bir örnektir. Geliştirilebilir:

**Veri Çeşitliliği:**
- Fibonacci dizisi
- Çift/tek sayı kalıpları
- Aritmetik/geometrik diziler
- Rastgele kalıplar

**Model İyileştirmeleri:**
- Daha derin LSTM katmanları
- Bidirectional LSTM
- GRU kullanımı
- Attention mekanizması

**Uygulama Alanları:**
- Zaman serisi tahmini
- Hisse senedi fiyat tahmini
- Hava durumu tahmini
- Enerji tüketimi tahmini

## 🔧 Sorun Giderme

### Hata: "4 adet sayı girmelisiniz"
**Çözüm:** Tam olarak 4 sayı girin, virgülle ayırın.

### Hata: "Sadece virgülle ayrılmış sayılar girin"
**Çözüm:** Sadece rakam ve virgül kullanın. Boşluk ekleyebilirsiniz.

**Doğru formatlar:**
```
50,51,52,53
50, 51, 52, 53
```

**Yanlış formatlar:**
```
50-51-52-53
50 51 52 53
elli,51,52,53
```

## 📝 Notlar

- Model 0-999 arası sayılarla eğitildiği için bu aralık dışındaki sayılarda tahmin doğruluğu azalabilir
- Her çalıştırmada model yeniden eğitilir (500 epoch ~1-2 dakika)
- Model `lstm_model.pth` olarak kaydedilir
- Gradio share linki 72 saat geçerlidir

## 🤝 Katkıda Bulunma

Bu basit proje eğitim amaçlıdır. Geliştirme önerileri:

1. Daha karmaşık diziler ekleyin
2. Model mimarisini derinleştirin
3. Farklı optimizasyon algoritmaları deneyin
4. Validation set ekleyin
5. Model performansını görselleştirin

## 📚 Kaynaklar

- [PyTorch LSTM Dokümantasyonu](https://pytorch.org/docs/stable/generated/torch.nn.LSTM.html)
- [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [Gradio Dokümantasyonu](https://www.gradio.app/docs/)

## ⚠️ Önemli

Bu proje **eğitim amaçlı** basit bir örnektir. Gerçek dünya uygulamaları için:

- Daha karmaşık veri setleri kullanın
- Cross-validation uygulayın
- Hiperparametre optimizasyonu yapın
- Model performansını detaylı analiz edin

---

**Not:** Bu notebook Google Colab ortamında çalışacak şekilde tasarlanmıştır. Lokal ortamda çalıştırmak için PyTorch kurulumu gerekir.
