# Module 4: Agent Architecture & Advanced RL Applications

## 1. Agent Architecture Design Choices

### State Representation
- **Raw vs Processed**: Quyết định sử dụng dữ liệu thô (pixels, sensors) hay features đã xử lý
- **Feature Engineering**: 
  - Bài toán nhỏ: hand-crafted features
  - Bài toán phức tạp: automated feature extraction (neural networks)
- **Dimensionality**: Ảnh hưởng đến kích thước và tính khả thi của state space

### Action Representation
- **Discrete vs Continuous**: 
  - Discrete: {up, down, left, right}
  - Continuous: steering angles, force values
- **Action Encoding**: one-hot hoặc parameterized

### Policy Representation
- **Tabular**: Cho state-action spaces nhỏ
- **Parameterized**: Linear hoặc neural networks cho spaces lớn
- **Stochastic vs Deterministic**: Output probabilities vs fixed actions

### Value Function Representation
- **Tabular**: Lưu value cho mỗi state/state-action pair
- **Function Approximation**: Linear (tile coding) hoặc nonlinear (deep NN)

## 2. Learning Algorithms

### Các loại chính:
1. **Value-Based**: Học value functions → derive policies (Q-learning, Sarsa)
2. **Policy-Based**: Học policy trực tiếp (Policy Gradient, REINFORCE)
3. **Actor-Critic**: Kết hợp cả hai, có actor (policy) và critic (value)

### Exploration Strategies:
- **Epsilon-Greedy**: Random explore với xác suất ε
- **Softmax/Entropy-Based**: Explore dựa trên uncertainty
- **Optimistic Initialization**: Bắt đầu với value estimates lạc quan

## 3. Neural Networks trong RL

### Ưu điểm:
- Approximation phi tuyến mạnh mẽ
- Capture được mối quan hệ phức tạp giữa states, actions, values
- Generalize tốt across similar states/actions

### TD Error Loss cho Q-learning với NN:
$$\text{Loss} = \left(R_{t+1} + \gamma \max_{a'} Q(s_{t+1}, a'; w^-) - Q(s_t, a_t; w)\right)^2$$

Trong đó:
- $w$: neural network weights
- $w^-$: target network weights

### Kỹ thuật ổn định:
- Experience replay
- Target networks
- Gradient clipping

## 4. System Identification & Model-Based RL

### Quy trình:
1. **Collect Data** → Learn environment model
2. **Fit Model** → Predict future states/rewards  
3. **Plan/Optimize** → Use model for policy optimization
4. **Deploy & Iterate** → Collect more data, improve model

### Optimal Control:
- Sử dụng learned model để tính control strategies
- Optimize performance criterion
- Agnostic methods: Strong guarantees khi true system không nằm trong assumed model class

## 5. RL trong Mobile Health (mHealth)

### Đặc điểm:
- **Environment**: Highly dynamic, user context thay đổi liên tục
- **Interventions**: Activity reminders, stress management prompts
- **Challenges**: High noise, small samples, minimally intrusive

### Average Reward Objective:
$$\bar{r}_\pi = \lim_{T \to \infty} \frac{1}{T} \mathbb{E}_\pi \left[ \sum_{t=1}^T R_t \right]$$

### Approach:
- **Micro-randomized trials (MRTs)**: Thu thập data cho offline RL
- **Online adaptation**: Real-time personalization
- **Decision rules**: Khi nào và như thế nào deliver interventions

## 6. Key Takeaways

### Design Principles:
- **Modular Design**: Separation of concerns, easy swapping components
- **Scalability**: Design cho larger problems, distributed architectures
- **Flexibility**: Easy experimentation và real-world deployment

### Trade-offs:
- **Learning efficiency vs Scalability**
- **Stability vs Adaptability** 
- **Sample efficiency vs Computational cost**

### Practical Considerations:
- Update mechanisms: Online vs Batch, Synchronous vs Asynchronous
- Memory: Experience replay, eligibility traces
- Architecture impacts: Learning efficiency, generalization ability
