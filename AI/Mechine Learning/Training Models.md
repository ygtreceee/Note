# Training Models

## Linear Regression

#### The Normal Equation

```py
import numpy as np

X = 2 * np.random.rand(100, 1)
y = 4 + 3 * X + np.random.randn(100, 1)
```

这段代码使用NumPy库生成一个包含随机数据的特征矩阵`X`和目标值矩阵`y`，用于模拟一个简单的线性回归问题。

具体解释如下：

1. `import numpy as np`：这行代码导入NumPy库，使我们能够使用其中的函数和数据类型。

1. `X = 2 * np.random.rand(100, 1)`：这行代码生成一个形状为`(100, 1)`的随机浮点数数组`X`，取值范围在0到2之间。这个数组将作为特征矩阵，其中每行代表一个样本，每列代表一个特征。

1. `y = 4 + 3 * X + np.random.randn(100, 1)`：这行代码根据线性关系生成目标值矩阵`y`。它将基于特征矩阵`X`，按照线性方程`y = 4 + 3*X + noise`生成目标值。`np.random.randn(100, 1)`部分添加了服从标准正态分布的随机噪声，以模拟真实数据中的随机误差。

通过这段代码，我们可以生成一个简单的线性回归问题，其中特征矩阵`X`包含100个样本，每个样本有一个特征，目标值矩阵`y`对应于每个样本的目标输出。我们可以使用这些数据来训练和评估线性回归模型。

```py
plt.plot(X, y, "b.")
plt.xlabel("$x_1$", fontsize=18)
plt.ylabel("$y$", rotation=0, fontsize=18)
plt.axis([0, 2, 0, 15])
save_fig("generated_data_plot")
plt.show()
```

这段代码使用matplotlib库将生成的数据进行可视化。

具体解释如下：

1. `plt.plot(X, y, "b.")`：这行代码使用蓝色的点来绘制特征矩阵`X`和目标值矩阵`y`之间的关系。每个点的横坐标是特征矩阵的值`X`，纵坐标是对应的目标值`y`。

1. `plt.xlabel("$x_1$", fontsize=18)`：这行代码设置x轴的标签为"$x_1$"，并设置字体大小为18。

1. `plt.ylabel("$y$", rotation=0, fontsize=18)`：这行代码设置y轴的标签为"$y$"，并设置字体大小为18。`rotation=0`表示标签不需要旋转。

1. `plt.axis([0, 2, 0, 15])`：这行代码设置坐标轴的取值范围。x轴的范围是0到2，y轴的范围是0到15。

1. `save_fig("generated_data_plot")`：这行代码将图像保存为文件。文件名为"generated_data_plot"。

1. `plt.show()`：这行代码显示绘制的图像。

通过这段代码，我们可以绘制生成的数据的散点图，并添加合适的标签和坐标轴范围。这有助于我们观察数据之间的关系和趋势。

```py
X_b = np.c_[np.ones((100, 1)), X]  # add x0 = 1 to each instance
theta_best = np.linalg.inv(X_b.T.dot(X_b)).dot(X_b.T).dot(y)
theta_best
```

这段代码对特征矩阵 `X` 进行扩展，添加了一个全为 1 的列作为新的特征 x0，然后使用最小二乘法求解线性回归模型的最优参数。

具体解释如下：

1. `X_b = np.c_[np.ones((100, 1)), X]`：这行代码使用 `np.ones` 创建一个形状为 `(100, 1)` 的全为 1 的数组，然后使用 `np.c_` 函数将这个数组与特征矩阵 `X` 按列连接起来，生成一个新的特征矩阵 `X_b`。这样做是为了在特征矩阵中添加一个新的特征 x0，其值都为 1，用于表示截距。

1. `theta_best = np.linalg.inv(X_b.T.dot(X_b)).dot(X_b.T).dot(y)`：这行代码使用最小二乘法求解线性回归模型的最优参数。首先，`X_b.T.dot(X_b)` 计算特征矩阵 `X_b` 的转置与自身的乘积，然后使用 `np.linalg.inv` 求解这个乘积的逆矩阵。接着，将逆矩阵与 `X_b.T` 进行乘积，再与目标值矩阵 `y` 进行乘积，得到最优参数 `theta_best`。

通过这段代码，我们可以得到根据线性回归模型拟合数据得到的最优参数 `theta_best`，其中包括截距和斜率。这些参数可以用于预测新的样本或对模型进行进一步的分析。

```py
X_new = np.array([[0], [2]])
X_new_b = np.c_[np.ones((2, 1)), X_new]  # add x0 = 1 to each instance
y_predict = X_new_b.dot(theta_best)
y_predict
```

这段代码用于使用训练好的线性回归模型参数 `theta_best` 对新的样本进行预测。

具体解释如下：

1. `X_new = np.array([[0], [2]])`：这行代码创建一个形状为 `(2, 1)` 的新特征矩阵 `X_new`，其中包含两个新样本。这些样本的特征值分别为 0 和 2。

1. `X_new_b = np.c_[np.ones((2, 1)), X_new]`：这行代码对新特征矩阵 `X_new` 进行扩展，添加了一个全为 1 的列作为新的特征 x0，生成一个新的扩展特征矩阵 `X_new_b`。

1. `y_predict = X_new_b.dot(theta_best)`：这行代码使用线性回归模型的最优参数 `theta_best` 对新扩展特征矩阵 `X_new_b` 进行预测。通过矩阵乘法运算，得到预测值 `y_predict`。

通过这段代码，我们可以使用训练好的线性回归模型对新的样本进行预测，并得到相应的预测结果 `y_predict`。预测结果可以用于评估模型在新样本上的表现或进行进一步的分析。

```py
from sklearn.linear_model import LinearRegression

lin_reg = LinearRegression()
lin_reg.fit(X, y)
lin_reg.intercept_, lin_reg.coef_

lin_reg.predict(X_new)
```

此代码使用了scikit-learn中的`LinearRegression`类来执行线性回归。

假设已经正确定义了输入数据`X`和目标变量`y`，你可以使用`LinearRegression`对象的`fit`方法来拟合线性回归模型，在拟合模型之后，可以通过`lin_reg`对象的`intercept_`和`coef_`属性来获取估计的截距项和系数，分别表示截距和每个特征的系数

```py
theta_best_svd, residuals, rank, s = np.linalg.lstsq(X_b, y, rcond=1e-6)
theta_best_svd
```

这段代码使用了NumPy中的`np.linalg.lstsq`函数来进行最小二乘线性回归。

根据提供的代码，`X_b`表示增广特征矩阵，`y`表示目标变量。

代码执行后，返回了四个值：`theta_best_svd`、`residuals`、`rank`和`s`。

- `theta_best_svd`是通过最小二乘法计算得到的最佳参数向量，即回归系数。
- `residuals`表示拟合残差的平方和，即回归模型的误差。
- `rank`表示增广特征矩阵的秩。
- `s`是增广特征矩阵`X_b`的奇异值。

所以，如果你想获取最佳参数向量，可以直接使用`theta_best_svd`变量。

```
np.linalg.pinv(X_b).dot(y)
```



## Gradient Descent

#### Batch Gradient Descent

**Lipschitz连续**

Lipschitz连续是一种用来描述函数的局部变化速率的性质。一个函数被称为Lipschitz连续，如果存在一个非负实数K，使得对于函数定义域内的任意两个点x和y，它们之间的函数值之差的绝对值不超过K乘以它们自身之间的距离，即：

