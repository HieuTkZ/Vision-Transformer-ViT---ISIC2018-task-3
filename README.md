# Image Classification using Vision Transformer (ViT) on ISIC 2018 – Task 3

##  Giới thiệu
Dự án này tập trung **nghiên cứu và đánh giá khả năng thay thế mạng CNN truyền thống bằng Vision Transformer (ViT)** trong bài toán **phân loại ảnh y tế**, cụ thể là phân loại tổn thương da trên **tập dữ liệu ISIC 2018 – Task 3**.

Thay vì trích xuất đặc trưng cục bộ như CNN, **Vision Transformer khai thác cơ chế Self-Attention** để học mối quan hệ toàn cục giữa các vùng ảnh, từ đó cải thiện khả năng tổng quát hóa trong phân loại hình ảnh.

Mô hình sử dụng **pretrained ViT-B/16 (vit-base-patch16-224)** và được fine-tune trên tập dữ liệu ISIC 2018.

---

##  Dataset: ISIC 2018 – Task 3

- **Tên đầy đủ:** ISIC 2018: Skin Lesion Analysis Towards Melanoma Detection
- **Nhiệm vụ:** Phân loại tổn thương da (multi-class classification)
- **Số lớp:** 7
- **Kích thước ảnh:** 224 × 224 × 3
- **Các lớp bao gồm:**
  - MEL (Melanoma)
  - NV (Melanocytic Nevus)
  - BCC (Basal Cell Carcinoma)
  - AKIEC
  - BKL
  - DF
  - VASC

---

##  Mô hình sử dụng

### Vision Transformer (ViT)

- **Model:** vit-base-patch16-224
- **Pretrained:** ImageNet
- **Patch size:** 16 × 16
- **Số Transformer Encoder:** 12
- **Hidden size:** 768
- **Attention heads:** 12

Ảnh đầu vào được chia thành các patch nhỏ, sau đó đưa qua Transformer Encoder để học đặc trưng toàn cục.

---

##  Quy trình huấn luyện

### 1. Tiền xử lý dữ liệu
- Resize ảnh về 224 × 224
- Chuẩn hóa theo mean và std của ImageNet
- Data augmentation (nếu có):
  - Random Horizontal Flip
  - Random Rotation
  - Color Jitter

### 2. Fine-tuning mô hình
- Thay thế classification head cho 7 lớp
- Huấn luyện end-to-end trên tập ISIC 2018

---

##  Cấu hình huấn luyện

```text
Optimizer      : AdamW
Learning rate  : 3e-4
Batch size     : 16 / 32
Epochs         : 20 – 50
Loss function  : Cross Entropy Loss
