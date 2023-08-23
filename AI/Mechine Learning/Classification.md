# **Chapter 3 – Classification**

## Setup

First, let's import a few common modules, ensure MatplotLib plots figures inline and prepare a function to save the figures. We also check that Python 3.5 or later is installed (although Python 2.x may work, it is deprecated so we strongly recommend you use Python 3 instead), as well as Scikit-Learn ≥0.20.

```py
# Python ≥3.5 is required
import sys
assert sys.version_info >= (3, 5)

# Is this notebook running on Colab or Kaggle?
IS_COLAB = "google.colab" in sys.modules
IS_KAGGLE = "kaggle_secrets" in sys.modules

# Scikit-Learn ≥0.20 is required
import sklearn
assert sklearn.__version__ >= "0.20"

# Common imports
import numpy as np
import os

# to make this notebook's output stable across runs
np.random.seed(42)

# To plot pretty figures
%matplotlib inline
import matplotlib as mpl
import matplotlib.pyplot as plt
mpl.rc('axes', labelsize=14)
mpl.rc('xtick', labelsize=12)
mpl.rc('ytick', labelsize=12)

# Where to save the figures
PROJECT_ROOT_DIR = "."
CHAPTER_ID = "classification"
IMAGES_PATH = os.path.join(PROJECT_ROOT_DIR, "images", CHAPTER_ID)
os.makedirs(IMAGES_PATH, exist_ok=True)

def save_fig(fig_id, tight_layout=True, fig_extension="png", resolution=300):
    path = os.path.join(IMAGES_PATH, fig_id + "." + fig_extension)
    print("Saving figure", fig_id)
    if tight_layout:
        plt.tight_layout()
    plt.savefig(path, format=fig_extension, dpi=resolution)
```

## MNIST

**Warning:** since Scikit-Learn 0.24, `fetch_openml()` returns a Pandas `DataFrame` by default. To avoid this and keep the same code as in the book, we use `as_frame=False`.

```py
from sklearn.datasets import fetch_openml
mnist = fetch_openml('mnist_784', version=1, as_frame=False)
mnist.keys()
X, y = mnist["data"], mnist["target"]

X.shape
y.shape

%matplotlib inline
import matplotlib as mpl
import matplotlib.pyplot as plt

some_digit = X[0]
some_digit_image = some_digit.reshape(28, 28)
plt.imshow(some_digit_image, cmap=mpl.cm.binary)
plt.axis("off")

save_fig("some_digit_plot")
plt.show()
```

```
y = y.astype(np.uint8)
```

```py
def plot_digit(data):
    image = data.reshape(28, 28)
    plt.imshow(image, cmap = mpl.cm.binary,
               interpolation="nearest")
    plt.axis("off")
```

```py
# EXTRA
def plot_digits(instances, images_per_row=10, **options):
    size = 28
    images_per_row = min(len(instances), images_per_row)
    # This is equivalent to n_rows = ceil(len(instances) / images_per_row):
    n_rows = (len(instances) - 1) // images_per_row + 1

    # Append empty images to fill the end of the grid, if needed:
    n_empty = n_rows * images_per_row - len(instances)
    padded_instances = np.concatenate([instances, np.zeros((n_empty, size * size))], axis=0)

    # Reshape the array so it's organized as a grid containing 28×28 images:
    image_grid = padded_instances.reshape((n_rows, images_per_row, size, size))

    # Combine axes 0 and 2 (vertical image grid axis, and vertical image axis),
    # and axes 1 and 3 (horizontal axes). We first need to move the axes that we
    # want to combine next to each other, using transpose(), and only then we
    # can reshape:
    big_image = image_grid.transpose(0, 2, 1, 3).reshape(n_rows * size, images_per_row * size)
    # Now that we have a big image, we just need to show it:
    plt.imshow(big_image, cmap = mpl.cm.binary, **options)
    plt.axis("off")
```

```py
plt.figure(figsize=(9,9))
example_images = X[:100]
plot_digits(example_images, images_per_row=10)
save_fig("more_digits_plot")
plt.show()
```

```py
X_train, X_test, y_train, y_test = X[:60000], X[60000:], y[:60000], y[60000:]
```



1. fetch_openml是一个Python库中的函数，用于从OpenML开放机器学习平台上下载数据集。OpenML是一个旨在促进机器学习研究的在线社区，它提供了一个集中的存储库，包含了各种各样的标准化数据集和机器学习任务。

   fetch_openml函数允许用户从OpenML平台上获取数据集并加载到Python环境中，以供进一步的机器学习任务使用。它提供了一种便捷的方式来访问和使用各种数据集，无需手动下载和处理数据。

   使用fetch_openml函数，你可以根据数据集的名称或ID来获取数据集。它支持各种数据类型，包括分类数据、回归数据、图像数据等。一旦数据集下载完成，它会以一种易于使用的格式返回，通常是一个NumPy数组或Pandas数据帧。

   fetch_openml函数的一些常用参数包括：

   - name或data_id：指定数据集的名称或ID。
   - version：指定数据集的版本号。
   - as_frame：设置为True时，返回一个Pandas数据帧。
   - return_X_y：设置为True时，只返回特征矩阵和目标变量，而不返回其他元数据。

   以下是一个使用fetch_openml函数的示例：

   ```python
   from sklearn.datasets import fetch_openml
   
   # 通过数据集名称获取数据
   data = fetch_openml(name='iris')
   
   # 通过数据集ID获取数据
   data = fetch_openml(data_id=61)
   ```

   通过fetch_openml函数，你可以轻松地访问OpenML平台上的各种数据集，并将其用于机器学习研究、算法开发和数据分析等任务。

2. 如果使用`fetch_openml`函数来获取MNIST数据集并将其赋值给`mnist`变量，然后调用`mnist.keys()`，你将得到以下内容：

   ```python
   print(mnist.keys())
   ```

   输出结果可能如下所示：

   ```
   dict_keys(['data', 'target', 'feature_names', 'DESCR', 'details', 'categories', 'url'])
   ```

   这些键提供了对MNIST数据集的不同方面的访问：

   - `data`: 包含特征矩阵的NumPy数组，每一行表示一个样本，每一列表示一个特征。
   - `target`: 包含目标变量的NumPy数组，标识每个样本所属的类别。
   - `feature_names`: 特征的名称列表，如果适用的话。
   - `DESCR`: 数据集的描述信息。
   - `details`: 包含关于数据集的详细信息的字典。
   - `categories`: 如果数据集是分类数据，包含类别的名称列表。
   - `url`: 数据集的来源网址。

   你可以使用这些键来访问和操作MNIST数据集的不同部分，例如获取特征矩阵和目标变量，查看数据集的描述信息，以及了解其他相关信息。