|f(x) - f(y)| ≤ K * |x - y|

其中，K被称为Lipschitz常数。换句话说，Lipschitz连续函数的斜率（在定义域内的任意两点之间）被限制在一个有界的范围内。

Lipschitz连续性是一个重要的数学性质，它在优化问题、数值方法和机器学习中具有广泛的应用。对于Lipschitz连续函数，我们可以更准确地控制函数的变化速率，有助于分析函数的性质、优化算法的稳定性以及推导收敛性等方面。在机器学习中，Lipschitz连续性常常与梯度下降等优化算法的收敛性和稳定性相关联。

```
eta = 0.1  # learning rate
n_iterations = 1000
m = 100

theta = np.random.randn(2,1)  # random initialization

for iteration in range(n_iterations):
    gradients = 2/m * X_b.T.dot(X_b.dot(theta) - y)
    theta = theta - eta * gradients
    
theta
X_new_b.dot(theta)
```

这段代码使用随机梯度下降（SGD）算法来拟合线性回归模型。下面是代码的解释：

- `eta = 0.1` 是学习率，用于控制每次更新参数时的步长大小。

- `n_iterations = 1000` 是迭代次数，指定了要执行梯度下降的总步数。

- `m = 100` 是样本的数量。

- `theta = np.random.randn(2,1)` 是对参数θ进行随机初始化。θ是一个包含截距和系数的2x1的列向量。

接下来是梯度下降的迭代过程：

- 使用一个循环来迭代指定的次数 `n_iterations`。
- 在每次迭代中，计算梯度 `gradients`，即损失函数对于参数θ的偏导数。
- `X_b` 是增加了偏置项的输入特征矩阵。`X_b.T` 是 `X_b` 的转置。
- `X_b.dot(theta) - y` 是预测值与实际值之间的差异。
- `2/m` 是损失函数的常数因子。
- `X_b.T.dot(X_b.dot(theta) - y)` 是损失函数对于参数θ的梯度。
- `theta = theta - eta * gradients` 使用梯度下降更新参数θ。

通过迭代更新参数θ，代码逐渐优化模型的参数，以使损失函数最小化。最终，`theta` 将收敛到使损失最小的值，得到一个拟合了训练数据的线性回归模型。



#### Stochastic Gradient Descent

```py
theta_path_sgd = []
m = len(X_b)
np.random.seed(42)
```

这段代码初始化了一个空列表`theta_path_sgd`和变量`m`，并设置了随机种子为42。

`theta_path_sgd`是一个用于存储随机梯度下降算法（Stochastic Gradient Descent，SGD）的参数路径的列表。在每次迭代中，算法将更新参数，并将当前参数值添加到`theta_path_sgd`列表中。

`m`表示输入数据`X_b`的样本数量。

`np.random.seed(42)`设置了随机种子，保证了在运行代码时得到的随机数序列是固定的。这样做可以使实验结果可重现，确保在相同的初始条件下每次运行时获得相同的随机数序列。

```py
def learning_schedule(t):
    return t0 / (t + t1)

theta = np.random.randn(2,1)  # random initialization

for epoch in range(n_epochs):
    for i in range(m):
        if epoch == 0 and i < 20:                    # not shown in the book
            y_predict = X_new_b.dot(theta)           # not shown
            style = "b-" if i > 0 else "r--"         # not shown
            plt.plot(X_new, y_predict, style)        # not shown
        random_index = np.random.randint(m)
        xi = X_b[random_index:random_index+1]
        yi = y[random_index:random_index+1]
        gradients = 2 * xi.T.dot(xi.dot(theta) - yi)
        eta = learning_schedule(epoch * m + i)
        theta = theta - eta * gradients
        theta_path_sgd.append(theta)                 # not shown

plt.plot(X, y, "b.")                                 # not shown
plt.xlabel("$x_1$", fontsize=18)                     # not shown
plt.ylabel("$y$", rotation=0, fontsize=18)           # not shown
plt.axis([0, 2, 0, 15])                              # not shown
save_fig("sgd_plot")                                 # not shown
plt.show()                                           # not shown

theta
```

1. 这段代码实现了随机梯度下降（Stochastic Gradient Descent，SGD）算法来拟合线性回归模型。以下是代码的主要步骤：

   1. 定义了一个学习率调度函数`learning_schedule(t)`，该函数根据迭代次数`t`返回学习率。这个函数可能根据具体需求进行调整，但一般情况下随着迭代次数的增加，学习率会逐渐减小。

   1. 使用`np.random.randn(2,1)`对参数`theta`进行随机初始化，其中`theta`是一个2x1的数组。

   1. 通过多轮迭代来更新参数`theta`。外层循环控制迭代次数，内层循环遍历每个样本。在每次迭代中，随机选择一个样本，并计算其梯度。然后根据学习率和梯度更新参数`theta`。

   1. 在每个迭代的初期（第一个epoch）的前20个样本点上，绘制当前参数`theta`对应的模型预测结果。这部分代码是为了在图中可视化随着迭代的进行，参数`theta`逐渐优化的过程。

   1. 最后，绘制原始数据点以及最终拟合的线性回归模型的结果。

   请注意，代码中有一些注释标记为`# not shown`，这些部分是为了说明代码的功能，并不直接影响主要的算法逻辑。

   如果需要完整运行这段代码，可能需要导入相应的模块（如`matplotlib`等），并确保相关数据（如`X`和`y`）已经正确定义。

2. 在这段代码中，使用随机梯度下降（Stochastic Gradient Descent，SGD）算法进行模型的迭代更新。下面是迭代过程的详细解释：

   1. 外层循环通过`for epoch in range(n_epochs)`迭代指定的轮数（n_epochs），表示模型参数的更新将在多个轮次中进行。

   1. 内层循环通过`for i in range(m)`遍历每个样本，其中m是样本的总数。每个样本都会被随机选择，因为在每次迭代中，使用`np.random.randint(m)`生成一个随机索引`random_index`来选择样本。

   1. 初始时刻（第一个epoch）的前20个样本点将用于绘制模型的预测结果，这段代码的目的是为了在图中可视化随着迭代的进行，参数`theta`逐渐优化的过程。

   1. 在每次迭代中，通过选取随机样本，计算该样本的梯度。首先从增广特征矩阵`X_b`和目标变量`y`中获取随机样本的输入特征`xi`和目标值`yi`。

   1. 计算梯度的步骤是根据线性回归的误差函数（平方误差）的梯度公式，即`gradients = 2 * xi.T.dot(xi.dot(theta) - yi)`。这里使用了矩阵运算来计算梯度。

   1. 学习率`eta`通过调用`learning_schedule(epoch * m + i)`来获取，其中`epoch * m + i`表示当前迭代的总步数。学习率决定了每次参数更新的幅度。

   1. 使用学习率和梯度更新参数`theta`，即`theta = theta - eta * gradients`。这是随机梯度下降算法的核心更新步骤，通过沿着梯度的反方向对参数进行调整来最小化损失函数。

   1. 在每次迭代中，将当前参数`theta`添加到`theta_path_sgd`列表中，以便记录参数的路径。

   总结起来，这段代码通过多轮迭代和随机样本选择的方式，使用随机梯度下降算法来更新线性回归模型的参数`theta`。每次迭代中，根据随机样本计算梯度，并使用学习率来更新参数。通过这种方式，模型逐渐优化，最终得到最佳的参数估计。

```py
from sklearn.linear_model import SGDRegressor

sgd_reg = SGDRegressor(max_iter=1000, tol=1e-3, penalty=None, eta0=0.1, random_state=42)
sgd_reg.fit(X, y.ravel())
```

