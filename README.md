# 📅 Trợ lý Quản lý Lịch Trình Cá Nhân

> Ứng dụng quản lý lịch trình cá nhân thông minh sử dụng NLP tiếng Việt để phân tích câu tự nhiên và tự động tạo sự kiện.

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/downloads/)
[![Streamlit](https://img.shields.io/badge/Streamlit-Latest-red.svg)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📋 Mục lục

- [Tính năng](#-tính-năng)
- [Yêu cầu hệ thống](#-yêu-cầu-hệ-thống)
- [Cài đặt](#-cài-đặt)
- [Sử dụng](#-sử-dụng)
- [Cấu trúc project](#️-cấu-trúc-project)
- [Thư viện sử dụng](#-thư-viện-sử-dụng)
- [Xử lý lỗi](#-xử-lý-lỗi)
- [Đóng góp](#-đóng-góp)

---

## 🚀 Tính năng

### ✨ Tính năng chính

- ✅ **Thêm sự kiện bằng câu tiếng Việt tự nhiên**
  - Ví dụ: *"Nhắc tôi họp nhóm lúc 10 giờ sáng mai ở phòng 302, nhắc trước 15 phút"*
  - Hỗ trợ phân tích tự động: thời gian, địa điểm, mô tả, nhắc nhở

- 📋 **Xem sự kiện linh hoạt**
  - Xem theo ngày, tuần, tháng
  - Hiển thị lịch tháng dạng lưới với các sự kiện
  - Tìm kiếm sự kiện theo từ khóa

- 🔔 **Nhắc nhở tự động**
  - Nhắc nhở trước khi sự kiện diễn ra (tùy chỉnh số phút)
  - Tự động refresh mỗi 30 giây

- ✏️ **Quản lý sự kiện**
  - Chỉnh sửa thông tin sự kiện
  - Xóa sự kiện
  - Xuất dữ liệu ra file JSON

---

## 📦 Yêu cầu hệ thống

### Phiên bản Python

| Phiên bản | Trạng thái | Ghi chú |
|-----------|------------|---------|
| **Python 3.11** | ✅ **Khuyến nghị** | Có pre-built wheels, cài đặt nhanh, **KHÔNG CẦN** Visual C++ Build Tools |
| Python 3.10 | ✅ Hoạt động tốt | |
| Python 3.9 | ✅ Hoạt động tốt | |
| Python 3.14+ | ❌ Không khuyến nghị | Chưa có pre-built wheels, cần Visual C++ Build Tools và Rust |

> **⚠️ Lưu ý**: Nếu bạn đang dùng Python 3.14+, vui lòng cài đặt Python 3.11:  
> [Download Python 3.11](https://www.python.org/downloads/release/python-3119/)

### Yêu cầu khác

- pip (trình quản lý gói Python)
- Kết nối internet (để tải các thư viện)

---

## 🔧 Cài đặt

### Bước 1: Clone hoặc tải project

```bash
# Clone repository
git clone <your-repo-url>
cd doanlichtrinh

# Hoặc tải về và giải nén
```

### Bước 2: Kiểm tra phiên bản Python

```bash
# Kiểm tra phiên bản Python hiện tại
python --version

# Hoặc nếu có nhiều phiên bản Python
py -3.11 --version
```

> **⚠️ Quan trọng**: Nếu bạn thấy Python 3.14+, vui lòng cài Python 3.11 trước khi tiếp tục.

### Bước 3: Tạo môi trường ảo (Virtual Environment)

```bash
# Tạo venv với Python mặc định (nếu đã là 3.11)
python -m venv venv

# Hoặc chỉ định Python 3.11 cụ thể
py -3.11 -m venv venv

# Kích hoạt môi trường ảo
# Trên Windows (PowerShell):
.\venv\Scripts\Activate.ps1

# Trên Windows (CMD):
venv\Scripts\activate.bat

# Trên Linux/Mac:
source venv/bin/activate
```

### Bước 4: Cài đặt các thư viện

#### 📌 Với Python 3.11: KHÔNG CẦN Visual C++ Build Tools

```bash
# Cập nhật pip
python -m pip install --upgrade pip

# Cài đặt scikit-learn bằng pre-built wheel (tránh build từ source)
python -m pip install --only-binary :all: scikit-learn

# Cài đặt các thư viện còn lại
pip install -r requirements.txt
```

#### Hoặc cài đặt từng thư viện:

```bash
pip install streamlit
pip install streamlit-autorefresh
pip install numpy
pip install --only-binary :all: scikit-learn
pip install python-dateutil
pip install underthesea
```

---

## ▶️ Chạy ứng dụng

Sau khi cài đặt xong, chạy lệnh sau để khởi động ứng dụng:

```bash
streamlit run main.py
```

Ứng dụng sẽ tự động mở trong trình duyệt tại địa chỉ: **http://localhost:8501**

> 💡 **Tip**: Nếu không tự động mở, bạn có thể truy cập thủ công bằng cách copy địa chỉ hiển thị trong terminal.

---

## 📝 Sử dụng

### Thêm sự kiện mới

Nhập câu mô tả sự kiện vào ô nhập liệu, ví dụ:

```
"Nhắc tôi họp nhóm lúc 10 giờ sáng mai ở phòng 302, nhắc trước 15 phút"
"Nhắc tôi ăn cơm lúc 8 giờ tối nay ở nhà, nhắc trước 10 phút"
"Nhắc đi làm lúc 9 giờ sáng mai ở an dương vương, nhắc trước 10 phút"
"Nhắc tôi học bài môn ai lúc 19:30 thứ hai, nhắc trước 30 phút"
"Nhắc tôi đi khám bệnh lúc 7h sáng 20/11, nhắc trước 2 giờ"
```

Sau đó nhấn nút **"Phân tích và thêm sự kiện"**.

### Xem sự kiện

Chọn chế độ xem từ dropdown:

| Chế độ | Mô tả |
|--------|-------|
| **Hôm nay** | Xem tất cả sự kiện trong ngày |
| **Tuần này** | Xem sự kiện trong tuần |
| **Tháng này** | Xem sự kiện trong tháng |
| **Lịch tháng** | Xem lịch dạng lưới với các sự kiện |
| **Tìm kiếm** | Tìm sự kiện theo từ khóa |

### Chỉnh sửa/Xóa sự kiện

1. Mở expander của sự kiện cần chỉnh sửa
2. Thay đổi thông tin cần thiết
3. Nhấn **"💾 Lưu thay đổi"** hoặc **"❌ Xóa sự kiện này"**

---

## 🗂️ Cấu trúc project

```
doanlichtrinh/
├── main.py                  # File chính chứa giao diện Streamlit
├── nlp_module.py            # Module xử lý NLP tiếng Việt
├── db.py                    # Module quản lý database SQLite
├── events.db                # Database SQLite (tự động tạo, không commit)
├── requirements.txt         # Danh sách thư viện cần cài
├── README.md               # File hướng dẫn này
├── .gitignore              # File ignore cho Git
├── test_underthesea.py     # File test thư viện underthesea
└── test_add_from_nlp.py    # File test chức năng NLP
```

---

## 🧪 Test

Bạn có thể test các module riêng lẻ:

```bash
# Test module NLP
python nlp_module.py

# Test thêm sự kiện từ NLP
python test_add_from_nlp.py

# Test database
python db.py
```

---

## 📚 Thư viện sử dụng

| Thư viện | Mục đích | Version |
|----------|----------|---------|
| [streamlit](https://streamlit.io/) | Framework tạo web app | Latest |
| [streamlit-autorefresh](https://github.com/kmcgrady/streamlit-autorefresh) | Tự động làm mới trang | Latest |
| [underthesea](https://github.com/undertheseanlp/underthesea) | Thư viện NLP tiếng Việt | Latest |
| [python-dateutil](https://dateutil.readthedocs.io/) | Xử lý ngày tháng | Latest |
| [numpy](https://numpy.org/) | Tính toán số học | Latest |
| [scikit-learn](https://scikit-learn.org/) | Machine learning (dependency của underthesea) | Latest |
| sqlite3 | Database (built-in Python) | - |

---

## ⚠️ Lưu ý

- Database SQLite (`events.db`) sẽ được tạo tự động khi chạy lần đầu
- Ứng dụng tự động refresh mỗi 30 giây để cập nhật nhắc nhở
- Nhắc nhở sẽ hiển thị khi đến thời gian đã cài đặt (trước X phút)
- File `events.db` và các file export JSON không được commit lên Git (đã có trong `.gitignore`)

---

## 🐛 Xử lý lỗi

### Lỗi khi cài đặt `underthesea` hoặc `python-crfsuite`

**Lỗi**: 
```
error: Microsoft Visual C++ 14.0 or greater is required
```

**Giải pháp**: 
- Với Python 3.11: Không cần Visual C++ Build Tools, chỉ cần cài đặt lại:
  ```bash
  pip uninstall underthesea python-crfsuite
  pip install python-crfsuite
  pip install underthesea
  ```
- Với Python 3.14+: Cần cài Visual C++ Build Tools hoặc downgrade về Python 3.11

### Lỗi khi cài đặt `scikit-learn`

**Lỗi**: 
```
scikit-learn requires GCC >= 8.0
```

**Giải pháp**: Cài đặt bằng pre-built wheel:
```bash
python -m pip install --only-binary :all: scikit-learn
```

### Lỗi khi chạy Streamlit

**Giải pháp**: Đảm bảo đã cài đặt đầy đủ:
```bash
pip install --upgrade streamlit
```

### Lỗi khi import underthesea

**Lỗi**: 
```
ModuleNotFoundError: No module named 'pycrfsuite'
```

**Giải pháp**:
1. Đảm bảo đã cài Visual C++ Build Tools (nếu dùng Python < 3.11)
2. Cài đặt lại:
   ```bash
   pip uninstall underthesea python-crfsuite
   pip install python-crfsuite
   pip install underthesea
   ```

---

## 🤝 Đóng góp

Mọi đóng góp đều được chào đón! Nếu bạn muốn đóng góp:

1. Fork project này
2. Tạo branch mới (`git checkout -b feature/AmazingFeature`)
3. Commit các thay đổi (`git commit -m 'Add some AmazingFeature'`)
4. Push lên branch (`git push origin feature/AmazingFeature`)
5. Mở Pull Request

---

## 📄 License

Project này được phát triển cho mục đích học tập và nghiên cứu.

---

## 👨‍💻 Tác giả

Được phát triển bởi [MINH KHA]

---

<div align="center">

**⭐ Nếu project này hữu ích, hãy cho một star! ⭐**

</div>