3. `reshape()`函数是一个在NumPy数组中用于改变数组形状的函数。它允许你重新组织数组的维度，而不改变数组中的元素。

   `reshape()`函数的作用如下：

   1. 改变数组的形状：你可以使用`reshape()`函数来改变数组的维度和形状。通过指定新的形状，你可以将数组从一个形状转换为另一个形状，只要新形状的元素数量与原数组的元素数量保持一致。例如，你可以将一个一维数组转换为二维数组或多维数组，或者改变数组的行数和列数等。

   1. 改变数组的维度：`reshape()`函数可以用于改变数组的维度，从而改变数组中轴的数量和长度。你可以增加或减少数组的维度，根据需要重新组织轴的顺序，或将多维数组转换为高维数组。

   需要注意的是，`reshape()`函数返回一个新的数组，而不会修改原始数组。如果你希望在原地修改数组的形状，可以使用`resize()`函数。

   下面是一个使用`reshape()`函数的简单示例：

   ```python
   import numpy as np
   
   # 创建一个一维数组
   arr = np.array([1, 2, 3, 4, 5, 6])
   
   # 将一维数组转换为二维数组
   reshaped_arr = arr.reshape((2, 3))
   
   print(reshaped_arr)
   # 输出:
   # [[1 2 3]
   #  [4 5 6]]
   ```

   在上面的示例中，我们创建了一个一维数组`arr`，然后使用`reshape()`函数将其转换为一个2x3的二维数组`reshaped_arr`。

   总之，`reshape()`函数允许你在NumPy中重新组织数组的形状和维度，以适应不同的数据处理需求。

4. 当`imshow()`函数的`cmap`参数设置为`matplotlib.cm.binary`时，它将使用二进制（binary）颜色映射来显示图像。

   二进制颜色映射是一种灰度颜色映射，通常用于表示二值图像或灰度图像中的二值区域。它将较低的灰度值映射为黑色，较高的灰度值映射为白色，因此可以使图像中的二值区域更加明显。

   当你使用`imshow()`函数显示灰度图像，并将`cmap`参数设置为`matplotlib.cm.binary`时，图像中的较低灰度值将呈现为黑色，较高灰度值将呈现为白色，中间灰度值则在黑色和白色之间平滑过渡。

   下面是一个示例，展示了如何使用`cmap=matplotlib.cm.binary`参数来显示灰度图像：

   ```python
   import numpy as np
   import matplotlib.pyplot as plt
   
   # 创建一个随机的灰度图像
   image = np.random.random((100, 100))
   
   # 显示灰度图像，使用二进制颜色映射
   plt.imshow(image, cmap=plt.cm.binary)
   
   # 添加标题和颜色条
   plt.title('Binary Image')
   plt.colorbar()
   
   # 显示图像
   plt.show()
   ```

   在上面的示例中，我们创建了一个随机的灰度图像，并使用`cmap=plt.cm.binary`参数将图像显示为二进制颜色映射。这将使较低灰度值的区域呈现为黑色，较高灰度值的区域呈现为白色。

   总之，当你将`cmap`参数设置为`matplotlib.cm.binary`时，`imshow()`函数将使用二进制颜色映射来显示灰度图像，突出显示图像中的二值区域。

5. `matplotlib.axis("off")`这句话的作用是在绘制图形时隐藏坐标轴。

   当你使用`matplotlib`库绘制图形时，默认情况下会显示坐标轴，包括 x 轴和 y 轴上的刻度标签和刻度线。然而，在某些情况下，你可能希望隐藏坐标轴，以便更好地突出显示图像或图表的内容。

   通过调用`matplotlib.axis("off")`，你可以将坐标轴设置为不可见状态，即隐藏它们。这将导致绘制的图形不再显示任何坐标轴。

   下面是一个简单的示例，展示了如何使用`matplotlib.axis("off")`来隐藏坐标轴：

   ```python
   import matplotlib.pyplot as plt
   
   # 创建一个简单的图形
   plt.plot([1, 2, 3, 4], [1, 4, 9, 16])
   
   # 隐藏坐标轴
   plt.axis("off")
   
   # 显示图形
   plt.show()
   ```

   在上面的示例中，我们创建了一个简单的图形（在这里是一条直线），然后使用`plt.axis("off")`隐藏了坐标轴。这样，绘制的图形将不再显示任何坐标轴。

   总之，通过调用`matplotlib.axis("off")`，你可以隐藏绘制图形时的坐标轴，以便更好地突出显示图像或图表的内容。

6. `astype(numpy.uint8)`的作用是将数组的元素类型转换为无符号8位整数（unsigned 8-bit integer）。在NumPy中，`uint8`是表示无符号8位整数的数据类型。

   无符号8位整数的取值范围是从0到255，因此它可以表示的整数范围是有限的。通过将数组元素类型转换为`uint8`，可以将原始数据限制在0到255之间，并且以较小的存储空间存储数据。

   下面是一个示例，展示了`astype(numpy.uint8)`的使用：

   ```python
   import numpy as np
   
   # 创建一个浮点数数组
   arr = np.array([0.1, 0.5, 1.2, 2.7, 3.8])
   
   # 将浮点数数组转换为无符号8位整数数组
   arr_uint8 = arr.astype(np.uint8)
   
   print(arr_uint8)
   ```

   在上面的示例中，我们创建了一个浮点数数组`arr`，然后使用`astype()`函数将其转换为无符号8位整数数组`arr_uint8`。由于浮点数数组的元素类型为`float64`（默认的浮点数类型），转换为`uint8`会将浮点数截断为整数，并将其限制在0到255的范围内。

   输出结果是：

   ```
   [0 0 1 2 3]
   ```

   可以看到，浮点数数组的元素被转换为了无符号8位整数，并且小数部分被截断。由于浮点数的取值范围较大，转换为8位整数可能会导致信息的丢失，因此需要谨慎使用。

   总之，`astype(numpy.uint8)`的作用是将数组的元素类型转换为无符号8位整数，将数据限制在0到255之间，并以较小的存储空间存储数据。这对于一些特定的应用场景，如图像处理和像素操作等，可能会很有用。

7. 这段代码的作用是将两个数组进行连接，并生成一个新的数组 `padded_instances`。

   具体来说，这段代码使用了 `np.concatenate()` 函数将两个数组 `instances` 和 `np.zeros((n_empty, size * size))` 沿着指定的轴 `axis=0` 进行连接。连接的结果存储在新的数组 `padded_instances` 中。

   解释一下每个部分的含义：

   - `instances`：一个数组，表示包含实例的数据。
   - `np.zeros((n_empty, size * size))`：一个由零组成的数组，形状为 `(n_empty, size * size)`。这个数组用于填充空缺的部分。
   - `axis=0`：指定连接操作沿着第一个维度（行）进行。

   通过这段代码，我们可以将 `instances` 数组和一个由零填充的数组连接在一起，以填充数据中的空缺部分。这在数据处理中常用于对齐不同长度的数据，使它们具有相同的形状。

   以下是一个示例，展示了如何使用上述代码进行数组连接：

   ```python
   import numpy as np
   
   # 创建一个示例数组
   instances = np.array([[1, 2, 3], [4, 5, 6]])
   
   # 定义连接参数
   n_empty = 2
   size = 3
   
   # 进行数组连接
   padded_instances = np.concatenate([instances, np.zeros((n_empty, size))], axis=0)
   
   print(padded_instances)
   ```

   在上述示例中，我们创建了一个示例数组 `instances`，它包含了两个形状为 `(3,)` 的实例。然后，我们使用 `np.zeros()` 函数创建一个由零组成的数组，形状为 `(n_empty, size * size)`，这里是 `(2, 9)`。接着，我们使用 `np.concatenate()` 函数将 `instances` 数组和零填充数组沿着第一个维度进行连接。

   输出结果为：

   ```
   [[1. 2. 3.]
    [4. 5. 6.]
    [0. 0. 0.]
    [0. 0. 0.]]
   ```

   可以看到，`padded_instances` 数组是将 `instances` 数组和零填充数组连接在一起的结果。

   总之，通过使用 `np.concatenate()` 函数，可以将两个数组沿指定的轴连接在一起，生成一个新的数组。这对于在数据处理中对齐不同长度的数据非常有用，可以填充数据中的空缺部分。