你提供的代码片段使用了scikit-learn库中的`SGDRegressor`类，使用随机梯度下降（SGD）优化算法拟合线性回归模型。

下面是代码的解释：

1. 导入必要的模块：`from sklearn.linear_model import SGDRegressor` 从scikit-learn的`linear_model`模块导入`SGDRegressor`类。

1. 初始化`SGDRegressor`对象：`sgd_reg = SGDRegressor(max_iter=1000, tol=1e-3, penalty=None, eta0=0.1, random_state=42)` 创建`SGDRegressor`的实例。它接受几个参数：

   - `max_iter` 指定SGD优化算法的最大迭代次数。
   - `tol` 是停止标准的容差值。如果损失的变化小于此值，算法将停止迭代。
   - `penalty` 确定要应用的正则化项，如果有的话。在这种情况下，`penalty=None` 表示不使用正则化。
   - `eta0` 是SGD算法的初始学习率。
   - `random_state` 是一个可选参数，用于设置随机种子，以便结果可重现性。

1. 拟合模型：`sgd_reg.fit(X, y.ravel())` 将`SGDRegressor`模型拟合到输入数据 `X` 和目标值 `y` 上。`X` 应该是一个包含特征的二维数组对象，`y` 应该是一个包含目标变量的一维数组对象。`ravel()` 方法用于确保 `y` 是一个一维数组。

执行这些代码后，`sgd_reg` 对象将在提供的数据上进行训练，模型将使用SGD优化算法学习线性回归问题的系数。

```
sgd_reg.intercept_, sgd_reg.coef_
```

`sgd_reg.intercept_`和`sgd_reg.coef_`是用于获取训练后的线性回归模型的截距和系数的属性。

- `sgd_reg.intercept_`表示线性回归模型的截距，即直线与y轴的交点。它是一个标量值。
- `sgd_reg.coef_`表示线性回归模型的系数，即每个特征对应的权重。对于多变量线性回归，它是一个一维数组，每个元素对应一个特征的系数。



#### Mini-batch gradient descent

```py
theta_path_mgd = []

n_iterations = 50
minibatch_size = 20

np.random.seed(42)
theta = np.random.randn(2,1)  # random initialization

t0, t1 = 200, 1000
def learning_schedule(t):
    return t0 / (t + t1)

t = 0
for epoch in range(n_iterations):
    shuffled_indices = np.random.permutation(m)
    X_b_shuffled = X_b[shuffled_indices]
    y_shuffled = y[shuffled_indices]
    for i in range(0, m, minibatch_size):
        t += 1
        xi = X_b_shuffled[i:i+minibatch_size]
        yi = y_shuffled[i:i+minibatch_size]
        gradients = 2/minibatch_size * xi.T.dot(xi.dot(theta) - yi)
        eta = learning_schedule(t)
        theta = theta - eta * gradients
        theta_path_mgd.append(theta)
        
        
theta
```

这段代码实现了小批量梯度下降（Mini-Batch Gradient Descent）算法来拟合线性回归模型。下面是代码的解释：

- `theta_path_mgd = []` 是一个空列表，用于存储每次迭代后的参数θ。

- `n_iterations = 50` 是迭代次数，指定了要执行梯度下降的总步数。

- `minibatch_size = 20` 是小批量的大小，即每次迭代中使用的样本数量。

- `np.random.seed(42)` 设置随机种子，以确保每次运行代码时生成的随机数相同。

- `theta = np.random.randn(2,1)` 对参数θ进行随机初始化。

- `t0, t1 = 200, 1000` 是学习率调度函数中的两个参数。

- `def learning_schedule(t):` 定义了学习率调度函数，根据迭代次数t返回相应的学习率。

- `t = 0` 初始化迭代次数。

- `for epoch in range(n_iterations):` 外层循环是迭代次数。
- `shuffled_indices = np.random.permutation(m)` 随机打乱样本的索引。
  
- `X_b_shuffled = X_b[shuffled_indices]` 根据打乱后的索引重新排列特征矩阵。
  
- `y_shuffled = y[shuffled_indices]` 根据打乱后的索引重新排列目标变量。
  
- `for i in range(0, m, minibatch_size):` 内层循环是小批量梯度下降的迭代。
  
  - `t += 1` 增加迭代次数。
  
  - `xi = X_b_shuffled[i:i+minibatch_size]` 获取当前小批量的特征矩阵。
  
  - `yi = y_shuffled[i:i+minibatch_size]` 获取当前小批量的目标变量。
  
  - `gradients = 2/minibatch_size * xi.T.dot(xi.dot(theta) - yi)` 计算当前小批量的梯度。
  
  - `eta = learning_schedule(t)` 根据学习率调度函数获取当前迭代的学习率。
  
  - `theta = theta - eta * gradients` 使用梯度下降更新参数θ。
  
  - `theta_path_mgd.append(theta)` 将当前参数θ添加到`theta_path_mgd`列表中。

这段代码通过小批量梯度下降算法，迭代更新参数θ来拟合线性回归模型。在每个迭代中，随机打乱样本顺序，并将样本分成多个小批量进行梯度计算和参数更新。通过这种方式，代码可以更高效地处理大规模数据集，并且相对于批量梯度下降和随机梯度下降，小批量梯度下降通常可以获得更好的收敛速度和模型性能。





## Polynomial Regression

```
import numpy as np
import numpy.random as rnd

np.random.seed(42)
```

```
m = 100
X = 6 * np.random.rand(m, 1) - 3
y = 0.5 * X**2 + X + 2 + np.random.randn(m, 1)
```

```
plt.plot(X, y, "b.")
plt.xlabel("$x_1$", fontsize=18)
plt.ylabel("$y$", rotation=0, fontsize=18)
plt.axis([-3, 3, 0, 10])
save_fig("quadratic_data_plot")
plt.show()
```

这段代码用于生成一个具有噪声的二次函数数据集。

下面是代码的解释：

- `m = 100` 定义了数据集的样本数量。

- `X = 6 * np.random.rand(m, 1) - 3` 生成一个包含m个样本的特征矩阵X，特征值范围在-3到3之间。

- `y = 0.5 * X**2 + X + 2 + np.random.randn(m, 1)` 根据特征矩阵X生成目标变量y。这里使用了二次函数关系，并添加了服从标准正态分布的随机噪声。

综合起来，这段代码生成了一个具有噪声的二次函数数据集，其中特征矩阵X是在-3到3范围内均匀分布的随机数，目标变量y根据二次函数关系生成，并添加了随机噪声。这样可以用来模拟实际问题中的非线性关系，并测试二次多项式回归等模型的拟合能力。

```
from sklearn.preprocessing import PolynomialFeatures
poly_features = PolynomialFeatures(degree=2, include_bias=False)
X_poly = poly_features.fit_transform(X)
X[0]
X_poly[0]
```

根据您提供的代码，`X` 是一个形状为 `(m, 1)` 的特征矩阵，其中 `m` 是样本数量。`X_poly` 是将 `X` 进行二次多项式转换后得到的特征矩阵。

下面是代码的解释：

- `from sklearn.preprocessing import PolynomialFeatures` 导入用于多项式特征转换的类 `PolynomialFeatures`。

- `poly_features = PolynomialFeatures(degree=2, include_bias=False)` 创建一个 `PolynomialFeatures` 类的实例，指定多项式的阶数为 2，并将偏差项 `include_bias` 设置为 `False`，以避免生成冗余的常数特征。

