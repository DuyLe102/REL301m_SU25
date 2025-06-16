# Module 4: Xấp Xỉ Hàm trong Reinforcement Learning

## 1. Episodic Sarsa với Xấp Xỉ Hàm

### Khái niệm cơ bản
- **Mục đích**: Xử lý không gian trạng thái lớn bằng cách sử dụng xấp xỉ hàm
- **Ưu điểm**: Không cần lưu trữ bảng Q-table khổng lồ

### Biểu diễn toán học
**Vector đặc trưng và trọng số:**
- Vector trọng số: w ∈ ℝᵈ
- Vector đặc trưng: φ(s,a) ∈ ℝᵈ  
- Giá trị hành động: q̂(s,a,w) = wᵀφ(s,a)

### Cập nhật trọng số
```
w_{t+1} = w_t + α × δ_t × ∇_w q̂(S_t,A_t,w_t)
```

Trong đó:
- α: learning rate
- δ_t: TD error
- ∇_w q̂: gradient của hàm xấp xỉ

### Phương pháp biểu diễn
**Tile Coding:**
- Đặc trưng cố định, hiệu quả tính toán
- Phù hợp với bài toán có cấu trúc đơn giản

**Mạng Neural:**
- Học được đặc trưng tự động
- Mạnh mẽ hơn nhưng phức tạp hơn

---

## 2. Phần Thưởng Trung Bình (Average Reward)

### Động lực
- **Vấn đề**: Discount factor γ có thể không phù hợp với một số bài toán
- **Giải pháp**: Tối ưu hóa phần thưởng trung bình dài hạn

### Định nghĩa phần thưởng trung bình
```
R_π = lim_{t→∞} (1/t) × Σ_{k=0}^{t-1} R_k
```

### Phần thưởng vi phân (Differential Reward)
```
G_t = (R_{t+1} - R_π) + (R_{t+2} - R_π) + ...
```

**Ý nghĩa**: Đo lường mức độ vượt trội so với phần thưởng trung bình

### Hàm giá trị vi phân
```
v_π(s) = E_π[G_t | S_t = s]
```

### Tần suất thăm trạng thái
- μ_π(s): tần suất dài hạn thăm trạng thái s
- Σ_s μ_π(s) = 1
- Phần thưởng trung bình = Σ_s μ_π(s) × r(s)

### Sarsa vi phân
**Khác biệt chính:**
- Theo dõi và cập nhật R_π liên tục
- Sử dụng phần thưởng vi phân thay vì phần thưởng gốc
- Không cần discount factor γ

---

## 3. Khám Phá trong Xấp Xỉ Hàm

### Thách thức chính
**Vấn đề cập nhật liên kết:**
- Mỗi lần cập nhật ảnh hưởng đến nhiều trạng thái
- Khó duy trì tính optimistic cho từng trạng thái riêng lẻ

### Giá trị khởi tạo lạc quan (Optimistic Initialization)
**Nguyên tắc:**
- Khởi tạo giá trị cao hơn giá trị thực tế
- Khuyến khích agent khám phá các hành động chưa thử

**Thách thức trong function approximation:**
- Cập nhật một trạng thái ảnh hưởng đến nhiều trạng thái khác
- Cần cơ chế cập nhật cục bộ để duy trì tính optimistic

### Epsilon-Greedy
**Ưu điểm:**
- Đơn giản, dễ cài đặt
- Áp dụng được cho mọi loại function approximation

**Nhược điểm:**
- Khám phá không có định hướng
- Không tận dụng được thông tin từ function approximation

### Giải pháp đề xuất
**Cập nhật cục bộ:**
- Chỉ cập nhật cho trạng thái hiện tại
- Giảm thiểu ảnh hưởng đến các trạng thái khác
- Cân bằng giữa khám phá và khai thác

---

## Tóm tắt chính

### Ưu điểm của Function Approximation
1. Xử lý được không gian trạng thái lớn
2. Khả năng tổng quát hóa tốt
3. Tiết kiệm bộ nhớ

### Thách thức chính
1. **Khám phá**: Khó duy trì optimistic initialization
2. **Convergence**: Không đảm bảo hội tụ như tabular methods
3. **Hyperparameter tuning**: Cần điều chỉnh learning rate, architecture

### Lời khuyên thực hành
- Bắt đầu với tile coding cho bài toán đơn giản
- Sử dụng neural networks cho bài toán phức tạp
- Cân nhắc average reward cho bài toán continuous
- Luôn theo dõi quá trình training để phát hiện overfitting

---

*Ghi chú: Module này là nền tảng cho Deep RL và các phương pháp hiện đại như DQN, Policy Gradient...*