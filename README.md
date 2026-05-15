# YOLO vs Embedding + Vector Database

## 1. YOLO = “Phát hiện và phân loại”

YOLO hoạt động kiểu:

```text
camera → detect object → trả label
```

Ví dụ:

```text
đây là:
- chai coca
- lon pepsi
- hộp oreo
```

Nó giống như:

> “AI đã học trước sản phẩm này là gì.”

Muốn YOLO nhận đúng:

- phải có dataset train
- phải gán label
- phải retrain khi có sản phẩm mới

---

## Sơ đồ YOLO

```text
Camera/Image
     │
     ▼
┌─────────────┐
│    YOLO     │
│ Detection   │
└─────────────┘
     │
     ▼
┌─────────────┐
│   Label     │
│ Coca Cola   │
└─────────────┘
```

---

## 2. Embedding + Vector DB = “Tìm sản phẩm giống nhất”

Embedding không hoạt động kiểu label cố định.

Nó hoạt động kiểu:

```text
ảnh → chuyển thành vector đặc trưng
→ tìm vector gần nhất trong database
```

Giống:

- TikTok Shop
- Shopee image search
- Google Lens

Ví dụ:

```text
user upload ảnh snack
→ hệ thống tìm các sản phẩm giống nhất
```

Nó không cần:

```text
“đây chắc chắn là Oreo vị vani”
```

Mà nó sẽ:

```text
“ảnh này giống 95% với sản phẩm A”
```

---

## Sơ đồ Embedding + Vector Database

```text
User Upload Image
        │
        ▼
┌────────────────┐
│ DINOv2 / CLIP  │
│  Embedding     │
└────────────────┘
        │
        ▼
┌────────────────┐
│ Vector Database│
│ pgvector/Qdrant│
└────────────────┘
        │
        ▼
Top-K Similar Products
```

---

## Khác biệt cốt lõi

| YOLO | Embedding + Vector DB |
|---|---|
| Detect object | Tìm similarity |
| Trả label/class | Trả sản phẩm gần giống |
| Cần train class cụ thể | Không cần class cố định |
| Thêm sản phẩm mới phải retrain | Chỉ cần add vector |
| Real-time detection mạnh | Search/recommend mạnh |
| Biết “đây là gì” | Biết “giống cái nào” |
| Hợp CCTV/camera | Hợp search/ecommerce |

---

## Ví dụ thực tế

### YOLO

```text
Camera thấy:
→ “Coca Cola”
```

vì model đã train Coca Cola trước đó.

### Embedding

```text
User upload lon nước lạ
→ hệ thống tìm:
- Coca
- Pepsi
- Sprite
gần giống nhất
```

---

## Trong retail hiện đại

Người ta thường kết hợp cả hai.

### YOLO dùng để

- detect vị trí sản phẩm
- tracking
- segmentation
- đếm sản phẩm
- realtime camera

### Embedding dùng để

- xác định SKU gần đúng
- visual search
- recommendation
- product matching
- similarity search

---

## Pipeline thực tế trong retail AI

```text
Camera/Image
     │
     ▼
┌─────────────┐
│    YOLO     │
│ Detect Item │
└─────────────┘
     │
Crop Product
     │
     ▼
┌──────────────────┐
│ DINOv2 / SigLIP  │
│   Embedding      │
└──────────────────┘
     │
     ▼
┌──────────────────┐
│ Vector Database  │
│ pgvector/Qdrant  │
└──────────────────┘
     │
     ▼
Similar Product Search
     │
     ▼
Product Name + Price
```

---
