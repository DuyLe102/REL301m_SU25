# Module 3: Advanced Function Approximation Methods

## 1. Coarse Coding

### Khái niệm cơ bản
- **Distributed representation**: Một state có thể kích hoạt nhiều features cùng lúc
- **Receptive fields**: Mỗi feature có vùng thu nhận riêng, có thể chồng lấp
- **Soft assignment**: Khác với state aggregation (hard assignment)

### Ưu điểm so với State Aggregation
- Tổng quát hóa tốt hơn nhờ overlap
- Biểu diễn liên tục và mềm dẻo
- Phù hợp với không gian trạng thái lớn và nhiều chiều

---

## 2. Tile Coding

### Nguyên lý
- **Multiple tilings**: Sử dụng nhiều lưới chồng lấp
- **Offset tilings**: Các lưới được lệch nhau một khoảng nhỏ
- **Computational efficiency**: Hiệu quả tính toán cao

### Kiểm soát tính chất
**Kích thước tile:**
- Tile lớn → tăng generalization
- Tile nhỏ → tăng discrimination

**Hình dạng tile:**
- Hình vuông: tổng quát hóa đều các chiều
- Hình chữ nhật: kiểm soát độ rộng theo từng chiều
- Co giãn chiều để điều chỉnh tầm ảnh hưởng

### Cải thiện discrimination
- **Một tiling**: tổng quát hóa trong hình vuông
- **Nhiều tiling**: tổng quát hóa theo đường chéo
- **Random offset**: tổng quát hóa hình cầu và đồng nhất

### Hạn chế
- Số lượng tiles tăng theo hàm mũ với số chiều
- Cần xử lý riêng từng chiều đầu vào
- Phụ thuộc vào đặc thù bài toán

---

## 3. Neural Networks for Non-linear Approximation

### Ưu điểm chính
- **Automatic feature learning**: Tự động học đặc trưng từ dữ liệu
- **Flexible representation**: Có thể biểu diễn hàm phức tạp
- **Universal approximation**: Có thể xấp xỉ bất kỳ hàm liên tục nào

### Cấu trúc cơ bản
**Các thành phần:**
- Input layer: nhận state
- Hidden layers: tạo intermediate representations
- Output layer: dự đoán value/action

**Activation functions:**
- ReLU: f(x) = max(0,x) - phổ biến nhất
- Sigmoid: f(x) = 1/(1+e^(-x)) - output (0,1)
- Tanh: f(x) = (e^x - e^(-x))/(e^x + e^(-x)) - output (-1,1)

### So sánh với Tile Coding
**Similarities:**
- Đều tạo features từ input
- Có thể biểu diễn hàm phức tạp
- Cần điều chỉnh hyperparameters

**Differences:**
- NN: học features tự động vs Tile Coding: features cố định
- NN: linh hoạt hơn nhưng cần nhiều data hơn
- NN: khó interpret hơn

### Receptive fields trong NN
- Mỗi neuron có vùng thu nhận riêng
- Các vùng có thể overlap
- Tạo distributed representation

---

## 4. Gradient Descent for Neural Networks

### Backpropagation Algorithm

**Forward pass:**
1. Tính output của hidden layer: x = f(AS)
2. Tính network output: ŷ = Bx
3. Tính loss function: L(ŷ, y)

**Backward pass:**
1. Tính gradient cho output weights:
   ∂L/∂B = (∂L/∂ŷ)(∂ŷ/∂B)

2. Tính gradient cho hidden weights:
   ∂L/∂A = (∂L/∂x)(∂x/∂A)

3. Chain rule để truyền gradient ngược

### Weight Updates
**Standard gradient descent:**
w_{t+1} = w_t - α∇_w L

**Key considerations:**
- Learning rate α: quá lớn → không hội tụ, quá nhỏ → học chậm
- Initialization: trọng số ban đầu ảnh hưởng lớn
- Computational efficiency: tránh tính toán lặp lại

### Practical Implementation
**ReLU example:**
- f(x) = max(0,x)
- ∂f/∂x = 1 if x > 0, else 0
- Đơn giản tính toán, tránh vanishing gradient

**Linear output layer:**
- ŷ = Bx
- ∂ŷ/∂B = x
- ∂ŷ/∂x = B

---

## 5. Key Comparisons & Trade-offs

### Method Selection Guide

**Tile Coding - Best for:**
- Low-dimensional problems (2-4 dimensions)
- Need interpretability
- Fast computation required
- Limited training data

**Neural Networks - Best for:**
- High-dimensional problems
- Complex patterns in data
- Plenty of training data available
- Don't need interpretability

### Computational Complexity
- **Tile Coding**: O(number of active tiles) - very fast
- **Neural Networks**: O(number of weights) - more expensive

### Sample Efficiency
- **Tile Coding**: Good with limited data
- **Neural Networks**: Need more data but better generalization

---

## 6. Practical Considerations

### Feature Engineering vs Automatic Learning
- Tile coding: cần thiết kế features carefully
- Neural networks: tự động học features nhưng cần architecture design

### Hyperparameter Tuning
**Tile Coding:**
- Số lượng tilings
- Kích thước tiles