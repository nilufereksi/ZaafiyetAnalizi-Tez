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
* **Bulut Bilişime Hazır (Cloud-Native):** Sistem; frontend ve backend olarak mikroservis mantığıyla ayrıştırılmış, Dockerize edilmiş ve Kubernetes (Minikube) ortamında orkestre edilebilir yapıdadır.

## 🏗️ Sistem Mimarisi ve Teknoloji Yığını

Platform, birbirine REST API üzerinden bağlanan üç temel katmandan oluşmaktadır:

1. **Kullanıcı Arayüzü (Frontend):** `C#` ve `ASP.NET Core MVC`
2. **Uygulama Sunucusu (Backend):** `Python`, `FastAPI`, `EasyOCR`, `Pillow`
3. **Çıkarım Sunucusu (AI Inference):** `LM Studio`, `Meta Llama-3 (8B Instruct)`
4. **DevOps & Dağıtım:** `Docker`

## 🚀 Kurulum ve Çalıştırma

Projeyi yerel ortamınızda çalıştırmak için aşağıdaki adımları sırasıyla izleyin.

### 1. LM Studio (Yapay Zeka Sunucusu) Hazırlığı
1. LM Studio'yu indirin ve açın.
2. Arama çubuğundan `meta-llama-3-8b-instruct` modelini indirip yükleyin.
3. Sol menüden **Local Server** `<->` simgesine tıklayın.
4. Port ayarının `1234` olduğundan emin olun ve **Start Server** butonuna tıklayın.

### 2. Python Backend (FastAPI) Başlatma
Analiz motorunu ayağa kaldırmak için terminali açın:
```bash
# Gerekli kütüphaneleri yükleyin
pip install -r requirements.txt
# Not: openai kütüphanesinin 0.28 sürümü zorunludur (pip install openai==0.28)

# Sunucuyu başlatın
python main.py
```
*Backend sunucusu `http://127.0.0.1:5001` adresinde çalışmaya başlayacaktır.*

### 3. .NET Frontend (Kullanıcı Arayüzü) Başlatma
1. Visual Studio veya terminal üzerinden projeyi derleyin.
2. Uygulamayı çalıştırın (`dotnet run`).
3. Tarayıcınızdan arayüze erişerek ilk güvenlik analizinizi başlatın.

---

## Docker Dağıtımı (DevOps)

Geliştirilen FastAPI analiz motoru, yüksek erişilebilirlik ve ölçeklenebilirlik prensipleri gereği Kubernetes ortamında çalışacak şekilde yapılandırılmıştır. 

Lokal kümenizde (Minikube) ayağa kaldırmak için:

```bash
# 1. Docker imajını oluşturun
docker build -t siber-ai-backend .

# 2. Kubernetes manifestolarını uygulayın
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml

# 3. Pod ve Servis durumunu kontrol edin
kubectl get pods
kubectl get services
```

## 📝 API Endpoints (Python Backend)

Uygulama sunucusu dış kaynaklardan gelen verileri analiz etmek için iki ana uç nokta sunar:

* `POST /analyze/image`: Görüntü dosyaları (PNG, JPG) için OCR ve LLM destekli analiz.
* `POST /analyze/json`: Uygulama logları ve yapılandırılmış metinsel (JSON) veriler için LLM analizi.

## 🎓 Akademik Bildirim
Bu proje, lisans bitirme tezi kapsamında geliştirilmiştir. Siber güvenlik süreçlerinde yapay zekanın yerel ve güvenli (On-Premise) kullanımına dair kavramsal bir kanıt (Proof of Concept) niteliği taşımaktadır.