## Training a Binary Classifier

```py
y_train_5 = (y_train == 5)
y_test_5 = (y_test == 5)
```

**Note**: some hyperparameters will have a different defaut value in future versions of Scikit-Learn, such as `max_iter` and `tol`. To be future-proof, we explicitly set these hyperparameters to their future default values. For simplicity, this is not shown in the book.

```py
from sklearn.linear_model import SGDClassifier

sgd_clf = SGDClassifier(max_iter=1000, tol=1e-3, random_state=42)
sgd_clf.fit(X_train, y_train_5)
```

```py
sgd_clf.predict([some_digit])
```

```py
from sklearn.model_selection import cross_val_score
cross_val_score(sgd_clf, X_train, y_train_5, cv=3, scoring="accuracy")
```

1. 这段代码创建了一个 `SGDClassifier` 的实例对象 `sgd_clf`，并设置了一些参数。

   具体来说，这段代码的作用如下：

   1. `max_iter=1000`：设置最大迭代次数为 1000。这表示模型在训练过程中最多迭代 1000 次，每一次迭代使用一部分数据进行更新。当达到最大迭代次数或达到收敛条件时，模型的训练过程将停止。

   1. `tol=1e-3`：设置收敛阈值（tolerance）为 0.001。这是一个控制模型收敛的参数，当模型在两次迭代之间的损失变化小于该阈值时，认为模型已经收敛，训练过程将停止。

   1. `random_state=42`：设置随机种子（random seed）为 42。随机种子用于控制模型中的随机性，设置相同的种子可以使结果可复现，即每次运行代码得到的结果相同。

   通过设置这些参数，`sgd_clf` 对象将具有指定的最大迭代次数、收敛阈值和随机种子。你可以使用该对象进行模型训练和预测，或者通过调整其他参数来进一步定制模型的行为。

   以下是一个示例，展示了如何使用上述代码创建 `SGDClassifier` 对象：

   ```python
   from sklearn.linear_model import SGDClassifier
   
   # 创建 SGDClassifier 对象
   sgd_clf = SGDClassifier(max_iter=1000, tol=1e-3, random_state=42)
   
   # 使用 sgd_clf 进行模型训练和预测
   # ...
   ```

   在上述示例中，我们导入了 `SGDClassifier` 类，并使用给定的参数创建了一个 `sgd_clf` 对象。然后，我们可以使用 `sgd_clf` 对象进行模型训练和预测，具体的训练和预测步骤根据具体的数据和问题而定。

   总之，通过设置 `max_iter`、`tol` 和 `random_state` 等参数，可以创建一个具有特定配置的 `SGDClassifier` 对象，用于分类问题的训练和预测。



## Performance Measures

#### Measuring Accuracy Using Cross-Validation

```py
from sklearn.model_selection import StratifiedKFold
from sklearn.base import clone

skfolds = StratifiedKFold(n_splits=3, shuffle=True, random_state=42)

for train_index, test_index in skfolds.split(X_train, y_train_5):
    clone_clf = clone(sgd_clf)
    X_train_folds = X_train[train_index]
    y_train_folds = y_train_5[train_index]
    X_test_fold = X_train[test_index]
    y_test_fold = y_train_5[test_index]

    clone_clf.fit(X_train_folds, y_train_folds)
    y_pred = clone_clf.predict(X_test_fold)
    n_correct = sum(y_pred == y_test_fold)
    print(n_correct / len(y_pred))
```

**Note**: `shuffle=True` was omitted by mistake in previous releases of the book.

```py
from sklearn.base import BaseEstimator
class Never5Classifier(BaseEstimator):
    def fit(self, X, y=None):
        pass
    def predict(self, X):
        return np.zeros((len(X), 1), dtype=bool)
```

```py
never_5_clf = Never5Classifier()
cross_val_score(never_5_clf, X_train, y_train_5, cv=3, scoring="accuracy")
```

1. 这段代码实现了使用分层交叉验证（Stratified K-Fold Cross Validation）对分类器进行评估的过程。下面是代码的具体作用解释：

   1. 首先，从scikit-learn库中导入了必要的模块和函数，包括`StratifiedKFold`用于分层交叉验证、`clone`用于创建分类器的克隆副本。

   1. 创建了一个`StratifiedKFold`对象`skfolds`，设置了参数`n_splits=3`表示将数据划分为3个折叠（即3折交叉验证），`shuffle=True`表示在进行划分之前对数据进行洗牌，`random_state=42`用于设置随机种子以确保可复现的划分结果。

   1. 在`for`循环中，使用`skfolds.split(X_train, y_train_5)`方法迭代生成每个折叠的训练集和测试集的索引。其中，`X_train`是特征数据，`y_train_5`是对应的目标变量（二分类标签）。

   1. 在每次迭代中，首先使用`clone(sgd_clf)`创建了分类器的克隆副本`clone_clf`，以确保每个折叠都使用相同的初始分类器。

   1. 将训练集和测试集的特征数据和标签分别赋值给`X_train_folds`、`y_train_folds`、`X_test_fold`和`y_test_fold`变量。

   1. 使用`clone_clf.fit(X_train_folds, y_train_folds)`对克隆的分类器进行训练，使用训练集的特征数据和标签。

   1. 使用训练好的分类器`clone_clf`对测试集的特征数据`X_test_fold`进行预测，得到预测结果`y_pred`。

   1. 通过比较预测结果`y_pred`和测试集的真实标签`y_test_fold`，计算正确预测的样本数量`n_correct`。

   1. 打印输出正确预测的样本比例，即准确率（Accuracy）。

   通过使用分层交叉验证，该代码段可以评估分类器在不同的训练集和测试集上的性能，并打印每个折叠的准确率。这有助于评估分类器的泛化能力和稳定性，避免对特定数据集的过拟合或欠拟合。

2. 将数据划分为3个折叠意味着将原始数据集分成3个部分，每个部分称为一个折叠。在每次交叉验证中，将其中一个折叠作为测试集，而其他两个折叠作为训练集。这样的过程会依次遍历所有折叠，确保每个折叠都会被用作测试集，并且每个样本都有机会在测试集中出现一次。

   具体来说，在这段代码中，使用了分层交叉验证（Stratified K-Fold Cross Validation），其中数据被划分为3个折叠。分层交叉验证在划分数据时会保持不同类别样本的比例。这对于处理不平衡数据集（其中某个类别的样本数量明显少于其他类别）特别有用，因为它可以确保每个折叠中都包含各个类别的样本。

   在每次迭代中，其中一个折叠将被用作测试集，而其他两个折叠将被用作训练集。然后，使用训练集对分类器进行训练，并使用测试集进行预测和性能评估。整个过程会重复3次，以确保每个折叠都充当过测试集，从而得到更准确的性能评估结果。最终，代码会打印每个折叠的准确率（Accuracy），以评估分类器的性能。



#### Confusion Matrix

```py
from sklearn.model_selection import cross_val_predict

y_train_pred = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3)
```

```py
from sklearn.metrics import confusion_matrix

confusion_matrix(y_train_5, y_train_pred)
```

```py
y_train_perfect_predictions = y_train_5  # pretend we reached perfection
confusion_matrix(y_train_5, y_train_perfect_predictions)
```



#### Precision and Recall

```py
from sklearn.metrics import precision_score, recall_score

precision_score(y_train_5, y_train_pred)
```