- `X_poly = poly_features.fit_transform(X)` 对特征矩阵 `X` 进行二次多项式转换，得到新的特征矩阵 `X_poly`。该转换将原始特征矩阵中的每个特征值扩展为包含原始特征及其交叉项的新特征。

- `X[0]` 获取特征矩阵 `X` 中的第一个样本的特征值。这将返回一个形状为 `(1,)` 的一维数组，包含第一个样本的特征值。

请注意，`X_poly` 是经过二次多项式转换后的特征矩阵，而 `X` 是原始的一维特征矩阵。因此，`X[0]` 只能获取第一个样本的原始特征值，而无法获取经过转换后的特征值。要获取经过转换后的特征矩阵的第一个样本，可以使用 `X_poly[0]`。

```
lin_reg = LinearRegression()
lin_reg.fit(X_poly, y)
lin_reg.intercept_, lin_reg.coef_
```

根据您提供的代码，`lin_reg` 是一个线性回归模型的实例，`X_poly` 是经过二次多项式转换后的特征矩阵，`y` 是目标变量。

下面是代码的解释：

- `lin_reg = LinearRegression()` 创建一个线性回归模型的实例 `lin_reg`。

- `lin_reg.fit(X_poly, y)` 使用经过二次多项式转换后的特征矩阵 `X_poly` 和目标变量 `y` 来训练线性回归模型。

- `lin_reg.intercept_` 获取线性回归模型的截距项，即模型预测中的常数项。

- `lin_reg.coef_` 获取线性回归模型的系数，即模型预测中特征的权重。

请注意，`lin_reg.intercept_` 是一个浮点数，表示线性回归模型的截距项。`lin_reg.coef_` 是一个数组，包含线性回归模型的系数，每个系数对应于特征矩阵中的一个特征。由于进行了二次多项式转换，所以 `lin_reg.coef_` 的长度将大于原始特征矩阵的特征数量。

```
X_new=np.linspace(-3, 3, 100).reshape(100, 1)
X_new_poly = poly_features.transform(X_new)
y_new = lin_reg.predict(X_new_poly)
plt.plot(X, y, "b.")
plt.plot(X_new, y_new, "r-", linewidth=2, label="Predictions")
plt.xlabel("$x_1$", fontsize=18)
plt.ylabel("$y$", rotation=0, fontsize=18)
plt.legend(loc="upper left", fontsize=14)
plt.axis([-3, 3, 0, 10])
save_fig("quadratic_predictions_plot")
plt.show()
```

这段代码用于绘制二次多项式回归模型在新输入数据上的预测结果。

下面是代码的解释：

- `X_new = np.linspace(-3, 3, 100).reshape(100, 1)` 创建一个包含100个等间距点的新输入特征矩阵 `X_new`，范围为-3到3。

- `X_new_poly = poly_features.transform(X_new)` 将新的输入特征矩阵进行二次多项式转换，得到经过转换后的特征矩阵 `X_new_poly`。

- `y_new = lin_reg.predict(X_new_poly)` 对经过转换后的特征矩阵 `X_new_poly` 进行预测，得到预测的目标变量值 `y_new`。

- `plt.plot(X, y, "b.")` 绘制训练数据的散点图，使用蓝色点表示。

- `plt.plot(X_new, y_new, "r-", linewidth=2, label="Predictions")` 绘制预测结果的曲线图，使用红色实线表示，并添加标签。

- `plt.xlabel("$x_1$", fontsize=18)` 设置x轴标签。

- `plt.ylabel("$y$", rotation=0, fontsize=18)` 设置y轴标签，并将其旋转为水平方向。

- `plt.legend(loc="upper left", fontsize=14)` 添加图例，位于左上角，标签为 "Predictions"。

- `plt.axis([-3, 3, 0, 10])` 设置坐标轴的范围。

- `save_fig("quadratic_predictions_plot")` 保存图形为文件，文件名为 "quadratic_predictions_plot"。

- `plt.show()` 显示图形。

这段代码的目的是绘制二次多项式回归模型在新输入数据上的预测结果。通过将新的输入特征矩阵进行二次多项式转换，并使用训练好的线性回归模型进行预测，可以得到模型在新数据上的预测值。然后，通过绘制训练数据的散点图和预测结果的曲线图，可以可视化模型的拟合效果。图中训练数据用蓝色点表示，预测结果用红色实线表示，并添加了图例和坐标轴标签。最后，图形被保存为文件并显示出来。

```
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split

def plot_learning_curves(model, X, y):
    X_train, X_val, y_train, y_val = train_test_split(X, y, test_size=0.2, random_state=10)
    train_errors, val_errors = [], []
    for m in range(1, len(X_train) + 1):
        model.fit(X_train[:m], y_train[:m])
        y_train_predict = model.predict(X_train[:m])
        y_val_predict = model.predict(X_val)
        train_errors.append(mean_squared_error(y_train[:m], y_train_predict))
        val_errors.append(mean_squared_error(y_val, y_val_predict))

    plt.plot(np.sqrt(train_errors), "r-+", linewidth=2, label="train")
    plt.plot(np.sqrt(val_errors), "b-", linewidth=3, label="val")
    plt.legend(loc="upper right", fontsize=14)   # not shown in the book
    plt.xlabel("Training set size", fontsize=14) # not shown
    plt.ylabel("RMSE", fontsize=14)              # not shown
```

这段代码定义了一个函数 `plot_learning_curves`，用于绘制学习曲线，以评估模型在不同训练集大小下的性能。

下面是代码的解释：

- `X_train, X_val, y_train, y_val = train_test_split(X, y, test_size=0.2, random_state=10)` 使用 `train_test_split` 函数将数据集 `X` 和目标变量 `y` 划分为训练集（`X_train` 和 `y_train`）和验证集（`X_val` 和 `y_val`），其中验证集大小为总样本的 20%。

- `train_errors, val_errors = [], []` 创建空列表 `train_errors` 和 `val_errors`，用于存储训练集和验证集的均方根误差（RMSE）。

- `for m in range(1, len(X_train) + 1):` 遍历训练集的大小，从 1 到训练集的总样本数。

  - `model.fit(X_train[:m], y_train[:m])` 使用部分训练集（从头开始到当前大小 `m`）来训练模型。

  - `y_train_predict = model.predict(X_train[:m])` 对部分训练集进行预测，得到预测的目标变量值 `y_train_predict`。

  - `y_val_predict = model.predict(X_val)` 对验证集进行预测，得到预测的目标变量值 `y_val_predict`。

  - `train_errors.append(mean_squared_error(y_train[:m], y_train_predict))` 计算并存储训练集的均方根误差。

  - `val_errors.append(mean_squared_error(y_val, y_val_predict))` 计算并存储验证集的均方根误差。

- `plt.plot(np.sqrt(train_errors), "r-+", linewidth=2, label="train")` 绘制训练集的均方根误差曲线，使用红色加号表示。

- `plt.plot(np.sqrt(val_errors), "b-", linewidth=3, label="val")` 绘制验证集的均方根误差曲线，使用蓝色实线表示。

- `plt.legend(loc="upper right", fontsize=14)` 添加图例，位于右上角，标签为 "train" 和 "val"。

- `plt.xlabel("Training set size", fontsize=14)` 设置x轴标签。

- `plt.ylabel("RMSE", fontsize=14)` 设置y轴标签。

