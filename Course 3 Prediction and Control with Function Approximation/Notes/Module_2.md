# Module 2: Function Approximation & Gradient Methods

## 1. Tại Sao Cần Hàm Tham Số Hóa?

### Vấn đề với Tabular Methods
- ❌ Không gian trạng thái quá lớn (tỷ states)
- ❌ Trạng thái liên tục → không thể lưu bảng
- ❌ Tốn RAM quá nhiều
- ❌ Không tổng quát hóa được

### Giải pháp: Function Approximation
- ✅ Biểu diễn gọn gàng với tham số w
- ✅ Tổng quát hóa cho states chưa thấy
- ✅ Tiết kiệm bộ nhớ
- ✅ Xử lý được continuous states

---

## 2. Các Loại Hàm Xấp Xỉ

### Linear Function
$$\hat{v}(s,w) = w^T \phi(s)$$
- w: vector trọng số
- φ(s): feature vector của state s

### Non-linear Function
- Neural Networks 
- Polynomial functions
- RBF (Radial Basis Function)

---

## 3. Gradient Descent Cơ Bản

### Công thức cập nhật
$$\theta_{t+1} = \theta_t - \alpha \nabla_\theta J(\theta_t)$$

**Giải thích đơn giản:**
- θ: tham số cần học
- α: learning rate (tốc độ học)
- ∇J: gradient (hướng tăng nhanh nhất)
- Đi ngược hướng gradient để minimize J

### 3 Variants:
1. **Batch GD**: Dùng toàn bộ data → chậm nhưng ổn định
2. **Stochastic GD**: Dùng 1 sample → nhanh nhưng noisy
3. **Mini-batch GD**: Dùng 1 batch nhỏ → cân bằng tốt ⭐

---

## 4. Value Estimation = Supervised Learning

### Cấu trúc bài toán
- **Input**: state s
- **Output**: value v(s)
- **Loss function**: MSE giữa true value và predicted value

$$J(w) = \frac{1}{2} \mathbb{E}[(v_{\pi}(s) - \hat{v}(s,w))^2]$$

### Khác biệt với SL thông thường:
- Data phụ thuộc thời gian
- Distribution shift liên tục
- Cần xử lý bootstrap

---

## 5. Monte Carlo Gradient Method

### Idea: Dùng actual returns làm target
$$w_{t+1} = w_t + \alpha[G_t - \hat{v}(S_t,w_t)]\nabla_w \hat{v}(S_t,w_t)$$

### Ưu nhược điểm:
- ✅ Unbiased (không thiên vị)
- ✅ Đơn giản implement
- ❌ Phải đợi end episode
- ❌ High variance
- ❌ Học chậm

---

## 6. Semi-Gradient TD Method

### Idea: Dùng bootstrap làm target
$$\delta_t = R_{t+1} + \gamma \hat{v}(S_{t+1},w_t) - \hat{v}(S_t,w_t)$$
$$w_{t+1} = w_t + \alpha \delta_t \nabla_w \hat{v}(S_t,w_t)$$

### Ưu nhược điểm:
- ✅ Online learning
- ✅ Low variance
- ✅ Hội tụ nhanh
- ❌ Biased (do bootstrap)
- ❌ Có thể không converge

---

## 7. Generalization vs Discrimination

### Trade-off quan trọng:
- **Generalization** : Khả năng áp dụng cho states mới
- **Discrimination** : Khả năng phân biệt các states khác nhau

### Phương pháp cân bằng:
1. **Tile Coding**: Chia space thành grids chồng lấp
2. **Coarse Coding**: Dùng circles chồng lấp
3. **Neural Networks**: Tự học features

---

## 8. Key Takeaways 

1. **Function approximation** giải quyết curse of dimensionality
2. **Gradient descent** là backbone của modern RL
3. **MC methods**: unbiased nhưng high variance
4. **TD methods**: biased nhưng low variance, learn faster
5. **Generalization-discrimination trade-off** cần cân bằng
6. **Feature engineering** rất quan trọng với linear functions

---