```py
cm = confusion_matrix(y_train_5, y_train_pred)
cm[1, 1] / (cm[0, 1] + cm[1, 1])
```

```py
recall_score(y_train_5, y_train_pred)
```

```py
cm[1, 1] / (cm[1, 0] + cm[1, 1])
```

```py
from sklearn.metrics import f1_score

f1_score(y_train_5, y_train_pred)
```

```py
cm[1, 1] / (cm[1, 1] + (cm[1, 0] + cm[0, 1]) / 2)
```



#### Precision/Recall Trade-off

```py
y_scores = sgd_clf.decision_function([some_digit])
y_scores

threshold = 0
y_some_digit_pred = (y_scores > threshold)
y_some_digit_pred

threshold = 8000
y_some_digit_pred = (y_scores > threshold)
y_some_digit_pred
```

这段代码的作用是使用一个随机梯度下降分类器（`sgd_clf`）对一个数字进行分类，并根据不同的阈值（`threshold`）确定分类结果。

代码的执行步骤如下：

1. `sgd_clf.decision_function([some_digit])`：这一行代码计算了分类器对输入数字 `some_digit` 的决策函数值（decision function）。决策函数值表示输入样本属于正类的置信度，或者说与正类的距离。这里将 `some_digit` 作为一个单独的样本传递给 `decision_function` 方法，返回一个包含决策函数值的数组 `y_scores`。

1. `y_scores`：这一行代码打印输出了决策函数值数组 `y_scores`，可以观察到 `some_digit` 属于正类的置信度。

1. `threshold = 0`：将阈值设为0。

1. `y_some_digit_pred = (y_scores > threshold)`：这一行代码将根据阈值判断 `some_digit` 的预测结果。将决策函数值 `y_scores` 与阈值进行比较，生成一个布尔数组 `y_some_digit_pred`，其中元素为 `True` 表示对应决策函数值大于阈值，即预测为正类（数字的分类结果），而元素为 `False` 表示对应决策函数值小于等于阈值，即预测为负类。

1. `y_some_digit_pred`：这一行代码打印输出了预测结果数组 `y_some_digit_pred`，可以观察到基于阈值0的预测结果。

1. `threshold = 8000`：将阈值设为8000。

1. `y_some_digit_pred = (y_scores > threshold)`：这一行代码重新根据新的阈值判断 `some_digit` 的预测结果。将决策函数值 `y_scores` 与新的阈值进行比较，生成一个新的布尔数组 `y_some_digit_pred`，其中元素为 `True` 表示对应决策函数值大于阈值，即预测为正类，而元素为 `False` 表示对应决策函数值小于等于阈值，即预测为负类。

1. `y_some_digit_pred`：这一行代码打印输出了基于新阈值的预测结果数组 `y_some_digit_pred`，可以观察到基于阈值8000的预测结果。

这段代码的目的是通过调整阈值来观察分类器对数字的预测结果的变化。不同的阈值可能导致不同的分类结果，可以用于探索分类器的性能和调整分类器的准确率和召回率等指标。

```py
from sklearn.metrics import precision_recall_curve

precisions, recalls, thresholds = precision_recall_curve(y_train_5, y_scores)
```

```py
def plot_precision_recall_vs_threshold(precisions, recalls, thresholds):
    plt.plot(thresholds, precisions[:-1], "b--", label="Precision", linewidth=2)
    plt.plot(thresholds, recalls[:-1], "g-", label="Recall", linewidth=2)
    plt.legend(loc="center right", fontsize=16) # Not shown in the book
    plt.xlabel("Threshold", fontsize=16)        # Not shown
    plt.grid(True)                              # Not shown
    plt.axis([-50000, 50000, 0, 1])             # Not shown



recall_90_precision = recalls[np.argmax(precisions >= 0.90)]
threshold_90_precision = thresholds[np.argmax(precisions >= 0.90)]


plt.figure(figsize=(8, 4))                                                                  # Not shown
plot_precision_recall_vs_threshold(precisions, recalls, thresholds)
plt.plot([threshold_90_precision, threshold_90_precision], [0., 0.9], "r:")                 # Not shown
plt.plot([-50000, threshold_90_precision], [0.9, 0.9], "r:")                                # Not shown
plt.plot([-50000, threshold_90_precision], [recall_90_precision, recall_90_precision], "r:")# Not shown
plt.plot([threshold_90_precision], [0.9], "ro")                                             # Not shown
plt.plot([threshold_90_precision], [recall_90_precision], "ro")                             # Not shown
save_fig("precision_recall_vs_threshold_plot")                                              # Not shown
plt.show()
```

这段代码使用了`sklearn.metrics`模块中的`precision_recall_curve`函数来计算分类器的精确率（precision）、召回率（recall）和阈值（thresholds）。

具体解释如下：

1. 导入`precision_recall_curve`函数：从`sklearn.metrics`模块中导入`precision_recall_curve`函数，该函数用于计算分类器的精确率、召回率和阈值。

1. 调用`precision_recall_curve`函数：使用`precision_recall_curve`函数计算分类器的精确率、召回率和阈值。该函数接受两个参数：

   - `y_train_5`：训练集的真实标签，用于计算精确率和召回率。
   - `y_scores`：分类器对训练集样本的决策函数值，用于计算精确率、召回率和阈值。

1. 返回结果：`precision_recall_curve`函数的返回结果包含三个数组：

   - `precisions`：精确率数组，记录了不同阈值下的精确率值。
   - `recalls`：召回率数组，记录了不同阈值下的召回率值。
   - `thresholds`：阈值数组，记录了用于计算精确率和召回率的阈值值。

通过使用`precision_recall_curve`函数，可以获得分类器在不同阈值下的精确率和召回率，并且可以使用这些值来绘制精确率-召回率曲线，以评估分类器的性能和进行模型选择。

```py
(y_train_pred == (y_scores > 0)).all()
```

```py
def plot_precision_vs_recall(precisions, recalls):
    plt.plot(recalls, precisions, "b-", linewidth=2)
    plt.xlabel("Recall", fontsize=16)
    plt.ylabel("Precision", fontsize=16)
    plt.axis([0, 1, 0, 1])
    plt.grid(True)

plt.figure(figsize=(8, 6))
plot_precision_vs_recall(precisions, recalls)
plt.plot([recall_90_precision, recall_90_precision], [0., 0.9], "r:")
plt.plot([0.0, recall_90_precision], [0.9, 0.9], "r:")
plt.plot([recall_90_precision], [0.9], "ro")
save_fig("precision_vs_recall_plot")
plt.show()
```

```py
threshold_90_precision = thresholds[np.argmax(precisions >= 0.90)]
threshold_90_precision
```

```py
y_train_pred_90 = (y_scores >= threshold_90_precision)
precision_score(y_train_5, y_train_pred_90)
recall_score(y_train_5, y_train_pred_90)
```



#### The ROC Curve

```py
from sklearn.metrics import roc_curve

fpr, tpr, thresholds = roc_curve(y_train_5, y_scores)
```