这个函数的目的是绘制学习曲线，用于观察模型在不同训练集大小下的性能表现。通过逐步增加训练集的大小，计算并绘制训练集和验证集的均方根误差曲线，可以了解模型在不同数据规模下的拟合情况和泛化能力。图中训练集的均方根误差用红色加号表示，验证集的均方根误差用蓝色实线表示，并添加了图例和坐标轴标签。

```
lin_reg = LinearRegression()
plot_learning_curves(lin_reg, X, y)
plt.axis([0, 80, 0, 3])                         # not shown in the book
save_fig("underfitting_learning_curves_plot")   # not shown
plt.show()  
```

这段代码使用线性回归模型 `lin_reg` 调用了之前定义的 `plot_learning_curves` 函数，绘制了线性回归模型的学习曲线。

下面是代码的解释：

- `lin_reg = LinearRegression()` 创建一个线性回归模型的实例。

- `plot_learning_curves(lin_reg, X, y)` 调用 `plot_learning_curves` 函数，传入线性回归模型 `lin_reg`、特征矩阵 `X` 和目标变量 `y`，绘制学习曲线。

- `plt.axis([0, 80, 0, 3])` 设置坐标轴的范围，x轴范围为0到80，y轴范围为0到3。

- `save_fig("underfitting_learning_curves_plot")` 将图形保存为文件，文件名为 "underfitting_learning_curves_plot"。

- `plt.show()` 显示图形。

这段代码的目的是绘制线性回归模型的学习曲线，并观察模型在不同训练集大小下的表现。通过限制坐标轴的范围，可以聚焦于训练集大小较小的区域，以更清晰地观察模型的欠拟合情况。最后，图形被保存为文件，并显示出来。

```
from sklearn.pipeline import Pipeline

polynomial_regression = Pipeline([
        ("poly_features", PolynomialFeatures(degree=10, include_bias=False)),
        ("lin_reg", LinearRegression()),
    ])

plot_learning_curves(polynomial_regression, X, y)
plt.axis([0, 80, 0, 3])           # not shown
save_fig("learning_curves_plot")  # not shown
plt.show()
```

这段代码创建了一个多项式回归模型 `polynomial_regression`，并使用该模型调用了 `plot_learning_curves` 函数，绘制了多项式回归模型的学习曲线。

下面是代码的解释：

- `polynomial_regression = Pipeline([...])` 创建一个管道（`Pipeline`），将多项式特征转换和线性回归模型连接在一起，形成多项式回归模型。

- `("poly_features", PolynomialFeatures(degree=10, include_bias=False))` 在管道中添加多项式特征转换步骤，使用阶数为10的多项式特征转换器。

- `("lin_reg", LinearRegression())` 在管道中添加线性回归模型步骤。

- `plot_learning_curves(polynomial_regression, X, y)` 调用 `plot_learning_curves` 函数，传入多项式回归模型 `polynomial_regression`、特征矩阵 `X` 和目标变量 `y`，绘制多项式回归模型的学习曲线。

- `plt.axis([0, 80, 0, 3])` 设置坐标轴的范围，x轴范围为0到80，y轴范围为0到3。

- `save_fig("learning_curves_plot")` 将图形保存为文件，文件名为 "learning_curves_plot"。

- `plt.show()` 显示图形。

这段代码的目的是创建并使用多项式回归模型，观察其在不同训练集大小下的学习曲线。通过限制坐标轴的范围，可以聚焦于训练集大小较小的区域，以更清晰地观察模型的拟合情况和泛化能力。最后，图形被保存为文件，并显示出来。



## Regularized Linear Models

#### Ridge Regression

```
np.random.seed(42)
m = 20
X = 3 * np.random.rand(m, 1)
y = 1 + 0.5 * X + np.random.randn(m, 1) / 1.5
X_new = np.linspace(0, 3, 100).reshape(100, 1)
```

这段代码生成了一组随机的特征矩阵 `X` 和目标变量 `y`，以及一个新的特征矩阵 `X_new`。

下面是代码的解释：

- `np.random.seed(42)` 设置随机种子为42，以确保生成的随机数可复现。

- `m = 20` 设置样本数量为20。

- `X = 3 * np.random.rand(m, 1)` 生成一个形状为 `(m, 1)` 的随机特征矩阵 `X`，其中的元素取值范围在0到3之间。

- `y = 1 + 0.5 * X + np.random.randn(m, 1) / 1.5` 根据特征矩阵 `X` 生成目标变量 `y`。目标变量的计算方式为 `1 + 0.5 * X + 噪声`，其中噪声服从均值为0，标准差为1.5的正态分布。

- `X_new = np.linspace(0, 3, 100).reshape(100, 1)` 生成一个形状为 `(100, 1)` 的新特征矩阵 `X_new`，其中的元素在0到3之间均匀分布。这个特征矩阵用于在0到3之间生成100个等间隔的值，用于绘制模型的预测结果。

这段代码的目的是生成一组随机的数据集，用于后续的模型训练和预测。特征矩阵 `X` 和目标变量 `y` 是基于一定的模式和噪声生成的，用于模拟实际数据集。新的特征矩阵 `X_new` 则用于在指定范围内生成一系列用于预测的新样本点。



```
from sklearn.linear_model import Ridge
ridge_reg = Ridge(alpha=1, solver="cholesky", random_state=42)
ridge_reg.fit(X, y)
ridge_reg.predict([[1.5]])
```

这段代码使用岭回归模型 `Ridge` 对特征矩阵 `X` 和目标变量 `y` 进行训练，并对给定的特征值进行预测。

下面是代码的解释：

- `from sklearn.linear_model import Ridge` 导入岭回归模型 `Ridge`。

- `ridge_reg = Ridge(alpha=1, solver="cholesky", random_state=42)` 创建一个岭回归模型的实例 `ridge_reg`，其中的参数设置如下：

  - `alpha=1`：正则化参数，控制正则化的强度。较大的 `alpha` 值表示更强的正则化。
  - `solver="cholesky"`：求解岭回归的方法，使用 `cholesky` 分解方法。
  - `random_state=42`：随机种子，用于控制模型的随机性。

- `ridge_reg.fit(X, y)` 使用岭回归模型对特征矩阵 `X` 和目标变量 `y` 进行训练，拟合回归模型。

- `ridge_reg.predict([[1.5]])` 对给定的特征值 `[[1.5]]` 进行预测，返回预测的目标变量值。

这段代码的目的是使用岭回归模型对数据进行拟合和预测。岭回归是一种带有正则化的线性回归方法，通过控制正则化参数 `alpha` 的值，可以调节模型的复杂度和拟合能力。在该代码中，使用训练好的岭回归模型对特征值 `1.5` 进行预测，并返回预测的目标变量值。



```
ridge_reg = Ridge(alpha=1, solver="sag", random_state=42)
ridge_reg.fit(X, y)
ridge_reg.predict([[1.5]])
```

求解岭回归的方法，使用随机平均梯度下降（Stochastic Average Gradient）方法



```
from sklearn.linear_model import Ridge

def plot_model(model_class, polynomial, alphas, **model_kargs):
    for alpha, style in zip(alphas, ("b-", "g--", "r:")):
        model = model_class(alpha, **model_kargs) if alpha > 0 else LinearRegression()
        if polynomial:
            model = Pipeline([
                    ("poly_features", PolynomialFeatures(degree=10, include_bias=False)),
                    ("std_scaler", StandardScaler()),
                    ("regul_reg", model),
                ])
        model.fit(X, y)
        y_new_regul = model.predict(X_new)
        lw = 2 if alpha > 0 else 1
        plt.plot(X_new, y_new_regul, style, linewidth=lw, label=r"$\alpha = {}$".format(alpha))
    plt.plot(X, y, "b.", linewidth=3)
    plt.legend(loc="upper left", fontsize=15)
    plt.xlabel("$x_1$", fontsize=18)
    plt.axis([0, 3, 0, 4])
```

