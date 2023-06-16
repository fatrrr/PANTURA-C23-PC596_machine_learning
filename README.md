# Pantura C23-PC596 Machine Learning Path

Full Projek: https://github.com/PANTURA-C23-PC596

## Anggota ML Path

|No|Bangkit ID|Nama|Akun Github|Universitas|
|---:|-|-|-|-|
|1.|M229DSX1457|Fatur Rahman|[@fatrrr](https://github.com/fatrrr)|Universitas Lambung Mangkurat|
|2.|M065DKX3768|Muhammad Kausar|[@kausarm](https://github.com/kausarm)|Politeknik Negeri Lhokseumawe|
|3.|M181DSY1569|Nisrina Anbar Fadhilah|[@nisrinanbr](https://github.com/nisrinanbr)|Universitas Indonesia|

## Jobdesk ML Path

Kami ditugaskan untuk membuat model deteksi tingkat kerusakan jalan, mulai dari tidak ada kerusakan, rendah, sedang, dan tinggi.

## Result

Kami berhasil membuat model Convolutional Neural Network dengan akurasi 98.5% dan F1-score 98.6%, dengan total 4,054,688 parameter.

## Steps

Tools:
1. Python - TensorFlow
2. Colaboratory

### Dataset

Dataset yang kami gunakan adalah [public dataset](https://www.kaggle.com/datasets/prudhvignv/road-damage-classification-and-assessment) dengan jumlah 2074 gambar.

#### Image Processing

1. Label ulang dataset:
    - satisfactory => tidak_ada_kerusakan
    - good         => rendah
    - poor         => sedang
    - very_poor    => tinggi

2. Load & extract dataset
3. Resize images
4. One-hot encode Label
5. Augment data
6. Split to training and validation data
7. Batching


### Model

- Model
Kami menggunakan transfer learning terhadap [EfficientNetV1 B0 Feature Vector](https://tfhub.dev/tensorflow/efficientnet/b0/feature-vector/1), dan 4 units layer dense, dengan aktivasi softmax. Disusun dengan 1-e3 learning rate Adam optimizer, categorical crossentropy loss.

- Training
Digunakan callback earlystop untuk mencegah overfitting, dilatih sebanyak 50 epoch, setiap 5 epoch simpan weight kemudian load weight sekitar 10 kali.

- Evaluasi
Kami evaluasi model kami dengan metode Precision, Recall, dan F1-score
1. Akurasi      : 98.5~%
2. Recall       : 98.6%
3. Precision    : 98.6%
4. F1-score     : 98.6%

- Save Model
Kami simpan model dalam format:
1. Folder saved model
2. tflite
3. HDF5
4. json

### Deployment

Kami deploy model secara lokal terhadap aplikasi Android dengan TensorFlowLite, dan [menulis metadata](https://www.tensorflow.org/lite/models/convert/metadata) bagi model.tflite.
