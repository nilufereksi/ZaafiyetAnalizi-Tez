# tez

![owasptez-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/2e1c96ea-2958-4987-899d-77ec25212f9f)


***

# 🛡️ AI-Destekli Otonom Zafiyet Analiz Platformu

Siber güvenlik test süreçlerini otonomlaştıran, görsel kanıtları (UI hataları) ve yapılandırılmış logları (JSON) çok modüllü (Multi-Modal) işleyerek OWASP standartlarında çözüm raporları üreten hibrit analiz platformu. 

Bu proje, kurumların hassas güvenlik verilerini 3. parti bulut sistemlerine göndermeden, **tamamen yerel ağda (On-Premise)** ve izole bir şekilde analiz yapabilmesi için tasarlanmıştır.

## ✨ Temel Özellikler

* **Çok Modüllü (Multi-Modal) Analiz:** Yalnızca metinsel logları (JSON) değil, aynı zamanda ekran görüntülerini de (PNG/JPG) OCR destekli görüntü işleme ile analiz eder.
* **Veri Mahremiyeti (Data Privacy - On-Premise):** Büyük Dil Modeli (Llama-3), LM Studio aracılığıyla yerel ağda çalıştırılır. Veriler asla dışarı çıkmaz.
* **Hibrit Analiz Motoru:** Klasik kural tabanlı tespit algoritmaları ile Büyük Dil Modellerinin (LLM) analitik gücünü birleştirerek sıfır hata (false-positive) oranını hedefler.
* **Otonom Raporlama:** Tespit edilen zafiyetler (Örn: SQL Injection, IDOR) için risk seviyesi belirler ve Türkçe teknik çözüm stratejileri üretir.

## 🏗️ Sistem Mimarisi ve Teknoloji Yığını

Platform, birbirine REST API üzerinden bağlanan üç temel katmandan oluşmaktadır:

1. **Kullanıcı Arayüzü (Frontend):** `C#` ve `ASP.NET Core MVC`
2. **Uygulama Sunucusu (Backend):** `Python`, `FastAPI`, `EasyOCR`, `Pillow`
3. **Çıkarım Sunucusu (AI Inference):** `LM Studio`, `Meta Llama-3-8B-Instruct`

---

## 🚀 Kurulum ve Çalıştırma

Projeyi GitHub'dan indirdikten sonra yerel ortamınızda ayağa kaldırmak için aşağıdaki adımları sırasıyla izleyin.

### 1. LM Studio (Yapay Zeka Sunucusu) Hazırlığı
1. Bilgisayarınıza [LM Studio](https://lmstudio.ai/)'yu indirin ve kurun.
2. Arama çubuğundan `meta-llama-3-8b-instruct` modelini indirip yükleyin.
3. Sol menüden **Local Server** (`<->` simgesi) sekmesine tıklayın.
4. Üst kısımdan indirdiğiniz Llama-3 modelini seçerek belleğe yükleyin.
5. Port ayarının `1234` olduğundan emin olun ve **Start Server** butonuna tıklayın.

### 2. Python Backend (FastAPI) Başlatma
Analiz motorunu ayağa kaldırmak için terminali açın ve `backend` klasörüne gidin:
```bash
cd backend

### Gerekli kütüphaneleri yükleyin (Not: openai kütüphanesinin 0.28 sürümü zorunludur)
pip install -r requirements.txt

### Sunucuyu başlatın
python main.py

Terminalde SİSTEM BAŞLATILIYOR yazısını göreceksiniz. Backend sunucusu http://127.0.0.1:5001 adresinde çalışmaya başlayacaktır. Bu terminal penceresini kapatmayın.
3. .NET Frontend (Kullanıcı Arayüzü) Başlatma

    Projenin ana dizininde Visual Studio'yu açıp .sln dosyasına tıklayın ve üstteki Run butonuna basarak projeyi derleyip çalıştırın.

    VEYA terminal üzerinden ana proje dizinindeyken aşağıdaki komutu çalıştırın:

Bash

dotnet run

    Tarayıcınızdan arayüze erişerek JSON veya görüntü yükleyip güvenlik analizinizi başlatabilirsiniz.

📝 API Endpoints (Python Backend)

Uygulama sunucusu dış kaynaklardan gelen verileri analiz etmek için iki ana uç nokta sunar:

    POST /analyze/image: Görüntü dosyaları (PNG, JPG) için OCR ve LLM destekli analiz.

    POST /analyze/json: Uygulama logları ve yapılandırılmış metinsel (JSON) veriler için LLM analizi.

🎓 Akademik Bildirim

Bu proje, lisans bitirme tezi kapsamında geliştirilmiştir. Siber güvenlik süreçlerinde yapay zekanın yerel ve güvenli (On-Premise) kullanımına dair kavramsal bir kanıt (Proof of Concept) niteliği taşımaktadır.