```py
def plot_roc_curve(fpr, tpr, label=None):
    plt.plot(fpr, tpr, linewidth=2, label=label)
    plt.plot([0, 1], [0, 1], 'k--') # dashed diagonal
    plt.axis([0, 1, 0, 1])                                    # Not shown in the book
    plt.xlabel('False Positive Rate (Fall-Out)', fontsize=16) # Not shown
    plt.ylabel('True Positive Rate (Recall)', fontsize=16)    # Not shown
    plt.grid(True)                                            # Not shown

plt.figure(figsize=(8, 6))                                    # Not shown
plot_roc_curve(fpr, tpr)
fpr_90 = fpr[np.argmax(tpr >= recall_90_precision)]           # Not shown
plt.plot([fpr_90, fpr_90], [0., recall_90_precision], "r:")   # Not shown
plt.plot([0.0, fpr_90], [recall_90_precision, recall_90_precision], "r:")  # Not shown
plt.plot([fpr_90], [recall_90_precision], "ro")               # Not shown
save_fig("roc_curve_plot")                                    # Not shown
plt.show()
```

```py
from sklearn.metrics import roc_auc_score

roc_auc_score(y_train_5, y_scores)
```

这段代码使用了`sklearn.metrics`模块中的`roc_auc_score`函数来计算二分类问题中的ROC曲线下的面积（ROC AUC）。

具体解释如下：

1. 导入`roc_auc_score`函数：从`sklearn.metrics`模块中导入`roc_auc_score`函数，该函数用于计算二分类问题中的ROC AUC。

1. 调用`roc_auc_score`函数：使用`roc_auc_score`函数计算ROC曲线下的面积（ROC AUC）。该函数接受两个参数：

   - `y_train_5`：训练集的真实标签，用于计算ROC曲线下的面积。
   - `y_scores`：分类器对训练集样本的决策函数值，用于计算ROC曲线下的面积。

1. 返回结果：`roc_auc_score`函数的返回结果是一个浮点数，表示计算得到的ROC曲线下的面积（ROC AUC）。ROC AUC的取值范围在0到1之间，值越接近1表示分类器的性能越好，值越接近0.5表示分类器的性能越差。

通过使用`roc_auc_score`函数，可以评估分类器在二分类问题中的性能，衡量其对正负样本的分类能力，并与其他分类器进行比较。

**Note**: we set `n_estimators=100` to be future-proof since this will be the default value in Scikit-Learn 0.22.

```py
from sklearn.ensemble import RandomForestClassifier
forest_clf = RandomForestClassifier(n_estimators=100, random_state=42)
y_probas_forest = cross_val_predict(forest_clf, X_train, y_train_5, cv=3,
                                    method="predict_proba")
```

这段代码使用了`sklearn.ensemble`模块中的`RandomForestClassifier`类和`cross_val_predict`函数来进行随机森林分类器的交叉验证预测。

具体解释如下：

1. 导入`RandomForestClassifier`类：从`sklearn.ensemble`模块中导入`RandomForestClassifier`类，该类用于创建随机森林分类器。

1. 创建随机森林分类器对象：使用`RandomForestClassifier`类创建一个随机森林分类器对象`forest_clf`。在这个例子中，随机森林分类器被配置为包含100棵决策树，并设置`random_state=42`以确保结果的可复现性。

1. 进行交叉验证预测：使用`cross_val_predict`函数进行交叉验证预测。该函数接受以下参数：

   - `forest_clf`：要使用的分类器对象，这里是随机森林分类器`forest_clf`。
   - `X_train`：训练集的特征数据。
   - `y_train_5`：训练集的真实标签，表示是否为数字5的标签。
   - `cv=3`：指定进行3折交叉验证。
   - `method="predict_proba"`：指定使用分类器的`predict_proba`方法进行预测，返回的是样本属于各个类别的概率。

1. 返回结果：`cross_val_predict`函数的返回结果是一个包含所有交叉验证样本的预测概率数组`y_probas_forest`。数组的每一行对应一个样本，每一列对应一个类别的概率。

这段代码的目的是使用随机森林分类器对训练集进行交叉验证预测，并获取每个样本属于各个类别的概率。这可以用于进一步的模型评估和分析。

```py
y_scores_forest = y_probas_forest[:, 1] # score = proba of positive class
fpr_forest, tpr_forest, thresholds_forest = roc_curve(y_train_5,y_scores_forest)
```

这段代码使用了`roc_curve`函数来计算随机森林分类器的ROC曲线的假正例率（FPR）、真正例率（TPR）和阈值（thresholds）。

具体解释如下：

1. `y_probas_forest[:, 1]`：这一行代码从随机森林分类器的预测概率数组`y_probas_forest`中提取出属于正类的概率值。通常，正类的索引为1，因此使用`[:, 1]`来获取正类的概率。

1. `roc_curve(y_train_5, y_scores_forest)`：这一行代码调用`roc_curve`函数，计算ROC曲线的FPR、TPR和阈值。该函数接受两个参数：

   - `y_train_5`：训练集的真实标签，用于计算ROC曲线。
   - `y_scores_forest`：随机森林分类器的预测分数或概率，这里使用随机森林分类器预测的正类概率值。

1. 返回结果：`roc_curve`函数的返回结果包含三个数组：

   - `fpr_forest`：假正例率数组，记录了不同阈值下的假正例率值。
   - `tpr_forest`：真正例率数组，记录了不同阈值下的真正例率值。
   - `thresholds_forest`：阈值数组，记录了用于计算假正例率和真正例率的阈值值。

通过使用`roc_curve`函数，可以获得随机森林分类器在不同阈值下的FPR和TPR，并且可以使用这些值来绘制ROC曲线，进一步评估分类器的性能。

```py
recall_for_forest = tpr_forest[np.argmax(fpr_forest >= fpr_90)]

plt.figure(figsize=(8, 6))
plt.plot(fpr, tpr, "b:", linewidth=2, label="SGD")
plot_roc_curve(fpr_forest, tpr_forest, "Random Forest")
plt.plot([fpr_90, fpr_90], [0., recall_90_precision], "r:")
plt.plot([0.0, fpr_90], [recall_90_precision, recall_90_precision], "r:")
plt.plot([fpr_90], [recall_90_precision], "ro")
plt.plot([fpr_90, fpr_90], [0., recall_for_forest], "r:")
plt.plot([fpr_90], [recall_for_forest], "ro")
plt.grid(True)
plt.legend(loc="lower right", fontsize=16)
save_fig("roc_curve_comparison_plot")
plt.show()
```

```py
roc_auc_score(y_train_5, y_scores_forest)
```

这段代码使用了`roc_auc_score`函数来计算随机森林分类器的ROC AUC（曲线下的面积）。

具体解释如下：

1. `roc_auc_score(y_train_5, y_scores_forest)`：这一行代码调用`roc_auc_score`函数，计算随机森林分类器的ROC AUC。该函数接受两个参数：

   - `y_train_5`：训练集的真实标签，用于计算ROC AUC。
   - `y_scores_forest`：随机森林分类器的预测分数或概率，这里使用随机森林分类器预测的正类概率值。

1. 返回结果：`roc_auc_score`函数的返回结果是一个浮点数，表示随机森林分类器的ROC曲线下的面积（ROC AUC）。ROC AUC的取值范围在0到1之间，值越接近1表示分类器的性能越好，值越接近0.5表示分类器的性能越差。

通过使用`roc_auc_score`函数，可以评估随机森林分类器在二分类问题中的性能，衡量其对正负样本的分类能力，并与其他分类器进行比较。

```py
y_train_pred_forest = cross_val_predict(forest_clf, X_train, y_train_5, cv=3)
precision_score(y_train_5, y_train_pred_forest)
```

这段代码使用了`cross_val_predict`函数和`precision_score`函数来计算随机森林分类器的精确率（precision）。

具体解释如下：

