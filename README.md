# [BTL] Dự đoán hành vi Streamer trên Twitch bằng thuật toán MUSAE (Multi-Scale Attributed Node Embedding)

**Nhóm thực hiện:** Nhóm 7  
**Bài báo tham khảo:** Multi-Scale attributed node embedding (Benedek Rozemberczki, Carl Allen, Rik Sarkar - 2021)

## 1. Giới thiệu dự án
Dự án này ứng dụng thuật toán Học máy trên Đồ thị **MUSAE** để giải quyết bài toán phân loại nhị phân trên mạng xã hội Twitch. Cụ thể, mô hình sẽ dự đoán xem một Streamer có sử dụng **ngôn ngữ nhạy cảm (Explicit Language)** hay không, dựa trên hai yếu tố:
1. **Cấu trúc mạng lưới:** Mối quan hệ kết nối (bạn bè/khán giả chung) giữa các Streamer.
2. **Đặc trưng cá nhân (Node Features):** Số lượt xem, thói quen streaming, game yêu thích, v.v.

Khác với các thuật toán truyền thống chỉ gộp chung đặc trưng, MUSAE trích xuất biểu diễn (embeddings) đa tỉ lệ (multi-scale), giúp phân biệt rõ ràng đặc trưng của những người hàng xóm gần và những người ở xa trong mạng lưới.

## 2. Tập dữ liệu (Dataset)
Dự án sử dụng bộ dữ liệu **Twitch Social Networks (Tập PT - Bồ Đào Nha)** do Đại học Stanford (SNAP) cung cấp.
- **Nodes (Đỉnh):** 1,912 Streamer.
- **Edges (Cạnh):** 31,299 mối quan hệ tương tác.
- **Features (Đặc trưng):** 3,169 chiều (games, habits,...).
- **Target (Nhãn):** `1` (Có sử dụng ngôn ngữ nhạy cảm) và `0` (Không sử dụng).

## 3. Quy trình thực hiện
Mã nguồn trong dự án đã được tự động hóa hoàn toàn theo các bước:
1. **Thu thập dữ liệu:** Tự động tải file nén `twitch.zip` trực tiếp từ máy chủ Stanford SNAP và trích xuất tập dữ liệu PT (Bồ Đào Nha).
2. **Trích xuất đặc trưng (Feature Extraction):** Chạy mã nguồn tham chiếu chính thức của thuật toán MUSAE để sinh ra vector nhúng (embeddings) kích thước 128 chiều cho mỗi Streamer.
3. **Huấn luyện mô hình (Classification):** Kết hợp vector MUSAE với nhãn thực tế để huấn luyện mô hình **Logistic Regression**. Tập dữ liệu được chia theo tỉ lệ 80% Train - 20% Test.

## 4. Hướng dẫn sử dụng
Toàn bộ mã nguồn và quá trình xử lý được gói gọn trong một file Google Colab duy nhất.
1. Mở file `Nhom7_Twitch_MUSAE_Classification.ipynb` trên Google Colab.
2. Cấp quyền chạy mã (Run all).
3. Code sẽ tự động tải mã nguồn MUSAE của tác giả từ GitHub, tải dữ liệu từ Stanford, chạy thuật toán và in ra **Bảng đánh giá (Classification Report)** cuối cùng bao gồm các chỉ số `Precision`, `Recall`, và `F1-score`.

## 5. Thư viện sử dụng
- `networkx`, `gensim` (Xử lý đồ thị và Random Walks)
- `scikit-learn` (Huấn luyện Logistic Regression và đánh giá)
- `pandas`, `numpy` (Xử lý ma trận dữ liệu)