**解析**

```python
from sklearn.linear_model import Ridge
```

这行代码从 `sklearn`（Scikit-Learn）库的 `linear_model` 模块中导入了 `Ridge` 类。`Ridge` 类表示带有L2正则化的线性回归模型。

```python
def plot_model(model_class, polynomial, alphas, **model_kargs):
```

这行代码定义了名为 `plot_model` 的函数，它接受几个参数：`model_class`（要使用的模型类，如 `Ridge`）、`polynomial`（一个布尔值，指示是否应使用多项式特征）、`alphas`（正则化强度的列表）和 `**model_kargs`（模型类的其他关键字参数）。

```python
for alpha, style in zip(alphas, ("b-", "g--", "r:")):
```

这行代码遍历 `alphas` 列表，并将每个值赋给变量 `alpha`。它还使用 `zip` 函数将不同的线条样式（"b-", "g--", "r:"）赋给变量 `style`。

```python
model = model_class(alpha, **model_kargs) if alpha > 0 else LinearRegression()
```

这行代码创建了 `model_class`（例如 `Ridge`）的一个实例，使用给定的 `alpha` 值和其他关键字参数（`**model_kargs`）。如果 `alpha` 大于 0，则创建一个带有正则化的模型（`model_class`）；否则，使用无正则化的线性回归模型（`LinearRegression`）。

```python
if polynomial:
    model = Pipeline([
        ("poly_features", PolynomialFeatures(degree=10, include_bias=False)),
        ("std_scaler", StandardScaler()),
        ("regul_reg", model),
    ])
```

如果 `polynomial` 为 `True`，这段代码将创建一个流水线（`Pipeline`），其中包含多项式特征、标准化和所选模型。这允许进行带有正则化的多项式回归。

```python
model.fit(X, y)
```

这行代码将模型拟合到训练数据 `X` 和目标值 `y` 上。

```python
y_new_regul = model.predict(X_new)
```

这行代码使用拟合好的模型对新的数据 `X_new` 进行预测，并将预测值赋给 `y_new_regul`。

```python
lw = 2 if alpha > 0 else 1
plt.plot(X_new, y_new_regul, style, linewidth=lw, label=r"$\alpha = {}$".format(alpha))
```

这行代码使用指定的线条样式 `style` 将预测值 `y_new_regul` 相对于新数据 `X_new` 进行绘图。如果 `alpha` 大于 0（表示正则化），则线条宽度 (`linewidth`) 设置为 2；否则设为 1。线条的标签也被设置为显示 `alpha` 的值。

```python
plt.plot(X, y, "b.", linewidth=3)
```

这行代码以蓝色点（"b."）绘制原始数据点 (`X` 和 `y`)。

```python
plt.legend(loc="upper left", fontsize=15)
plt.xlabel("$x_1$", fontsize=18)
plt.axis([0, 3, 0, 4])
```

这些代码添加了图例、设置了 x 轴标签，并调整了图表的坐标轴范围。



```
plt.figure(figsize=(8,4))
plt.subplot(121)
plot_model(Ridge, polynomial=False, alphas=(0, 10, 100), random_state=42)
plt.ylabel("$y$", rotation=0, fontsize=18)
plt.subplot(122)
plot_model(Ridge, polynomial=True, alphas=(0, 10**-5, 1), random_state=42)

save_fig("ridge_regression_plot")
plt.show()
```

这段代码创建了一个图形窗口，包含两个子图，并调用了 `plot_model` 函数来绘制两个子图中的模型预测结果。最后，调用 `save_fig` 函数保存图形，并使用 `plt.show()` 函数显示图形。

请注意，`save_fig` 函数在您提供的代码中并未定义，因此您需要将其定义或使用适当的保存图形的方法。

以下是代码的解释：

```python
plt.figure(figsize=(8, 4))
```

这行代码创建一个图形窗口，设置宽度为8英寸，高度为4英寸。

```python
plt.subplot(121)
plot_model(Ridge, polynomial=False, alphas=(0, 10, 100), random_state=42)
plt.ylabel("$y$", rotation=0, fontsize=18)
```

这段代码创建了第一个子图，位于图形窗口的左侧位置（1行2列中的第1个位置）。然后，调用 `plot_model` 函数，并传递了相应的参数，绘制了带有不同正则化强度的线性回归模型的预测结果。接下来，设置了y轴标签为"$y$"，并进行了适当的旋转和字体大小设置。

```python
plt.subplot(122)
plot_model(Ridge, polynomial=True, alphas=(0, 10**-5, 1), random_state=42)
```

这段代码创建了第二个子图，位于图形窗口的右侧位置（1行2列中的第2个位置）。然后，再次调用 `plot_model` 函数，并传递了相应的参数，绘制了带有不同正则化强度的多项式回归模型的预测结果。

```python
save_fig("ridge_regression_plot")
```

这行代码调用了一个名为 `save_fig` 的函数，用于保存图形。请确保在代码中定义了该函数或使用适当的保存图形的方法。

```python
plt.show()
```

这行代码显示图形窗口，展示绘制的图形。

总的来说，这段代码创建了一个包含两个子图的图形窗口，分别展示了线性回归模型和多项式回归模型在不同正则化强度下的预测结果。



**Note**: to be future-proof, we set `max_iter=1000` and `tol=1e-3` because these will be the default values in Scikit-Learn 0.21.

```
sgd_reg = SGDRegressor(penalty="l2", max_iter=1000, tol=1e-3, random_state=42)
sgd_reg.fit(X, y.ravel())
sgd_reg.predict([[1.5]])
```



#### Lasso Regression

```
from sklearn.linear_model import Lasso

plt.figure(figsize=(8,4))
plt.subplot(121)
plot_model(Lasso, polynomial=False, alphas=(0, 0.1, 1), random_state=42)
plt.ylabel("$y$", rotation=0, fontsize=18)
plt.subplot(122)
plot_model(Lasso, polynomial=True, alphas=(0, 10**-7, 1), random_state=42)

save_fig("lasso_regression_plot")
plt.show()
```

```
from sklearn.linear_model import Lasso
lasso_reg = Lasso(alpha=0.1)
lasso_reg.fit(X, y)
lasso_reg.predict([[1.5]])
```



#### Elastic Net

```
from sklearn.linear_model import ElasticNet
elastic_net = ElasticNet(alpha=0.1, l1_ratio=0.5, random_state=42)
elastic_net.fit(X, y)
elastic_net.predict([[1.5]])
```

这段代码使用 `sklearn` 库中的 `ElasticNet` 类创建了一个弹性网络模型，并对数据进行拟合和预测。

以下是代码的解释：

```python
from sklearn.linear_model import ElasticNet
```

这行代码从 `sklearn` 库的 `linear_model` 模块中导入了 `ElasticNet` 类。`ElasticNet` 是一种线性回归模型，它结合了 L1 和 L2 正则化，可以用于特征选择和稀疏性。

```python
elastic_net = ElasticNet(alpha=0.1, l1_ratio=0.5, random_state=42)
```