1. `cross_val_predict(forest_clf, X_train, y_train_5, cv=3)`：这一行代码使用`cross_val_predict`函数进行交叉验证预测。函数的参数包括：

   - `forest_clf`：随机森林分类器对象。
   - `X_train`：训练集的特征数据。
   - `y_train_5`：训练集的真实标签，表示是否为数字5的标签。
   - `cv=3`：指定进行3折交叉验证。

   该函数返回一个包含所有交叉验证样本的预测标签数组`y_train_pred_forest`。

1. `precision_score(y_train_5, y_train_pred_forest)`：这一行代码调用`precision_score`函数，计算随机森林分类器的精确率。函数的参数包括：

   - `y_train_5`：训练集的真实标签。
   - `y_train_pred_forest`：随机森林分类器的预测标签。

   该函数返回一个浮点数，表示随机森林分类器的精确率。

通过使用`cross_val_predict`函数和`precision_score`函数，可以对随机森林分类器进行交叉验证预测，并计算其在训练集上的精确率。这有助于评估分类器的性能和准确性。

```py
recall_score(y_train_5, y_train_pred_forest)
```

这段代码使用了`recall_score`函数来计算随机森林分类器的召回率（recall）。

具体解释如下：

1. `recall_score(y_train_5, y_train_pred_forest)`：这行代码调用`recall_score`函数，计算随机森林分类器的召回率。函数的参数包括：

   - `y_train_5`：训练集的真实标签。
   - `y_train_pred_forest`：随机森林分类器的预测标签。

   该函数返回一个浮点数，表示随机森林分类器的召回率。

通过使用`recall_score`函数，可以评估随机森林分类器在训练集上的召回率，即分类器正确识别正样本的能力。召回率越高，表示分类器能够更好地捕捉到正样本，具有更高的检测能力。





## Multiclass Classification

```py
from sklearn.svm import SVC

svm_clf = SVC(gamma="auto", random_state=42)
svm_clf.fit(X_train[:1000], y_train[:1000]) # y_train, not y_train_5
svm_clf.predict([some_digit])
```

```py
some_digit_scores = svm_clf.decision_function([some_digit])
some_digit_scores
```

```py
np.argmax(some_digit_scores)
```

这一行代码调用`np.argmax`函数，对数组`some_digit_scores`进行操作。函数的参数是一个数组或列表

```
svm_clf.classes_
```

`svm_clf.classes_`是一个属性，它返回支持向量机分类器（SVM）`svm_clf`所识别的类别列表。

具体解释如下：

`svm_clf.classes_`属性返回一个包含分类器所识别的类别的数组或列表。每个类别在数组中的位置与其对应的类别标签相关联。

例如，如果支持向量机分类器是一个二分类器，它可以识别两个类别，比如正类和负类。那么`svm_clf.classes_`将返回一个包含这两个类别的数组，其中第一个位置对应负类标签，第二个位置对应正类标签。

通过查看`svm_clf.classes_`属性，可以了解支持向量机分类器所识别的类别，以便在需要时进行相关处理或分析。

```py
from sklearn.multiclass import OneVsRestClassifier
ovr_clf = OneVsRestClassifier(SVC(gamma="auto", random_state=42))
ovr_clf.fit(X_train[:1000], y_train[:1000])
ovr_clf.predict([some_digit])
```

这段代码使用了`OneVsRestClassifier`类来实现多类别分类，并训练了一个多类别的支持向量机分类器。

具体解释如下：

1. `from sklearn.multiclass import OneVsRestClassifier`：这行代码导入了`OneVsRestClassifier`类，它是用于多类别分类的一对多（One-vs-Rest）策略的分类器。

1. `ovr_clf = OneVsRestClassifier(SVC(gamma="auto", random_state=42))`：这行代码创建了一个`OneVsRestClassifier`对象，并指定使用`SVC`作为基础分类器。`SVC`是支持向量机分类器，参数`gamma="auto"`表示使用自动选择的gamma值，`random_state=42`表示设置随机种子以确保可重复的结果。

1. `ovr_clf.fit(X_train[:1000], y_train[:1000])`：这行代码对训练集的前1000个样本进行训练，使用`fit`方法拟合（训练）`OneVsRestClassifier`对象。

1. `ovr_clf.predict([some_digit])`：这行代码使用训练好的多类别支持向量机分类器进行预测。`predict`方法接受输入样本，并返回预测的类别结果。

通过使用`OneVsRestClassifier`类，可以将二分类器（如支持向量机）扩展为多类别分类器。此代码段中的`ovr_clf`对象是一个多类别分类器，它使用了支持向量机作为基础分类器，并且在训练集上进行了拟合。最后，使用`predict`方法对`some_digit`样本进行预测，并返回预测的类别结果。

```
len(ovr_clf.estimators_)
```

`len(ovr_clf.estimators_)`是一个用于获取`OneVsRestClassifier`对象中基础分类器数量的代码。

具体解释如下：

1. `ovr_clf.estimators_`是`OneVsRestClassifier`对象的属性，它返回一个列表，包含了该对象内部使用的基础分类器（estimator）。

1. `len(ovr_clf.estimators_)`使用`len()`函数获取基础分类器列表的长度，即基础分类器的数量。

通过这段代码可以获得`OneVsRestClassifier`对象中基础分类器的数量，这对于了解多类别分类器的内部结构和基础分类器的个数非常有用。

```py
sgd_clf.fit(X_train, y_train)
sgd_clf.predict([some_digit])

sgd_clf.decision_function([some_digit])
```

这段代码使用了`decision_function`方法来计算随机梯度下降分类器（SGDClassifier）对于给定输入样本`some_digit`的决策函数值。

具体解释如下：

1. `sgd_clf.decision_function([some_digit])`：这行代码调用了`decision_function`方法，传入`[some_digit]`作为输入样本。`decision_function`方法用于计算分类器对于给定输入样本的决策函数值。

   - `sgd_clf`：代表随机梯度下降分类器对象。
   - `[some_digit]`：单个输入样本，通常是一个特征向量。

1. 返回结果：`decision_function`方法的返回结果是一个一维数组，其中包含了输入样本`some_digit`的决策函数值。决策函数值表示样本被分类为正类的置信度或距离，值的大小可以用来判断分类器对于该样本的分类倾向。

通过使用`decision_function`方法，可以获取随机梯度下降分类器对于给定输入样本的决策函数值，进而进行分类或进行其他相关分析。

```py
cross_val_score(sgd_clf, X_train, y_train, cv=3, scoring="accuracy")
```

这段代码使用了`cross_val_score`函数来进行交叉验证评估随机梯度下降分类器（SGDClassifier）的准确率（accuracy）。

具体解释如下：

1. `cross_val_score(sgd_clf, X_train, y_train, cv=3, scoring="accuracy")`：这行代码调用了`cross_val_score`函数，进行交叉验证评估。函数的参数包括：

   - `sgd_clf`：随机梯度下降分类器对象。
   - `X_train`：训练集的特征数据。
   - `y_train`：训练集的真实标签。
   - `cv=3`：指定进行3折交叉验证。
   - `scoring="accuracy"`：指定评估指标为准确率。

   `cross_val_score`函数将数据集拆分为多个训练集和验证集的组合，然后对每个组合进行训练和评估。最后返回一个包含每次验证的准确率的数组。

通过使用`cross_val_score`函数，可以进行交叉验证评估随机梯度下降分类器的准确率，以评估分类器的性能和泛化能力。这对于选择模型、调整参数以及比较不同分类器的性能非常有用。

