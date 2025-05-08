# Animal-Image-Classification

README.md
🐍 Animal Image Classifier: Cats, Dogs, & Snakes

📝 Deskripsi Proyek
Proyek ini merupakan implementasi klasifikasi gambar hewan (kucing, anjing, dan ular) menggunakan dataset Animal Image Classification. Tujuan utama adalah memenuhi kriteria akhir program Studi Independen Machine Learning Engineer dengan akurasi tinggi dan penyimpanan model dalam berbagai format.

📦 Dataset
- Source: https://www.kaggle.com/datasets/borhanitrash/animal-image-classification-dataset
- Jumlah Total Gambar: 3.000 JPG
- Kelas:
    1. Cats (1.000 gambar)
    2. Dogs (1.000 gambar)
    3. Snakes (1.000 gambar)
- Format: .jpg
- Resolusi: 256×256 px (disesuaikan ke 224×224 untuk model transfer learning)
- Warna: RGB

🗂️ Struktur Folder

Animals/        # Dataset asli
├── cats/
├── dogs/
└── snakes/

Animals_split/      # Hasil split 80/10/10
├── train/
│   ├── cats/
│   ├── dogs/
│   └── snakes/
├── val/
│   ├── cats/
│   ├── dogs/
│   └── snakes/
└── test/
    ├── cats/
    ├── dogs/
    └── snakes/

🧠 Arsitektur Model
- Backbone: MobileNetV2 (pretrained ImageNet, include_top=False)
- Entry Conv2D: Dummy 1×1 conv untuk menyesuaikan shape
- Global Pooling: GlobalAveragePooling2D
- Fully Connected: Dense 128 + Dropout 50%
- Output: Dense 3 (softmax)

🔀 Pembagian Dataset (80/10/10)
- 📊 Train: 2.400 gambar (80%)
- 🧪 Validation: 300 gambar (10%)
- 🧾 Test: 300 gambar (10%)

🛠️ Preprocessing dan Augmentasi
- 🔄 Resize ke 224×224 px
- 📉 Rescale piksel ke [0,1]
- 🧬 Augmentasi (train set):
    - 🔃 Flip horizontal
    - 🔁 Rotasi hingga 30°
    - 💡 Brightness range [0.8,1.2]
    - 📐 Shear dan zoom 0.2

⏱️ Callback
- ⛔ EarlyStopping: monitor val_accuracy, patience=5
- 🔄 ReduceLROnPlateau: monitor val_loss, factor=0.5, patience=3
- 💾 ModelCheckpoint: menyimpan best_model.keras

📈 Evaluasi
- 🎯 Target Akurasi: ≥85% (train & test)
- 🏆 Target Tambahan: ≥95%
- 📉 Tampilkan grafik akurasi & loss per epoch

💾 Penyimpanan Model 
Model disimpan dalam 3 format:
1. 🧠 TensorFlow SavedModel (saved_model/)
2. 📱 TensorFlow Lite (model.tflite)
3. 🌐 TensorFlow.js (tfjs_model/)

🔍 Inferensi
Contoh inferensi menggunakan TFLite:

interpreter = tf.lite.Interpreter(model_path='model.tflite')
interpreter.allocate_tensors()
# set tensor input & invoke...

📚 Dependencies
tensorflow >= 2.11
scikit-learn
numpy
matplotlib
tensorflowjs  # hanya untuk konversi TFJS

▶️ Cara Menjalankan Proyek
1. Tempatkan dataset asli di animal_dataset/
2. Buka dan jalankan notebook Submission_Final.ipynb
3. Notebook akan: split data, training, evaluasi, plotting, dan menyimpan model
4. Setelah selesai, folder saved_model/, model.tflite, dan tfjs_model/ siap digunakan

👤 Kontributor
- 📛 Nama: Arthur Nehemia Gilbert Eduardo Luke Keintjem
- 🏫 Asal Kampus: Universitas Brawijaya
- 🎓 Program: Studi Independen - Machine Learning Engineer (Coding Camp 2025 powered by DBS Foundation)