这行代码创建了一个 `ElasticNet` 类的实例 `elastic_net`。通过指定参数 `alpha`（正则化强度）、`l1_ratio`（L1 正则化和总正则化之间的比例）和 `random_state`（随机种子），定义了弹性网络模型的属性。

```python
elastic_net.fit(X, y)
```

这行代码将弹性网络模型拟合到训练数据 `X` 和目标值 `y` 上，用于学习模型的参数。

```python
elastic_net.predict([[1.5]])
```

这行代码使用拟合好的弹性网络模型对给定的输入数据 `[[1.5]]` 进行预测，并返回预测结果。

总的来说，这段代码创建了一个弹性网络模型，并对给定的输入数据进行预测。预测结果将作为输出返回。



#### Early Stopping

```
np.random.seed(42)
m = 100
X = 6 * np.random.rand(m, 1) - 3
y = 2 + X + 0.5 * X**2 + np.random.randn(m, 1)

X_train, X_val, y_train, y_val = train_test_split(X[:50], y[:50].ravel(), test_size=0.5, random_state=10)
```

这段代码使用 NumPy 库生成了一些随机数据，并将其划分为训练集和验证集。

以下是代码的解释：

```python
np.random.seed(42)
```

这行代码设置随机种子为 42。这样做可以确保每次运行代码时生成的随机数是相同的，以保持结果的可重复性。

```python
m = 100
X = 6 * np.random.rand(m, 1) - 3
y = 2 + X + 0.5 * X**2 + np.random.randn(m, 1)
```

这段代码生成了一组包含 100 个样本的随机数据。`X` 是一个包含 `m` 行、1 列的数组，每个元素都是在 -3 到 3 之间的随机数。`y` 是通过给定的公式计算得到的目标值，其中包括了一些随机噪声。

```python
X_train, X_val, y_train, y_val = train_test_split(X[:50], y[:50].ravel(), test_size=0.5, random_state=10)
```

这行代码使用 `train_test_split` 函数将数据集划分为训练集和验证集。`X[:50]` 和 `y[:50]` 表示从原始数据中取前 50 个样本用于划分。`test_size=0.5` 表示将数据集划分成训练集和验证集的比例为 1:1。`random_state=10` 设置了随机种子，以确保每次运行代码时划分结果相同。

划分后的结果为：

- `X_train`：训练集特征数据，包含前 50 个样本
- `X_val`：验证集特征数据，包含前 50 个样本
- `y_train`：训练集目标值，对应训练集特征数据
- `y_val`：验证集目标值，对应验证集特征数据

通过这样的划分，可以在训练集上训练模型，并使用验证集评估模型的性能。



```
from copy import deepcopy

poly_scaler = Pipeline([
        ("poly_features", PolynomialFeatures(degree=90, include_bias=False)),
        ("std_scaler", StandardScaler())
    ])

X_train_poly_scaled = poly_scaler.fit_transform(X_train)
X_val_poly_scaled = poly_scaler.transform(X_val)

sgd_reg = SGDRegressor(max_iter=1, tol=-np.infty, warm_start=True,
                       penalty=None, learning_rate="constant", eta0=0.0005, random_state=42)
```

这段代码使用 scikit-learn 库中的一些功能来进行特征转换和模型拟合。

以下是代码的解释：

```python
from copy import deepcopy
```

这行代码导入了 `deepcopy` 函数，用于创建对象的深拷贝。

```python
poly_scaler = Pipeline([
    ("poly_features", PolynomialFeatures(degree=90, include_bias=False)),
    ("std_scaler", StandardScaler())
])
```

这段代码创建了一个管道（Pipeline）对象 `poly_scaler`，该管道包含两个步骤：`poly_features` 和 `std_scaler`。`poly_features` 步骤使用 `PolynomialFeatures` 类将特征进行多项式转换，设置了多项式的阶数为 90，并将偏差（bias）项设置为 False。`std_scaler` 步骤使用 `StandardScaler` 类对特征进行标准化处理。

```python
X_train_poly_scaled = poly_scaler.fit_transform(X_train)
X_val_poly_scaled = poly_scaler.transform(X_val)
```

这两行代码分别对训练集和验证集的特征数据进行多项式转换和标准化处理。`fit_transform` 方法用于对训练集进行拟合和转换操作，而 `transform` 方法只进行转换操作。这样可以确保训练集和验证集使用相同的转换方式。

```python
sgd_reg = SGDRegressor(max_iter=1, tol=-np.infty, warm_start=True,
                       penalty=None, learning_rate="constant", eta0=0.0005, random_state=42)
```

这段代码创建了一个 `SGDRegressor` 类的实例 `sgd_reg`，该模型使用随机梯度下降（SGD）算法进行回归。它的参数设置如下：

- `max_iter=1`：每次迭代的最大次数，这里设置为 1，表示每次只迭代一次。
- `tol=-np.infty`：迭代停止的阈值，这里设置为负无穷，表示不会停止迭代。
- `warm_start=True`：如果为 True，则在调用 `fit` 方法时保留之前的模型状态，以便可以继续训练。
- `penalty=None`：惩罚项，这里设置为 None，表示没有惩罚项。
- `learning_rate="constant"`：学习率的类型，这里设置为常数学习率。
- `eta0=0.0005`：初始学习率。
- `random_state=42`：随机种子，以确保每次运行代码时得到相同的结果。

通过以上的设置，可以创建一个使用 SGD 算法的回归模型。接下来，您可以使用该模型拟合训练集，并进行预测和评估。



```
minimum_val_error = float("inf")
best_epoch = None
best_model = None
for epoch in range(1000):
    sgd_reg.fit(X_train_poly_scaled, y_train)  # continues where it left off
    y_val_predict = sgd_reg.predict(X_val_poly_scaled)
    val_error = mean_squared_error(y_val, y_val_predict)
    if val_error < minimum_val_error:
        minimum_val_error = val_error
        best_epoch = epoch
        best_model = deepcopy(sgd_reg)
```

这段代码使用随机梯度下降（SGD）回归模型进行训练，并记录在验证集上的最小均方误差（mean squared error），同时保存具有最小验证误差的模型。

以下是代码的解释：

```python
minimum_val_error = float("inf")
best_epoch = None
best_model = None
```

这几行代码初始化了用于记录最小验证误差和对应模型的变量。`minimum_val_error` 被初始化为正无穷，以便在循环中找到更小的验证误差。`best_epoch` 和 `best_model` 被初始化为 `None`。

```python
for epoch in range(1000):
    sgd_reg.fit(X_train_poly_scaled, y_train)  # continues where it left off
    y_val_predict = sgd_reg.predict(X_val_poly_scaled)
    val_error = mean_squared_error(y_val, y_val_predict)
    if val_error < minimum_val_error:
        minimum_val_error = val_error
        best_epoch = epoch
        best_model = deepcopy(sgd_reg)
```

这段代码开始一个循环，在每个迭代周期中，使用拟合了多项式转换和标准化后的训练数据 `X_train_poly_scaled` 和目标值 `y_train` 来训练 SGD 回归模型。`fit` 方法将从上一次停止的地方继续训练。

然后，使用训练好的模型对验证集进行预测，得到预测结果 `y_val_predict`。

接下来，计算预测结果与验证集目标值 `y_val` 之间的均方误差，并将其存储在 `val_error` 变量中。

如果当前的验证误差 `val_error` 小于之前记录的最小验证误差 `minimum_val_error`，则更新 `minimum_val_error` 为当前的 `val_error`，并将 `best_epoch` 更新为当前迭代周期 `epoch` 的值。同时，使用 `deepcopy` 函数创建 `sgd_reg` 的深拷贝，并将其保存在 `best_model` 中。

