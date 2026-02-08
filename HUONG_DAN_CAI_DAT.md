# Hướng Dẫn Cài Đặt và Chạy Facial Landmarks Recognition

## 📋 Mục Lục
- [Yêu Cầu Hệ Thống](#-yêu-cầu-hệ-thống)
- [Cài Đặt Python](#-cài-đặt-python)
- [Cài Đặt Môi Trường Ảo](#-cài-đặt-môi-trường-ảo)
- [Cài Đặt Thư Viện](#-cài-đặt-thư-viện)
- [Chạy Ứng Dụng](#-chạy-ứng-dụng)
- [Xử Lý Lỗi Thường Gặp](#-xử-lý-lỗi-thường-gặp)

---

## 🖥️ Yêu Cầu Hệ Thống

| Thành phần | Yêu cầu |
|------------|---------|
| Hệ điều hành | Windows 10/11 (64-bit) |
| Python | **3.9.x** (khuyến nghị 3.9.13) |
| RAM | Tối thiểu 4GB |
| Webcam | Cần có webcam để chạy ứng dụng |
| Dung lượng | ~200MB cho thư viện + model |

> [!IMPORTANT]
> **Bắt buộc sử dụng Python 3.9.x** vì thư viện `dlib` trong dự án chỉ tương thích với phiên bản này.

---

## 🐍 Cài Đặt Python

### Bước 1: Tải Python 3.9.13
- Truy cập: https://www.python.org/downloads/release/python-3913/
- Tải file: **Windows installer (64-bit)**

### Bước 2: Cài đặt Python
1. Chạy file installer vừa tải
2. **✅ Tích chọn "Add Python 3.9 to PATH"**
3. Chọn **"Customize installation"**
4. Chọn tất cả các optional features
5. Hoàn tất cài đặt

### Bước 3: Kiểm tra cài đặt
```bash
python --version
# Kết quả mong đợi: Python 3.9.13
```

---

## 🔧 Cài Đặt Môi Trường Ảo

> [!TIP]
> Sử dụng môi trường ảo giúp tránh xung đột thư viện với các dự án khác.

### Tạo môi trường ảo
```bash
# Di chuyển vào thư mục dự án
cd d:\CUONG\PTIT\THI_GIAC_MAY_TINH\facial-landmarks-recognition

# Tạo môi trường ảo với Python 3.9
python -m venv .venv
```

### Kích hoạt môi trường ảo
```bash
# Windows (PowerShell)
.\.venv\Scripts\Activate.ps1

# Windows (CMD)
.\.venv\Scripts\activate.bat
```

Sau khi kích hoạt, bạn sẽ thấy `(.venv)` xuất hiện ở đầu dòng lệnh.

---

## 📦 Cài Đặt Thư Viện

### Danh sách thư viện cần thiết

| Thư viện | Phiên bản | Mục đích |
|----------|-----------|----------|
| opencv-python | 4.7.0.72 | Xử lý hình ảnh và video |
| imutils | 0.5.4 | Tiện ích xử lý ảnh |
| dlib | 19.22.99 | Phát hiện khuôn mặt và landmarks |
| numpy | <2 | Tính toán mảng số |

### Phương pháp 1: Cài đặt từ file wheel (Khuyến nghị cho Windows)

> [!WARNING]
> Cài đặt `dlib` từ pip thường gặp lỗi trên Windows. Sử dụng file wheel có sẵn trong dự án để tránh lỗi.

```bash
# Kích hoạt môi trường ảo trước
.\.venv\Scripts\Activate.ps1

# Cài đặt numpy trước (yêu cầu phiên bản < 2)
pip install "numpy<2"

# Cài đặt dlib từ file wheel có sẵn
pip install dlib-19.22.99-cp39-cp39-win_amd64.whl

# Cài đặt các thư viện còn lại
pip install opencv-python==4.7.0.72
pip install imutils==0.5.4
```

### Phương pháp 2: Cài đặt từ requirements.txt
```bash
pip install -r requirements.txt
```

> [!CAUTION]
> Nếu gặp lỗi với `dlib`, hãy sử dụng Phương pháp 1.

---

## ▶️ Chạy Ứng Dụng

### Bước 1: Kiểm tra file model
Đảm bảo file `shape_predictor_68_face_landmarks.dat` (~95MB) có trong thư mục dự án.

### Bước 2: Chạy ứng dụng
```bash
# Kích hoạt môi trường ảo (nếu chưa kích hoạt)
.\.venv\Scripts\Activate.ps1

# Chạy ứng dụng
python main.py
```

### Bước 3: Sử dụng
- Webcam sẽ tự động bật
- 68 điểm facial landmarks sẽ được vẽ lên khuôn mặt (màu xanh lá)
- Nhấn **ESC** để thoát

---

## ❗ Xử Lý Lỗi Thường Gặp

### 1. Lỗi `dlib` không cài được

**Nguyên nhân:** Thiếu Visual Studio Build Tools hoặc sai phiên bản Python.

**Giải pháp:**
```bash
# Sử dụng file wheel có sẵn
pip install dlib-19.22.99-cp39-cp39-win_amd64.whl
```

### 2. Lỗi `numpy.dtype size changed`

**Nguyên nhân:** Phiên bản numpy không tương thích.

**Giải pháp:**
```bash
pip uninstall numpy
pip install "numpy<2"
```

### 3. Lỗi `cannot open camera`

**Nguyên nhân:** Webcam đang được sử dụng bởi ứng dụng khác hoặc không được kết nối.

**Giải pháp:**
- Đóng các ứng dụng đang sử dụng webcam (Zoom, Teams, etc.)
- Kiểm tra webcam trong Device Manager
- Thử thay `cv2.VideoCapture(0)` thành `cv2.VideoCapture(1)` trong `main.py`

### 4. Lỗi `shape_predictor_68_face_landmarks.dat not found`

**Nguyên nhân:** Thiếu file model.

**Giải pháp:**
- Tải từ: http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2
- Giải nén và đặt vào thư mục dự án

### 5. Lỗi PowerShell Execution Policy

**Nguyên nhân:** PowerShell chặn script.

**Giải pháp:**
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

## 📁 Cấu Trúc Thư Mục Dự Án

```
facial-landmarks-recognition/
├── .venv/                                    # Môi trường ảo Python
├── main.py                                   # File chính
├── requirements.txt                          # Danh sách thư viện
├── dlib-19.22.99-cp39-cp39-win_amd64.whl    # Wheel file cho dlib
├── shape_predictor_68_face_landmarks.dat    # Model nhận diện (~95MB)
└── README.md                                 # Hướng dẫn ngắn
```

---

## 📌 Lưu Ý Quan Trọng

1. **Luôn kích hoạt môi trường ảo** trước khi cài đặt hoặc chạy code
2. **Thứ tự cài đặt quan trọng:** numpy → dlib → opencv-python → imutils
3. **Không nâng cấp numpy lên phiên bản 2.x** vì sẽ gây xung đột với dlib
4. **File model rất lớn (~95MB)**, đảm bảo không xóa hoặc di chuyển file này

---

## 🔗 Tham Khảo

- [dlib Documentation](http://dlib.net/)
- [OpenCV Python Tutorial](https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html)
- [68 Face Landmarks](https://ibug.doc.ic.ac.uk/resources/facial-point-annotations/)
