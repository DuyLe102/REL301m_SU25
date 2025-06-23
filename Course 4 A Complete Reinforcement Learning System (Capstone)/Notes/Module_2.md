## 1. Formalizing RL Problems

### Key Steps để chuyển real-world problem thành MDP:

1. **Mô tả bài toán thực tế** – Xác định mục tiêu và lý do sử dụng RL  
2. **Định nghĩa các thành phần của MDP**:
   - **States ($S$)**: Thông tin mô tả tình huống tại mỗi time step  
   - **Actions ($A$)**: Các lựa chọn của agent ở mỗi state  
   - **Rewards ($R$)**: Phản hồi sau khi thực hiện action  
   - **Transitions ($P$)**: $P(s'|s,a)$ mô tả cách environment thay đổi theo actions  
   - **Episode type**: Episodic hay continuing?

3. **Định nghĩa tiêu chí thành công** – Đo lường hiệu quả như thế nào  
4. **Thảo luận các ràng buộc và giả định**

## 2. Markov Decision Processes (MDPs)

### Định nghĩa
MDP là framework toán học dùng để mô hình hóa quyết định trong môi trường có yếu tố ngẫu nhiên và có kiểm soát.

### Thành phần chính: 

$$
\langle S, A, P, R, \gamma \rangle
$$

| Component    | Ký hiệu     | Mô tả                                  |
|--------------|-------------|----------------------------------------|
| States       | $S$         | Tập hợp tất cả các trạng thái có thể   |
| Actions      | $A$         | Tập hợp tất cả các hành động có thể    |
| Transitions  | $P$         | $P(s'\|s,a)$: Xác suất chuyển trạng thái |
| Rewards      | $R$         | $R(s,a,s')$: Phần thưởng tức thì       |
| Discount     | $\gamma$    | Hệ số chiết khấu phần thưởng tương lai |

### Markov Property

**"Memoryless"** – Trạng thái tương lai chỉ phụ thuộc vào trạng thái hiện tại và hành động, không phụ thuộc lịch sử.

### Policies và Value Functions

- **Policy $\pi$**: Quy tắc chọn hành động tại mỗi trạng thái  
  - Deterministic: $a = \pi(s)$  
  - Stochastic: $\pi(a|s)$  

- **Value Functions**:
  - $V^{\pi}(s)$: Kỳ vọng tổng phần thưởng từ $s$ theo $\pi$
  - $Q^{\pi}(s,a)$: Kỳ vọng tổng phần thưởng từ $(s,a)$ theo $\pi$

### Phương trình Bellman

$$
V^{\pi}(s) = \sum_{a} \pi(a|s) \sum_{s'} P(s'|s,a) \left[ R(s,a,s') + \gamma V^{\pi}(s') \right]
$$

## 3. Episodic vs Continuing Tasks

### Episodic Tasks

- **Return**:

$$
G_t = \sum_{k=0}^{T-t-1} R_{t+k+1}
$$

### Continuing Tasks

- **Return**:

$$
G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}
$$

## 4. Eligibility Traces

### Công thức:

$$
E_t(s) = \gamma \lambda E_{t-1}(s) + \mathbb{I}(S_t = s)
$$

Trong đó:
- $\gamma$: Discount factor  
- $\lambda$: Trace-decay parameter  
- $\mathbb{I}(S_t = s)$: Hàm chỉ báo (1 nếu $S_t = s$, 0 nếu khác)

## Quick Reference

- MDP Tuple: $\langle S, A, P, R, \gamma \rangle$
- Bellman: $V^{\pi}(s) = \mathbb{E}_{\pi} \left[ R + \gamma V^{\pi}(s') \right]$
- Episodic Return: $G_t = \sum_{k=0}^{T-t-1} R_{t+k+1}$
- Continuing Return: $G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}$
- Eligibility Trace: $E_t(s) = \gamma \lambda E_{t-1}(s) + \mathbb{I}(S_t = s)$
