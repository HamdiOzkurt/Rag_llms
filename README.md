RAG LLM Doküman Analiz Aracı
Bu proje, yerel LLM (Large Language Model) modellerini kullanarak yüklenen PDF dokümanları üzerinde soru-cevap yapmanızı ve bilgi çıkarmanızı sağlayan bir Streamlit uygulamasıdır.

Uygulama, RAG (Retrieval-Augmented Generation) mimarisini kullanır. Yüklenen PDF dokümanlarını parçalar, vektör veritabanına (ChromaDB) kaydeder ve Ollama üzerinden çalışan yerel bir LLM modeli ile soruları yanıtlar.

🚀 Özellikler
PDF Yükleme ve Önizleme: Kullanıcı dostu arayüz ile PDF yükleme ve görüntüleme.
Vektör Veritabanı: Dokümanlar parçalanarak ChromaDB üzerinde vektörleştirilir ve saklanır.
Yerel LLM Desteği: Ollama entegrasyonu sayesinde verileriniz dışarı çıkmadan yerel modelinizle çalışır.
Otomatik Bilgi Çıkarımı: Araştırma kağıtlarından başlık, özet, yayın tarihi ve yazar bilgilerini otomatik olarak çıkarır.
🛠️ Teknolojiler
Arayüz: Streamlit
Orkestrasyon: LangChain
Vektör Veritabanı: ChromaDB
LLM Sunucusu: Ollama
Konteynerizasyon: Docker & Docker Compose
📋 Gereksinimler
Docker ve Docker Compose (Önerilen)
VEYA Python 3.9+ ve yerel olarak çalışan bir Ollama kurulumu
🐳 Docker ile Kurulum (Önerilen)
En kolay kurulum yöntemidir. Tüm servisleri (Uygulama ve Ollama) tek komutla ayağa kaldırır.

Repoyu klonlayın veya indirin:

git clone <repo-url>
cd rag_llms
Uygulamayı başlatın:

docker-compose up --build
Not: docker-compose.yml dosyasındaki Ollama volume ayarı (C:\Users\hamdi\.ollama:/root/.ollama) Windows yoluna göre ayarlanmıştır. Kendi bilgisayarınızdaki Ollama modellerinin bulunduğu yolu buraya verebilir veya bu satırı kaldırarak container içinde modelleri tekrar indirebilirsiniz.

Uygulamaya erişin: Tarayıcınızda http://localhost:8501 adresine gidin.

🐍 Yerel Kurulum (Python)
Docker kullanmadan çalıştırmak isterseniz:

Sanal ortam oluşturun ve aktif edin:

python -m venv venv
# Windows için:
.\venv\Scripts\activate
# Linux/Mac için:
source venv/bin/activate
Bağımlılıkları yükleyin:

pip install -r requirements.txt
Ollama'nın çalıştığından emin olun: Bilgisayarınızda Ollama'yı kurun ve çalıştırın.

ollama serve
Gerekli modeli indirdiğinizden emin olun (kod içinde varsayılan olarak kullanılan model, örn: mistral, llama veya nomic-embed-text vb.).

Uygulamayı başlatın:

streamlit run app/streamlit_app.py
📂 Proje Yapısı
rag_llms/
├── app/
│   ├── db/               # ChromaDB veritabanı dosyaları
│   ├── functions.py      # RAG pipeline, Embedding ve LLM fonksiyonları
│   └── streamlit_app.py  # Ana uygulama arayüzü
├── data/                 # Örnek veri klasörü
├── docker-compose.yml    # Docker servis tanımları
├── dockerfile            # Uygulama için Docker imaj dosyası
├── requirements.txt      # Python kütüphaneleri
└── README.md             # Dokümantasyon
⚙️ Konfigürasyon
Uygulama app/functions.py içerisindeki get_ollama_base_url fonksiyonu ile çalışma ortamını (Docker veya Local) otomatik algılar.

Docker Ortamı: http://ollama:11434 adresine bağlanır.
Local Ortam: http://localhost:11434 adresine bağlanır.
Eğer farklı bir URL kullanmak isterseniz OLLAMA_BASE_URL çevre değişkenini (environment variable) ayarlayabilirsiniz.
