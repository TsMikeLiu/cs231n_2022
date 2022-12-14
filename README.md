# cs231n_2022

code for cs231n(2022) Assignment and some learning notes.

Current Progress
================================================================
1. [Assignment 1](https://cs231n.github.io/assignments2022/assignment1/)
   - Q1: k-Nearest Neighbor classifier
   - Q2: Training a Support Vector Machine
   - Q3: Implement a Softmax classifier(2022.7.27)
   - Q4: Two-Layer Neural Network(2022.7.28)
   - Q5: Higher Level Representations: Image Features

Study Notes
================================================================
Assignment 1
------------------------------------------------
1. np.reshape():
   - np.reshape(N,-1): N rows and any columns
   - np.reshape(-1,M): any rows and N columns
2. transpose in python: 
   - np.array.T: suitable for transpose of one- or two-dimensional arrays.
   - np.array.transpose( ): suitable for high-dimensional arrays' transposition in which requires a tuple of axis numbers. e.x. for a three-dimensional array, transpose(1,0,2) means swap the first and second dimension.
3. calculate the derivatives of function in matrix is similar to the normal variables, just need to pay attention to dimension.
4. np.max() & np,maximum()
   - np.max(A,axis):get the largest number of row(axis=0) or column(axis=1)
   - np.maximum(A,B): A and B should have the same shape, get the larger number of each element.
5. It's easy to get confused when trying to calculate the derivatives of x and W. It will be clearer if we raise an example like X has 2 samples and 3 dimensions, set them to be $x_{00},x_{01},...$. so we can see $\frac{\partial L}{\partial x_{ij}}$ clearly.
6. If we want to use **broadcast**, for some one-dimensional arrays, we need to reshape it to (N,-1) or (-1,N)
7. np.random.normal(mean, std, shape)
8. In **Q4**, we shouldn't use the default learning_rate of sgd(Stochastic Gradient Descent) in the origin code which is `learning_rate = 1e-2`. This learning rate is too high for this problem, which make each step too big, so that dW is too high. It makes the loss increase exponentially.
9. Different **UPDATE RULES**:
    - sgd(Stochastic Gradient Descent):`w -= learning_rate * dW`
    - sgd_momentum: consider the momentum of the decreasing velocity.`v = momentum*v - learning_rate * dW`, `w += v`
    - RMSProp: consider the momentum of the gradient. `S_grad = decay_rate * S_grad + (1-decay_rate) * (dW**2)`,`w -= learning_rate * dW / (sqrt(S_grad)+epsilon)`.
    - $$\begin{align}&S_{d W}=\beta S_{d W}+(1-\beta) d W^{2} \\&S_{d b}=\beta S_{d b}+(1-\beta) d b^{2} \\&W=W-\alpha \frac{d W}{\sqrt{S_{d W}}+\varepsilon}, b=b-\alpha \frac{d b}{\sqrt{S_{d b}}+\varepsilon}\end{align}$$
    - adam: combine sgd_momentum and RMSProp together. Consider the first moment and second moment of history gradient.`m = beta1*m + (1-beta1)*dw`,`v = beta2*v (1-beta2)*(dw**2)`, `w -= learning_rate * m / (sqrt(v)+epsilon)` (first moment: **m**, second moment:**v**)
    - $$\begin{aligned}m_{t}=\beta_1 \times m_{t-1}+(1-\beta_1)\times dW \\ v_t =\beta_2 \times v_{t-1} + (1-\beta_2) \times dW^2 \\ W_t = W_{t-1} - \alpha \frac{m_t}{\sqrt{v_t}+\epsilon}\end{aligned}$$