```py
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train.astype(np.float64))
cross_val_score(sgd_clf, X_train_scaled, y_train, cv=3, scoring="accuracy")
```

这段代码使用了`StandardScaler`进行特征缩放，并使用缩放后的特征数据进行交叉验证评估随机梯度下降分类器（SGDClassifier）的准确率。

具体解释如下：

1. `from sklearn.preprocessing import StandardScaler`：这行代码导入了`StandardScaler`类，用于特征缩放。

1. `scaler = StandardScaler()`：这行代码创建了一个`StandardScaler`对象，用于对特征进行缩放。

1. `X_train_scaled = scaler.fit_transform(X_train.astype(np.float64))`：这行代码使用`fit_transform`方法对训练集的特征数据进行缩放。`fit_transform`方法会根据训练集数据计算缩放所需的均值和标准差，并将训练集进行缩放转换。

1. `cross_val_score(sgd_clf, X_train_scaled, y_train, cv=3, scoring="accuracy")`：这行代码使用缩放后的特征数据进行交叉验证评估。函数的参数包括：

   - `sgd_clf`：随机梯度下降分类器对象。
   - `X_train_scaled`：缩放后的训练集特征数据。
   - `y_train`：训练集的真实标签。
   - `cv=3`：指定进行3折交叉验证。
   - `scoring="accuracy"`：指定评估指标为准确率。

   `cross_val_score`函数将缩放后的数据集拆分为多个训练集和验证集的组合，然后对每个组合进行训练和评估。最后返回一个包含每次验证的准确率的数组。

通过对特征进行缩放，可以消除不同特征之间的量纲差异，使得它们具有相似的尺度，从而有助于提高分类器的性能。在这段代码中，特征缩放的操作是通过`StandardScaler`实现的。然后，使用缩放后的特征数据进行交叉验证评估随机梯度下降分类器的准确率，以评估模型的性能和泛化能力。



## Error Analysis

```py
y_train_pred = cross_val_predict(sgd_clf, X_train_scaled, y_train, cv=3)
conf_mx = confusion_matrix(y_train, y_train_pred)
conf_mx 
```

```py
# since sklearn 0.22, you can use sklearn.metrics.plot_confusion_matrix()
def plot_confusion_matrix(matrix):
    """If you prefer color and a colorbar"""
    fig = plt.figure(figsize=(8,8))
    ax = fig.add_subplot(111)
    cax = ax.matshow(matrix)
    fig.colorbar(cax)
```

```py
plt.matshow(conf_mx, cmap=plt.cm.gray)
save_fig("confusion_matrix_plot", tight_layout=False)
plt.show()
```

```py
row_sums = conf_mx.sum(axis=1, keepdims=True)
norm_conf_mx = conf_mx / row_sums
```

这段代码用于计算混淆矩阵（Confusion Matrix）的归一化版本。

具体解释如下：

1. `row_sums = conf_mx.sum(axis=1, keepdims=True)`：这行代码计算混淆矩阵每一行的元素和。`conf_mx`是原始的混淆矩阵，`axis=1`表示按行求和，`keepdims=True`保持结果的维度与原始矩阵一致。

1. `norm_conf_mx = conf_mx / row_sums`：这行代码计算归一化的混淆矩阵。将原始混淆矩阵的每个元素除以对应行的元素和，得到每个元素在其所在行的比例。

   - `conf_mx`：原始混淆矩阵。
   - `row_sums`：每一行的元素和。
   - `norm_conf_mx`：归一化的混淆矩阵。

归一化的混淆矩阵可以帮助我们更直观地理解分类器在各个类别上的性能。归一化后的矩阵中的每个元素表示分类器将样本预测为某个类别的比例。通过观察归一化混淆矩阵，可以发现分类器在不同类别上的预测偏差或错误情况，进而对模型进行改进或调整。

```py
np.fill_diagonal(norm_conf_mx, 0)
plt.matshow(norm_conf_mx, cmap=plt.cm.gray)
save_fig("confusion_matrix_errors_plot", tight_layout=False)
plt.show()
```

这段代码用于绘制归一化混淆矩阵的图像，并保存为文件。

具体解释如下：

1. `np.fill_diagonal(norm_conf_mx, 0)`：这行代码将归一化混淆矩阵的对角线元素（代表正确分类的样本）设置为0。这样做是为了突出显示分类器在不同类别上的错误。

1. `plt.matshow(norm_conf_mx, cmap=plt.cm.gray)`：这行代码使用`matshow`函数绘制归一化混淆矩阵的图像。`norm_conf_mx`是归一化后的混淆矩阵，`cmap=plt.cm.gray`表示使用灰度颜色映射进行显示。

1. `save_fig("confusion_matrix_errors_plot", tight_layout=False)`：这行代码将绘制的图像保存为文件。`"confusion_matrix_errors_plot"`是保存文件的名称。

1. `plt.show()`：这行代码显示绘制的图像。

通过绘制归一化混淆矩阵的图像，可以直观地观察分类器在不同类别上的错误情况。对角线上的元素为0，表示正确分类的样本，而非对角线上的元素表示分类错误的样本。绘制的图像可以帮助我们发现分类器在哪些类别上容易混淆或出现错误，从而指导我们进一步改进分类器或关注特定类别的性能问题。

```py
cl_a, cl_b = 3, 5
X_aa = X_train[(y_train == cl_a) & (y_train_pred == cl_a)]
X_ab = X_train[(y_train == cl_a) & (y_train_pred == cl_b)]
X_ba = X_train[(y_train == cl_b) & (y_train_pred == cl_a)]
X_bb = X_train[(y_train == cl_b) & (y_train_pred == cl_b)]

plt.figure(figsize=(8,8))
plt.subplot(221); plot_digits(X_aa[:25], images_per_row=5)
plt.subplot(222); plot_digits(X_ab[:25], images_per_row=5)
plt.subplot(223); plot_digits(X_ba[:25], images_per_row=5)
plt.subplot(224); plot_digits(X_bb[:25], images_per_row=5)
save_fig("error_analysis_digits_plot")
plt.show()
```

这段代码用于进行错误分析，将被错误分类的样本可视化并保存为图像。

具体解释如下：

1. `cl_a, cl_b = 3, 5`：这行代码定义了两个类别`cl_a`和`cl_b`，用于进行错误分类的样本分析。

1. `X_aa = X_train[(y_train == cl_a) & (y_train_pred == cl_a)]`：这行代码选取被正确分类为类别`cl_a`的样本，保存在`X_aa`中。

1. `X_ab = X_train[(y_train == cl_a) & (y_train_pred == cl_b)]`：这行代码选取被错误分类为类别`cl_b`的样本，保存在`X_ab`中。

1. `X_ba = X_train[(y_train == cl_b) & (y_train_pred == cl_a)]`：这行代码选取被错误分类为类别`cl_a`的样本，保存在`X_ba`中。

1. `X_bb = X_train[(y_train == cl_b) & (y_train_pred == cl_b)]`：这行代码选取被正确分类为类别`cl_b`的样本，保存在`X_bb`中。

1. `plt.figure(figsize=(8,8))`：这行代码创建一个图像窗口，设置其大小为8x8。

1. `plt.subplot(221); plot_digits(X_aa[:25], images_per_row=5)`：这行代码在图像窗口中创建一个子图，并调用`plot_digits`函数绘制被正确分类为类别`cl_a`的样本。`X_aa[:25]`表示选取前25个样本进行展示，`images_per_row=5`表示每行显示5张图像。

