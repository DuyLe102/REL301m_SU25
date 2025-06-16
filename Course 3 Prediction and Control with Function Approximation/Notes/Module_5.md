# Module 5: Policy Gradient & Actor-Critic Methods

## 1. Policy Gradient Theorem
**Mục tiêu**: Tối đa hóa phần thưởng trung bình bằng gradient ascent.  
**Công thức**:  
$$\nabla_\theta J(\theta) = \mathbb{E}_\pi[\nabla_\theta \log \pi(A_t|S_t,\theta)q_\pi(S_t,A_t)]$$  
- $J(\theta)$: Phần thưởng trung bình.  
- $\pi(A_t|S_t,\theta)$: Chính sách tham số hóa.  
- $q_\pi(S_t,A_t)$: Giá trị hành động.  

**Ưu điểm**:  
- Không cần mô hình môi trường.  
- Hiệu quả với dữ liệu mẫu.  

---

## 2. Học Chính Sách Trực Tiếp
**Softmax Policy**:  
$$\pi(a|s) = \frac{e^{h(s,a,\theta)}}{\sum_b e^{h(s,b,\theta)}}$$  
- $h(s,a,\theta)$: Hàm ưu tiên hành động (vd: tuyến tính hoặc neural network).  
- Đảm bảo:  
  - Xác suất không âm.  
  - Tổng xác suất bằng 1.  

**So sánh với Epsilon-Greedy**:  
- Softmax: Phân phối mềm dẻo, ưu tiên hành động tốt hơn.  
- Epsilon-Greedy: Có thể chọn hành động kém do khám phá.  

---

## 3. Ước Lượng Policy Gradient
**Cập nhật tham số**:  
$$\theta = \theta + \alpha \nabla_\theta \log \pi(a|s) Q(s,a)$$  
- $\alpha$: Tốc độ học.  
- $\nabla_\theta \log \pi$: Gradient log chính sách (dễ tính toán).  

**Lý do dùng log**:  
$$\nabla_\theta \pi = \pi \nabla_\theta \log \pi$$  

---

## 4. Actor-Critic Methods
**Cấu trúc**:  
- **Actor**: Cập nhật chính sách $\pi(a|s,\theta)$ dựa trên gradient.  
- **Critic**: Đánh giá hành động qua $V(s)$ (TD learning).  

**Công thức**:  
- **TD Error**:  
  $$\delta_t = r_t + \gamma V(s_{t+1}) - V(s_t)$$  
- **Cập nhật Actor**:  
  $$\theta_{t+1} = \theta_t + \alpha \delta_t \nabla_\theta \log \pi(a_t|s_t)$$  
- **Cập nhật Critic**:  
  $$\Delta w = \alpha \delta_t \phi(s_t)$$  

**Ưu điểm**:  
- Giảm phương sai so với Monte Carlo.  
- Học trực tuyến, phản hồi nhanh.  

---

## 5. Thuật Toán Actor-Critic Đầy Đủ
**Bước 1**: Khởi tạo $\theta$ (Actor), $w$ (Critic), tốc độ học $\alpha_\theta$, $\alpha_w$.  
**Bước 2**: Lặp:  
1. Chọn hành động $a \sim \pi(\cdot|s,\theta)$.  
2. Nhận $(s', r)$ từ môi trường.  
3. Tính $\delta_t = r + \gamma V(s') - V(s)$.  
4. Cập nhật Critic: $w \leftarrow w + \alpha_w \delta_t \phi(s)$.  
5. Cập nhật Actor: $\theta \leftarrow \theta + \alpha_\theta \delta_t \nabla_\theta \log \pi(a|s)$.  

**Ứng dụng**: Robot, game, môi trường liên tục.  