通过这样的循环，可以找到在验证集上具有最小验证误差的模型，并将其保存下来。





## Logistic Regression

#### Decision Boundaries

```
X = iris["data"][:, 3:]  # petal width
y = (iris["target"] == 2).astype(np.int)  # 1 if Iris virginica, else 0
```

这段代码使用了鸢尾花数据集（iris dataset）加载特征数据和目标变量。

```python
X = iris["data"][:, 3:]  # petal width
```

这行代码从鸢尾花数据集中选择了特征数据。`iris["data"]` 返回整个数据集的特征矩阵，`[:, 3:]` 选择了所有行的第三列及之后的列，即选择了花瓣宽度（petal width）作为特征。

```python
y = (iris["target"] == 2).astype(np.int)  # 1 if Iris virginica, else 0
```

这行代码创建了目标变量（标签）。`iris["target"]` 返回数据集的目标向量，其中每个元素表示对应样本的类别。通过比较 `iris["target"]` 是否等于 2，得到一个布尔值向量，其中 `True` 表示样本属于 Iris virginica 类别，`False` 表示不属于。然后，使用 `astype(np.int)` 将布尔值向量转换为整数类型，将 `True` 转换为 1，将 `False` 转换为 0。

综合起来，这段代码将鸢尾花数据集的花瓣宽度作为特征（X），并将样本的类别转换为二元标签，其中 1 表示 Iris virginica 类别，0 表示其他类别。



```
from sklearn.linear_model import LogisticRegression
log_reg = LogisticRegression(solver="lbfgs", random_state=42)
log_reg.fit(X, y)
```

```
decision_boundary
```

```
log_reg.predict([[1.7], [1.5]])
```



#### Softmax Regression

```
from sklearn.linear_model import LogisticRegression

X = iris["data"][:, (2, 3)]  # petal length, petal width
y = (iris["target"] == 2).astype(np.int)

log_reg = LogisticRegression(solver="lbfgs", C=10**10, random_state=42)
log_reg.fit(X, y)

x0, x1 = np.meshgrid(
        np.linspace(2.9, 7, 500).reshape(-1, 1),
        np.linspace(0.8, 2.7, 200).reshape(-1, 1),
    )
X_new = np.c_[x0.ravel(), x1.ravel()]

y_proba = log_reg.predict_proba(X_new)
```

这段代码使用了 `LogisticRegression` 类从鸢尾花数据集中训练了一个逻辑回归模型，并使用该模型对新的数据进行预测。

以下是代码的解释：

```python
X = iris["data"][:, (2, 3)]  # petal length, petal width
y = (iris["target"] == 2).astype(np.int)
```

这两行代码选择了鸢尾花数据集中的两个特征，即花瓣长度（petal length）和花瓣宽度（petal width）。`X` 是特征矩阵，包含了所有样本的这两个特征。`y` 是目标变量，使用了与之前相同的逻辑，将 Iris virginica 类别设为 1，其他类别设为 0。

```python
log_reg = LogisticRegression(solver="lbfgs", C=10**10, random_state=42)
log_reg.fit(X, y)
```

这几行代码创建了一个逻辑回归模型，并使用 `fit` 方法对模型进行训练。`solver="lbfgs"` 指定了求解优化问题的算法为 L-BFGS（Limited-memory Broyden-Fletcher-Goldfarb-Shanno），`C=10**10` 设置了逆正则化强度，`random_state=42` 设置了随机种子，以确保结果的可复现性。

```python
x0, x1 = np.meshgrid(
        np.linspace(2.9, 7, 500).reshape(-1, 1),
        np.linspace(0.8, 2.7, 200).reshape(-1, 1),
    )
X_new = np.c_[x0.ravel(), x1.ravel()]
```

这几行代码用于生成一个新的特征矩阵 `X_new`，用于可视化分类边界。`np.meshgrid` 函数根据指定的范围和步长生成网格点坐标矩阵。`np.linspace` 函数生成一维均匀间隔的数组，`reshape(-1, 1)` 将一维数组转换为列向量，然后使用 `np.meshgrid` 生成二维坐标矩阵。`x0` 和 `x1` 分别表示生成的两个坐标矩阵。

```python
y_proba = log_reg.predict_proba(X_new)
```

这行代码使用训练好的逻辑回归模型对新的数据集 `X_new` 进行预测，并返回预测样本属于各个类别的概率。`predict_proba` 方法返回一个数组，每一行表示一个样本，每一列表示样本属于对应类别的概率。



```py
X = iris["data"][:, (2, 3)]  # petal length, petal width
y = iris["target"]

softmax_reg = LogisticRegression(multi_class="multinomial",solver="lbfgs", C=10, random_state=42)
softmax_reg.fit(X, y)
```

这段代码使用了 `LogisticRegression` 类从鸢尾花数据集中训练了一个多类别的逻辑回归模型（Softmax 回归），并使用该模型对新的数据进行预测。

以下是代码的解释：

```python
X = iris["data"][:, (2, 3)]  # petal length, petal width
y = iris["target"]
```

这两行代码选择了鸢尾花数据集中的两个特征，即花瓣长度（petal length）和花瓣宽度（petal width）。`X` 是特征矩阵，包含了所有样本的这两个特征。`y` 是目标变量，表示鸢尾花的类别。

```python
softmax_reg = LogisticRegression(multi_class="multinomial",solver="lbfgs", C=10, random_state=42)
softmax_reg.fit(X, y)
```

这几行代码创建了一个多类别的逻辑回归模型（Softmax 回归），并使用 `fit` 方法对模型进行训练。`multi_class="multinomial"` 指定了多类别分类的类型为 multinomial，`solver="lbfgs"` 指定了求解优化问题的算法为 L-BFGS（Limited-memory Broyden-Fletcher-Goldfarb-Shanno），`C=10` 设置了逆正则化强度，`random_state=42` 设置了随机种子，以确保结果的可复现性。通过调用 `fit` 方法，模型使用特征矩阵 `X` 和目标变量 `y` 进行训练。

训练完成后，`softmax_reg` 变量就是训练好的 Softmax 回归模型，可以用于对新的数据进行预测。



```
softmax_reg.predict([[5, 2]])
```

`softmax_reg.predict([[5, 2]])` 这行代码使用训练好的 Softmax 回归模型 `softmax_reg` 对新的数据进行预测。

`[[5, 2]]` 表示一个新的样本，它的花瓣长度为 5，花瓣宽度为 2。

`predict` 方法接收一个特征矩阵作为输入，并返回预测的类别结果。在这个例子中，它会预测给定样本的类别。

你可以运行这行代码来获取预测结果。请注意，预测结果将是鸢尾花的类别之一，取决于模型的训练结果和输入样本的特征值。



```
softmax_reg.predict_proba([[5, 2]])
```

`softmax_reg.predict_proba([[5, 2]])` 这行代码使用训练好的 Softmax 回归模型 `softmax_reg` 对新的数据进行概率预测。

`[[5, 2]]` 表示一个新的样本，它的花瓣长度为 5，花瓣宽度为 2。

`predict_proba` 方法接收一个特征矩阵作为输入，并返回每个类别的概率预测结果。在这个例子中，它会返回给定样本属于每个类别的概率值。

你可以运行这行代码来获取概率预测结果。结果将是一个二维数组，其中每一行表示一个样本，每一列表示一个类别，并且每个元素表示对应类别的概率值。



