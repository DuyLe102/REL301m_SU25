## 1. Choosing the Right RL Algorithm

### Key Factors trong Algorithm Selection:

1. **Task Type**
   - Episodic hay Continuing?
   - Duration và structure như thế nào?

2. **State & Action Spaces**
   - Discrete hay Continuous?
   - Size: Small (tabular) hay Large (function approximation)?

3. **Exploration Requirements**
   - Exploration vs Exploitation balance
   - Risk tolerance của environment

4. **Computational Constraints**
   - Time limitations
   - Resource availability
   - Real-time requirements

5. **Learning Objective**
   - Discounted return
   - Average reward
   - Other specific objectives

### Algorithm Families Overview:

| Family           | Characteristics          | Examples                   | Best For                        |
|------------------|---------------------------|-----------------------------|----------------------------------|
| Tabular Methods  | Small discrete spaces     | Q-learning, SARSA          | Simple, well-defined problems   |
| Value-Based      | Learn value functions     | DQN, Q-learning            | Discrete action spaces          |
| Policy-Based     | Learn policies directly   | REINFORCE, Policy Gradient | Continuous actions              |
| Actor-Critic     | Hybrid approach           | A2C, DDPG                  | Complex, continuous problems    |

---

## 2. Core RL Algorithms

### Q-Learning (Off-Policy)

**Đặc điểm**: Learns optimal policy while following exploratory policy

**Update Formula**:

$$
Q(s,a) \leftarrow Q(s,a) + \alpha \left[ r + \gamma \max_{a'} Q(s',a') - Q(s,a) \right]
$$

**Key Points**:
- Model-free
- Off-policy learning
- Guaranteed convergence (với điều kiện)
- Widely used in DQN

---

### Expected SARSA (Hybrid)

**Đặc điểm**: Blends SARSA và Q-learning strengths, less noisy updates

**Update Formula**:

$$
Q(s,a) \leftarrow Q(s,a) + \alpha \left[ r + \gamma \sum_{a'} \pi(a'|s') Q(s',a') - Q(s,a) \right]
$$

**Advantages**:
- More stable than SARSA
- Can be on-policy or off-policy
- Q-learning là special case (greedy policy)
- Better for stochastic environments

---

### Actor-Critic

**Concept**: Actor (policy) + Critic (value function)

**Core Steps**:

1. TD Error:

$$
\delta_t = r_{t+1} + \gamma v_w(s_{t+1}) - v_w(s_t)
$$

2. Critic Update:

$$
w \leftarrow w + \alpha_c \delta_t \nabla_w v_w(s_t)
$$

3. Actor Update:

$$
\theta \leftarrow \theta + \alpha_a \delta_t \nabla_{\theta} \log \pi_{\theta}(a_t|s_t)
$$

**Benefits**:
- Efficient for large/continuous spaces
- Can handle stochastic policies
- Extensible (eligibility traces, deep networks)

---

## 3. Average Reward Formulation

### Concept

Alternative to discounted rewards, especially for continuing tasks.

**Objective**:

$$
\bar{r}_{\pi} = \lim\limits_{T \to \infty} \frac{1}{T} \mathbb{E}_{\pi} \left[ \sum_{t=1}^T R_t \right]
$$

### When to Use:
- Infinite-horizon continuing tasks
- No natural episodes
- Long-term average performance matters
- Examples: Process control, resource management

### Algorithms:
- Differential SARSA
- Average Reward Actor-Critic
- Differential value functions
