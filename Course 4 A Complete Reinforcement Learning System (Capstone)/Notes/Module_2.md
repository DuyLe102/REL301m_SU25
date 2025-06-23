## 1. Formalizing RL Problems

### Key Steps để chuyển real-world problem thành MDP:

1. **Mô tả bài toán thực tế** – Xác định mục tiêu và lý do sử dụng RL  
2. **Định nghĩa các thành phần của MDP**:
   - **States (S)**: Thông tin mô tả tình huống tại mỗi time step  
   - **Actions (A)**: Các lựa chọn của agent ở mỗi state  
   - **Rewards (R)**: Phản hồi sau khi thực hiện action  
   - **Transitions (P)**: Mô tả cách environment thay đổi theo actions  
   - **Episode type**: Episodic hay continuing?

3. **Định nghĩa tiêu chí thành công** – Đo lường hiệu quả như thế nào  
4. **Thảo luận các ràng buộc và giả định**

### Best Practices:
- Thảo luận với stakeholders
- Ghi chép kỹ lưỡng để tham khảo sau
- Luôn sẵn sàng chỉnh sửa lại problem formulation

---

## 2. Markov Decision Processes (MDPs)

### Định nghĩa
MDP là framework toán học dùng để mô hình hóa quyết định trong môi trường có yếu tố ngẫu nhiên và có kiểm soát.

### Thành phần chính: 

$$
(S, A, P, R, \gamma)
$$

| Component    | Ký hiệu     | Mô tả                                  |
|--------------|-------------|-----------------------------------------|
| States       | \( S \)     | Tập hợp tất cả các trạng thái có thể   |
| Actions      | \( A \)     | Tập hợp tất cả các hành động có thể    |
| Transitions  | \( P \)     | \( P(s'|s,a) \): Xác suất chuyển trạng thái |
| Rewards      | \( R \)     | \( R(s,a,s') \): Phần thưởng tức thì    |
| Discount     | \( gamma \) | Hệ số chiết khấu phần thưởng tương lai |

### Markov Property

**"Memoryless"** – Trạng thái tương lai chỉ phụ thuộc vào trạng thái hiện tại và hành động, không phụ thuộc lịch sử.

### Policies và Value Functions

- **Policy** \( \pi \): Quy tắc chọn hành động tại mỗi trạng thái  
  - Deterministic: Luôn chọn cùng một hành động  
  - Stochastic: Chọn theo phân phối xác suất  

- **Value Functions**:
  - \( V^{\pi}(s) \): Kỳ vọng tổng phần thưởng bắt đầu từ trạng thái \( s \) theo policy \( \pi \)
  - \( Q^{\pi}(s,a) \): Kỳ vọng tổng phần thưởng bắt đầu từ \( s \), thực hiện hành động \( a \), theo policy \( \pi \)

### Phương trình Bellman

$$
V^{\pi}(s) = \sum_{a} \pi(a|s) \sum_{s'} P(s'|s,a) \left[ R(s,a,s') + \gamma V^{\pi}(s') \right]
$$

### Giải MDPs

- **Value Iteration**: Cập nhật giá trị → trích xuất policy tối ưu  
- **Policy Iteration**: Luân phiên đánh giá và cải tiến policy

---

## 3. Episodic vs Continuing Tasks

### Episodic Tasks

- **Đặc điểm**: Có trạng thái kết thúc, thời gian hữu hạn, có điểm bắt đầu/kết thúc rõ ràng  
- **Return**:

$$
G_t = R_{t+1} + R_{t+2} + \dots + R_T
$$

- **Ví dụ**: Trò chơi, game, giải mê cung  
- **Thuật toán phù hợp**: Monte Carlo methods, evaluation theo episode

### Continuing Tasks

- **Đặc điểm**: Không có điểm kết thúc rõ ràng, vô hạn  
- **Return**:

$$
G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}
$$

- **Ví dụ**: Điều khiển hệ thống, giao dịch tài chính  
- **Thuật toán phù hợp**: Temporal Difference learning, average reward methods

---

## 4. Eligibility Traces

### Định nghĩa
Cơ chế để giải bài toán **temporal credit assignment** – xác định những trạng thái/hành động trong quá khứ nào nên nhận credit cho phần thưởng hiện tại.

### Tại sao gọi là "Eligibility Traces"?
Vì chỉ một số trạng thái/hành động nhất định đủ điều kiện nhận credit cho phần thưởng tại thời điểm nhất định.

### Công thức:

$$
E_t(s) = \gamma \lambda E_{t-1}(s) + \mathbf{1}(S_t = s)
$$

Trong đó:
- \( \gamma \): Discount factor  
- \( \lambda \): Trace-decay parameter  
- \( \mathbf{1}(S_t = s) \): Hàm chỉ báo (1 nếu trạng thái hiện tại là \( s \), 0 nếu không)

### Forward vs Backward View

- **Forward View**: Dạng lý thuyết – kết hợp TD và Monte Carlo  
- **Backward View**: Dạng thuật toán – bộ nhớ suy giảm theo thời gian

### Lợi ích

- Học nhanh hơn  
- Phân bổ credit rõ ràng và hợp lý  
- Kết nối lý thuyết giữa TD và Monte Carlo

---

## 5. Key Takeaways

1. Formalization bằng MDP là bước quan trọng đầu tiên  
2. Markov Property đảm bảo chỉ trạng thái và hành động hiện tại quan trọng  
3. Phân biệt rõ giữa Episodic và Continuing tasks để chọn thuật toán phù hợp  
4. Eligibility Traces giúp học nhanh và hiệu quả hơn  
5. Bellman Equation là trung tâm để tính toán giá trị và trích xuất chính sách tối ưu

---

## Quick Reference

- MDP Tuple: 

  $$
  (S, A, P, R, \gamma)
  $$

- Bellman:

  $$
  V^{\pi}(s) = \mathbb{E}_{\pi} \left[ R + \gamma V^{\pi}(s') \right]
  $$

- Episodic Return:

  $$
  G_t = \sum_{k=0}^{T-t-1} R_{t+k+1}
  $$

- Continuing Return:

  $$
  G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}
  $$

- Eligibility Trace:

  $$
  E_t(s) = \gamma \lambda E_{t-1}(s) + \mathbf{1}(S_t = s)
  $$