1. `plt.subplot(222); plot_digits(X_ab[:25], images_per_row=5)`：这行代码在图像窗口中创建第二个子图，并调用`plot_digits`函数绘制被错误分类为类别`cl_b`的样本。

1. `plt.subplot(223); plot_digits(X_ba[:25], images_per_row=5)`：这行代码在图像窗口中创建第三个子图，并调用`plot_digits`函数绘制被错误分类为类别`cl_a`的样本。

1. `plt.subplot(224); plot_digits(X_bb[:25], images_per_row=5)`：这行代码在图像窗口中创建第四个子图，并调用`plot_digits`函数绘制被正确分类为类别`cl_b`的样本。

1. `save_fig("error_analysis_digits_plot")`：这行代码将图像窗口中的图像保存为文件。文件名为"error_analysis_digits_plot"。

1. `plt.show()`：这行代码显示绘制的图像。

通过这段代码，我们可以可视化被错误分类的样本，分析分类器在不同类别上的错误情况。四个子图分别显示了被正确分类为`cl_a`、被错误分类为`cl_b`、被错误分类为`cl_a`以及被正确分类为`cl_b`的样本。通过观察这些样本，可以帮助我们理解分类器的错误模式，并有针对性地改进分类器的性能。



## Multilabel Classification

```py
from sklearn.neighbors import KNeighborsClassifier

y_train_large = (y_train >= 7)
y_train_odd = (y_train % 2 == 1)
y_multilabel = np.c_[y_train_large, y_train_odd]

knn_clf = KNeighborsClassifier()
knn_clf.fit(X_train, y_multilabel)
```

这段代码使用`sklearn.neighbors`模块中的`KNeighborsClassifier`类来构建一个K最近邻分类器，并将其应用于多标签分类任务。

具体解释如下：

1. `y_train_large = (y_train >= 7)`：这行代码创建一个布尔数组`y_train_large`，其中元素为True表示对应的训练样本的标签大于等于7，反之为False。

1. `y_train_odd = (y_train % 2 == 1)`：这行代码创建一个布尔数组`y_train_odd`，其中元素为True表示对应的训练样本的标签为奇数，反之为False。

1. `y_multilabel = np.c_[y_train_large, y_train_odd]`：这行代码使用`np.c_`函数将`y_train_large`和`y_train_odd`按列合并，得到一个二维数组`y_multilabel`，其中每一列对应一个标签。

1. `knn_clf = KNeighborsClassifier()`：这行代码创建了一个K最近邻分类器的实例`knn_clf`。

1. `knn_clf.fit(X_train, y_multilabel)`：这行代码使用训练数据`X_train`和多标签的目标值`y_multilabel`来训练K最近邻分类器。该分类器将根据输入样本的特征进行最近邻搜索，并根据邻居样本的标签进行多标签分类。

通过这段代码，我们可以构建一个K最近邻分类器，并将其应用于多标签分类任务。多标签分类任务是指每个样本可以属于多个类别，而不仅仅属于一个类别。在这个例子中，我们将训练样本的标签拆分为两个二进制标签，一个表示标签大于等于7，另一个表示标签是否为奇数。然后使用K最近邻分类器进行训练，以便进行多标签分类预测。

```
knn_clf.predict([some_digit])
```

```py
y_train_knn_pred = cross_val_predict(knn_clf, X_train, y_multilabel, cv=3)
f1_score(y_multilabel, y_train_knn_pred, average="macro")
```



## Multioutput Classification

```py
noise = np.random.randint(0, 100, (len(X_train), 784))
X_train_mod = X_train + noise
noise = np.random.randint(0, 100, (len(X_test), 784))
X_test_mod = X_test + noise
y_train_mod = X_train
y_test_mod = X_test
```

这段代码用于创建带有噪声的训练和测试数据集，并创建目标值数据集，其中目标值与输入数据相同。

具体解释如下：

1. `noise = np.random.randint(0, 100, (len(X_train), 784))`：这行代码生成一个形状为`(len(X_train), 784)`的随机整数数组`noise`，范围在0到100之间。该数组将用作训练数据集的噪声。

1. `X_train_mod = X_train + noise`：这行代码将噪声数组`noise`添加到训练数据集`X_train`中，得到带有噪声的训练数据集`X_train_mod`。

1. `noise = np.random.randint(0, 100, (len(X_test), 784))`：这行代码生成一个形状为`(len(X_test), 784)`的随机整数数组`noise`，范围在0到100之间。该数组将用作测试数据集的噪声。

1. `X_test_mod = X_test + noise`：这行代码将噪声数组`noise`添加到测试数据集`X_test`中，得到带有噪声的测试数据集`X_test_mod`。

1. `y_train_mod = X_train`：这行代码将训练数据集`X_train`作为目标值数据集`y_train_mod`，即目标值与输入数据相同。

1. `y_test_mod = X_test`：这行代码将测试数据集`X_test`作为目标值数据集`y_test_mod`，即目标值与输入数据相同。

通过这段代码，我们可以创建带有随机噪声的训练和测试数据集，并创建与输入数据相同的目标值数据集。这可以用于模拟在现实情况下输入数据存在噪声的情况，以便进行模型训练和评估。

```py
some_index = 0
plt.subplot(121); plot_digit(X_test_mod[some_index])
plt.subplot(122); plot_digit(y_test_mod[some_index])
save_fig("noisy_digit_example_plot")
plt.show()
```

这段代码用于可视化带有噪声的数字示例。

具体解释如下：

1. `some_index = 0`：这行代码定义一个索引`some_index`，表示要可视化的示例在测试数据集中的索引位置。

1. `plt.subplot(121); plot_digit(X_test_mod[some_index])`：这行代码在图像窗口中创建一个子图，并调用`plot_digit`函数绘制带有噪声的输入数据`X_test_mod[some_index]`。子图位于左侧，编号为121。

1. `plt.subplot(122); plot_digit(y_test_mod[some_index])`：这行代码在图像窗口中创建一个子图，并调用`plot_digit`函数绘制目标值数据`y_test_mod[some_index]`，即与输入数据相同的目标值。子图位于右侧，编号为122。

1. `save_fig("noisy_digit_example_plot")`：这行代码将图像窗口中的图像保存为文件。文件名为"noisy_digit_example_plot"。

1. `plt.show()`：这行代码显示绘制的图像。

通过这段代码，我们可以选择一个索引，然后将带有噪声的输入数据和对应的目标值数据可视化。左侧的子图显示了带有噪声的输入数据，右侧的子图显示了与输入数据相同的目标值数据。这有助于我们观察和比较噪声对输入数据和目标值的影响。

```py
knn_clf.fit(X_train_mod, y_train_mod)
clean_digit = knn_clf.predict([X_test_mod[some_index]])
plot_digit(clean_digit)
save_fig("cleaned_digit_example_plot")
```

这段代码使用带有噪声的训练数据集`X_train_mod`和目标值数据集`y_train_mod`来训练K最近邻分类器`knn_clf`。

接下来，代码使用训练好的分类器对带有噪声的测试数据`X_test_mod[some_index]`进行预测，并将预测结果存储在`clean_digit`变量中。

然后，代码调用`plot_digit`函数来绘制经过清理后的数字图像`clean_digit`。

最后，代码使用`save_fig`函数将清理后的数字图像保存为文件，文件名为"cleaned_digit_example_plot"。
