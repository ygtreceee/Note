# 02 _end_to_end_machine_learning_project

**Welcome to Machine Learning!**

This project requires Python 3.7 or above:

```py
import sys

assert sys.version_info >= (3, 7)
```

It also requires Scikit-Learn ≥ 1.0.1:

```py
from packaging import version
import sklearn

assert version.parse(sklearn.__version__) >= version.parse("1.0.1")
```

## Get the Data

#### Download the Data

```py
from pathlib import Path
import pandas as pd
import tarfile
import urllib.request

def load_housing_data():
    tarball_path = Path("datasets/housing.tgz")                           # 实例化Path对象
    if not tarball_path.is_file():
        Path("datasets").mkdir(parents=True, exist_ok=True)               # 创建目录
        url = "https://github.com/ageron/data/raw/main/housing.tgz"
        urllib.request.urlretrieve(url, tarball_path)                     # 下载tgz文件到本地
        with tarfile.open(tarball_path) as housing_tarball:
            housing_tarball.extractall(path="datasets")
    return pd.read_csv(Path("datasets/housing/housing.csv"))

housing = load_housing_data()
```

1. `Path()` 是 Python 标准库中的 `pathlib` 模块中的一个类，用于创建、操作和访问文件路径。

   `Path()` 类提供了一种面向对象的方式来处理文件和目录路径，它可以代替传统的字符串路径操作，更加简洁和可读。通过实例化 `Path` 对象，你可以执行各种文件路径相关的操作，如创建、删除、重命名、遍历目录、获取文件属性等。

   下面是一些 `Path()` 类的常用方法和属性：

   - `Path()`：实例化 `Path` 对象，接受一个字符串参数作为文件路径。
   - `.resolve()`：返回规范化的绝对路径。
   - `.exists()`：检查路径是否存在。
   - `.is_file()`：检查路径是否为文件。
   - `.is_dir()`：检查路径是否为目录。
   - `.name`：获取路径的文件名部分。
   - `.parent`：获取路径的父目录。
   - `.suffix`：获取路径的文件扩展名。
   - `.suffixes`：获取路径的所有文件扩展名（如果有多个）。
   - `.stem`：获取路径的文件名（不包含扩展名）。
   - `.parts`：获取路径的各个组成部分。
   - `.joinpath(*args)`：连接多个路径部分生成新的路径。
   - `.mkdir(mode=0o777, parents=False, exist_ok=False)`：创建目录。
   - `.rename(new)`：重命名路径。
   - `.unlink()`：删除文件。
   - `.rmdir()`：删除目录。
   - `.glob(pattern)`：返回匹配指定模式的所有路径。
   - `.iterdir()`：返回目录下的所有路径。
   - `.stat()`：获取路径的文件属性。
   - `.chmod(mode)`：修改路径的权限模式。
   - `.touch()`：创建一个空文件。

   通过使用 `Path()` 类，你可以以更直观和方便的方式操作文件路径，而不需要手动处理字符串路径的各种细节。它提供了一种更优雅和面向对象的方式来处理文件和目录的操作，使得你的代码更加可读和可维护。

2. `Path.mkdir()` 方法用于在文件系统中创建目录。

   方法的语法如下：

   ```python
   mkdir(mode=0o777, parents=False, exist_ok=False)
   ```

   参数说明：

   - `mode`：可选参数，用于设置目录的权限模式，默认为 `0o777`。
   - `parents`：可选参数，如果设置为 `True`，则会自动创建所有必需的中间目录，默认为 `False`。
   - `exist_ok`：可选参数，如果设置为 `True`，则在目录已经存在的情况下不会引发异常，默认为 `False`。

   下面是一个示例，演示如何使用 `mkdir()` 方法创建目录：

   ```python
   from pathlib import Path
   
   # 创建单层目录
   path = Path("path/to/directory")
   path.mkdir()
   
   # 创建多层目录
   path = Path("path/to/multiple/directories")
   path.mkdir(parents=True)
   
   # 创建目录并设置权限模式
   path = Path("path/to/directory")
   path.mkdir(mode=0o755)
   
   # 创建目录，如果目录已经存在，则不做任何操作
   path = Path("path/to/directory")
   path.mkdir(exist_ok=True)
   ```

   在上述示例中，我们首先通过 `Path()` 创建一个 `Path` 对象，然后调用 `.mkdir()` 方法来创建目录。如果路径中的某个目录不存在，使用 `mkdir()` 方法将会创建该目录。如果目录已经存在，则默认情况下会引发异常，但你可以通过将 `exist_ok` 参数设置为 `True` 来避免异常的发生。

   如果需要创建多层目录，你可以将 `parents` 参数设置为 `True`，它会自动创建所有必需的中间目录。

   你还可以通过 `mode` 参数设置目录的权限模式，默认为 `0o777`。这个权限模式会在创建目录时应用于操作系统的文件权限。

   请注意，在使用 `mkdir()` 方法创建目录时，请确保你有足够的权限执行该操作。

3. `urllib.request.urlretrieve()`函数是Python标准库中`urllib.request`模块的一部分。它用于从指定的URL下载文件到本地。

   该函数的语法如下：

   ```python
   urllib.request.urlretrieve(url, filename=None, reporthook=None, data=None)
   ```

   参数说明：

   - `url`：要下载文件的URL地址。
   - `filename`：可选参数，指定要保存文件的本地路径。如果未提供此参数，将会自动生成一个临时文件名来保存下载的内容。
   - `reporthook`：可选参数，用于指定一个回调函数，用于在下载过程中显示进度信息。
   - `data`：可选参数，如果提供了该参数，它将会作为请求的数据发送给服务器。

   下面是一个示例，演示如何使用`urllib.request.urlretrieve()`函数下载文件：

   ```python
   import urllib.request
   
   url = 'https://example.com/file.txt'
   filename = 'downloaded_file.txt'
   
   urllib.request.urlretrieve(url, filename)
   ```

   在上述示例中，`urlretrieve()`函数会从指定的URL下载文件，并将文件保存到指定的本地路径。如果未提供文件名，将会生成一个临时文件名。

   你还可以通过提供一个回调函数来显示下载进度。回调函数会在下载过程中被调用，并接收当前下载的块数和块大小作为参数，你可以在回调函数中自定义进度显示的方式。

   请注意，`urlretrieve()`函数在下载大文件时可能会导致程序阻塞，因为它会等待整个文件下载完成后才会返回。如果你需要更高级的下载功能，例如异步下载或断点续传，你可能需要使用更为强大的第三方库，如`requests`或`wget`。

4. `tarfile.open()` 函数是 `tarfile` 模块中的一个方法，用于打开和操作 TAR 文件（tarball）。

   方法的语法如下：

   ```python
   open(name=None, mode='r', fileobj=None, bufsize=10240, **kwargs)
   ```

   参数说明：

   - `name`：可选参数，指定要打开的 TAR 文件的文件名或路径。
   - `mode`：可选参数，指定打开 TAR 文件的模式。默认为 `'r'`，表示只读模式。其他常用的模式包括 `'w'`（写入模式）和 `'x'`（创建新的 TAR 文件）。
   - `fileobj`：可选参数，指定一个文件对象来代替文件名进行操作。如果提供了 `fileobj`，则会忽略 `name` 参数。
   - `bufsize`：可选参数，指定缓冲区大小，默认为 10240 字节（10KB）。

   下面是一个示例，演示如何使用 `tarfile.open()` 函数打开 TAR 文件：

   ```python
   import tarfile
   
   tar_path = "path/to/archive.tar"
   
   with tarfile.open(tar_path, 'r') as tar:
       # 对 TAR 文件进行操作
       # ...
   ```

   在上述示例中，我们使用 `tarfile.open()` 打开 TAR 文件，并使用 `'r'` 模式以只读方式进行操作。然后，我们可以在 `with` 语句块内对 TAR 文件进行各种操作，例如读取文件、提取文件等。

   根据指定的模式，`tarfile.open()` 可以在文件系统中打开现有的 TAR 文件进行读取（`'r'` 模式），创建新的 TAR 文件并将文件添加到其中（`'w'` 模式），或者创建新的 TAR 文件并只允许写入新的文件（`'x'` 模式）。

   你可以根据具体的需求选择适当的模式，并根据需要进行各种操作，如读取文件内容、提取文件、添加文件到 TAR 文件等。

   请注意，对于压缩的 TAR 文件（.tar.gz 或 .tgz），你可以使用 `tarfile.open()` 函数打开并进行操作。`tarfile` 模块自动处理压缩和解压缩。当你打开一个压缩的 TAR 文件时，可以像操作普通的 TAR 文件一样操作其中的内容。

5. `tarfile.extractall()` 是 `tarfile` 模块中 `TarFile` 类的一个方法，用于从 TAR 文件中提取（解压缩）所有的文件和目录。

   方法的语法如下：

   ```python
   extractall(path=".", members=None, *, numeric_owner=False)
   ```

   参数说明：

   - `path`：可选参数，指定要提取文件的目标路径。默认为当前工作目录。
   - `members`：可选参数，用于指定要提取的特定文件或目录。它应该是一个字符串列表，每个字符串表示 TAR 文件中的一个文件或目录。如果未提供此参数，则会提取所有文件和目录。
   - `numeric_owner`：可选参数，指定是否使用数字用户 ID 和组 ID 进行提取。默认为 `False`，表示使用用户和组的名称。

   下面是一个示例，演示如何使用 `extractall()` 方法从 TAR 文件中提取所有内容：

   ```python
   import tarfile
   
   tar_path = "path/to/archive.tar"
   target_path = "path/to/extract"
   
   with tarfile.open(tar_path, 'r') as tar:
       tar.extractall(target_path)
   ```

   在上述示例中，我们首先通过 `tarfile.open()` 打开 TAR 文件，并使用 `'r'` 模式读取文件。然后，我们使用 `extractall()` 方法将 TAR 文件中的所有内容提取到指定的目标路径。如果未提供 `path` 参数，则会提取到当前工作目录。

   你还可以通过指定 `members` 参数来提取特定的文件或目录。`members` 应该是一个字符串列表，每个字符串表示 TAR 文件中的一个文件或目录。

   `extractall()` 方法还接受 `numeric_owner` 参数，用于指定是否使用数字用户 ID 和组 ID 进行提取。默认情况下，它会使用用户和组的名称进行提取。如果你希望使用数字 ID 进行提取，可以将 `numeric_owner` 参数设置为 `True`。

   请注意，在使用 `extractall()` 方法提取文件时，请确保你有足够的权限执行该操作，并且只从受信任的来源提取文件。此外，请注意 TAR 文件中可能存在恶意文件的风险。在提取文件之前，建议仔细检查和验证 TAR 文件的内容，以确保安全性。

6. `pandas.read_csv()` 函数是 Pandas 库中的一个方法，用于从 CSV（逗号分隔值）文件中读取数据并创建一个 DataFrame 对象。

   方法的语法如下：

   ```python
   pandas.read_csv(filepath_or_buffer, sep=',', delimiter=None, header='infer', names=None, index_col=None, usecols=None)
   ```

   参数说明：

   - `filepath_or_buffer`：必需参数，指定要读取的 CSV 文件的路径（包括文件名）或 URL，或者是一个类文件对象（如打开的文件）。
   - `sep`：可选参数，指定字段之间的分隔符，默认为逗号 `,`。
   - `delimiter`：可选参数，指定字段之间的定界符。如果指定了 `delimiter`，则会覆盖 `sep` 参数。
   - `header`：可选参数，指定行号用作列名的行，默认为 `'infer'`，表示自动推断列名。可以指定一个整数值作为列名所在的行号，或者指定一个行号列表作为多级列名。
   - `names`：可选参数，用于指定自定义的列名。如果指定了 `names`，则会覆盖 `header` 参数。
   - `index_col`：可选参数，用于指定作为索引的列。可以指定一个整数值表示索引列的位置，或者指定列名作为索引列。
   - `usecols`：可选参数，用于指定要读取的列。可以指定一个整数值列表表示要读取的列的位置，或者指定一个列名列表表示要读取的列。

   下面是一个示例，演示如何使用 `read_csv()` 方法从 CSV 文件中读取数据并创建 DataFrame：

   ```python
   import pandas as pd
   
   csv_path = "path/to/data.csv"
   
   df = pd.read_csv(csv_path)
   ```

   在上述示例中，我们使用 `read_csv()` 方法读取指定路径的 CSV 文件，并将其存储在一个名为 `df` 的 DataFrame 对象中。

   `read_csv()` 方法会根据指定的参数解析 CSV 文件，并将其转换为 DataFrame 对象。它可以自动推断列名、处理缺失值、选择特定的列、指定自定义的列名等。

   你可以根据需要使用不同的参数来配置读取过程，例如指定分隔符、定界符，指定列名所在的行，选择特定的列进行读取，以及将某列作为索引等。

   读取的 CSV 数据将以 DataFrame 对象的形式存储在变量中，你可以使用 Pandas 提供的各种功能和方法来处理和分析数据。



#### Take a Quick Look at the Data Structure

```py
housing.head()
```

1. DataFrame 对象的 `head()` 方法用于返回 DataFrame 的前几行数据，默认返回前 5 行。

   方法的语法如下：

   ```python
   DataFrame.head(n=5)
   ```

   参数说明：

   - `n`：可选参数，指定要返回的行数。默认为 5。

   下面是一个示例，演示如何使用 `head()` 方法查看 DataFrame 的前几行数据：

   ```python
   import pandas as pd
   
   # 创建一个示例 DataFrame
   data = {'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
           'Age': [25, 30, 35, 40, 45],
           'City': ['New York', 'London', 'Paris', 'Tokyo', 'Sydney']}
   df = pd.DataFrame(data)
   
   # 使用 head() 方法查看前几行数据
   print(df.head())
   ```

   输出结果：

   ```
         Name  Age      City
   0    Alice   25  New York
   1      Bob   30    London
   2  Charlie   35     Paris
   3    David   40     Tokyo
   4      Eve   45    Sydney
   ```

   在上述示例中，我们首先创建了一个示例的 DataFrame 对象 `df`。然后，我们使用 `head()` 方法来查看 DataFrame 的前 5 行数据，默认情况下返回前 5 行。输出结果显示了 DataFrame 的前几行数据，包括列名和对应的值。

   你可以通过指定 `n` 参数来返回不同数量的行数。例如，如果你想要返回前 3 行数据，可以将 `n` 参数设置为 3：

   ```python
   print(df.head(n=3))
   ```

   输出结果：

   ```
         Name  Age      City
   0    Alice   25  New York
   1      Bob   30    London
   2  Charlie   35     Paris
   ```

   使用 `head()` 方法可以快速查看 DataFrame 的开头几行数据，帮助你了解数据的结构和内容。如果你想要查看 DataFrame 的后几行数据，可以使用 `tail()` 方法，其用法类似于 `head()` 方法，但返回 DataFrame 的最后几行数据。



```py
housing.info()
```

1. DataFrame 对象的 `info()` 方法用于提供关于 DataFrame 的基本信息摘要，包括列名、数据类型、非空值数量等。

   方法的语法如下：

   ```python
   DataFrame.info(verbose=True, null_counts=False)
   ```

   参数说明：

   - `verbose`：可选参数，控制详细程度。当设置为 `True` 时，会显示每列的数据类型和非空值数量。当设置为 `False` 时，只显示列的总数和每列的名称。默认为 `True`。
   - `null_counts`：可选参数，控制是否显示每列的非空值数量。当设置为 `True` 时，会显示每列的非空值数量。当设置为 `False` 时，不显示非空值数量。默认为 `False`。

   下面是一个示例，演示如何使用 `info()` 方法查看 DataFrame 的基本信息摘要：

   ```python
   import pandas as pd
   
   # 创建一个示例 DataFrame
   data = {'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
           'Age': [25, 30, 35, 40, 45],
           'City': ['New York', 'London', 'Paris', 'Tokyo', 'Sydney']}
   df = pd.DataFrame(data)
   
   # 使用 info() 方法查看 DataFrame 的基本信息
   df.info()
   ```

   输出结果：

   ```
   <class 'pandas.core.frame.DataFrame'>
   RangeIndex: 5 entries, 0 to 4
   Data columns (total 3 columns):
    #   Column  Non-Null Count  Dtype 
   ---  ------  --------------  ----- 
    0   Name    5 non-null      object
    1   Age     5 non-null      int64 
    2   City    5 non-null      object
   dtypes: int64(1), object(2)
   memory usage: 248.0+ bytes
   ```

   在上述示例中，我们创建了一个示例的 DataFrame 对象 `df`。然后，我们使用 `info()` 方法来查看 DataFrame 的基本信息摘要。输出结果提供了以下信息：

   - `class 'pandas.core.frame.DataFrame'`：表示对象的类型为 DataFrame。
   - `RangeIndex: 5 entries, 0 to 4`：表示 DataFrame 的索引范围，从 0 到 4。
   - `Data columns (total 3 columns):`：表示 DataFrame 共有 3 列。
   - `Column  Non-Null Count  Dtype`：表示每列的名称、非空值的数量和数据类型。
   - `dtypes: int64(1), object(2)`：表示每列的数据类型。
   - `memory usage: 248.0+ bytes`：表示 DataFrame 占用的内存大小。

   通过 `info()` 方法，你可以获得 DataFrame 的基本信息，包括列名、数据类型和非空值数量等，这有助于了解 DataFrame 中的数据。此外，还可以通过查看内存使用情况来评估 DataFrame 对系统资源的占用情况。



```py
housing["ocean_proximity"].value_counts()
```

1. `value_counts()` 函数是 Pandas 库中的一个方法，用于计算 DataFrame 列中每个唯一值的出现次数。

   方法的语法如下：

   ```python
   Series.value_counts(normalize=False, sort=True, ascending=False, bins=None, dropna=True)
   ```

   参数说明：

   - `normalize`：可选参数，控制是否返回每个唯一值的频率而不是计数。当设置为 `True` 时，返回的结果为每个唯一值的频率。默认为 `False`。
   - `sort`：可选参数，控制是否按计数值对结果进行排序。当设置为 `True` 时，结果按计数值降序排列。当设置为 `False` 时，结果不排序。默认为 `True`。
   - `ascending`：可选参数，控制排序顺序。当设置为 `True` 时，结果按计数值升序排列。当设置为 `False` 时，结果按计数值降序排列。默认为 `False`。
   - `bins`：可选参数，用于将连续值离散化为指定数量的区间。仅适用于数值列。默认为 `None`，表示不离散化。
   - `dropna`：可选参数，控制是否排除缺失值（NaN）计数。当设置为 `True` 时，不计算缺失值的计数。当设置为 `False` 时，包括缺失值在内的所有值计数。默认为 `True`。

   `value_counts()` 方法通常应用于 Series 对象，也可以在 DataFrame 中的某个列上使用，返回的是该列中每个唯一值的计数结果。如果要对整个 DataFrame 进行计数，可以使用 `value_counts()` 方法的链式调用，例如 `df['column'].value_counts()`。

   下面是一个示例，演示如何使用 `value_counts()` 方法统计 DataFrame 列中每个唯一值的计数：

   ```python
   import pandas as pd
   
   # 创建一个示例 DataFrame
   data = {'Name': ['Alice', 'Bob', 'Charlie', 'Bob', 'David', 'Eve', 'Alice'],
           'Age': [25, 30, 35, 30, 40, 45, 25]}
   df = pd.DataFrame(data)
   
   # 对 'Name' 列使用 value_counts() 方法进行计数
   name_counts = df['Name'].value_counts()
   
   print(name_counts)
   ```

   输出结果：

   ```
   Alice      2
   Bob        2
   Charlie    1
   David      1
   Eve        1
   Name: Name, dtype: int64
   ```

   在上述示例中，我们创建了一个示例的 DataFrame 对象 `df`。然后，我们对 'Name' 列使用 `value_counts()` 方法进行计数。输出结果显示了 'Name' 列中每个唯一值的计数结果。例如，'Alice' 和 'Bob' 出现了两次，'Charlie'、'David' 和 'Eve' 分别出现了一次。

   你可以根据需要使用 `value_counts()` 方法的不同参数来进行计数结果的定制，例如计算频率而不是计数、排序计数结果等。

   `value_counts()` 方法是一个方便而强大的函数，可以帮助你快速了解列中每个唯一值的出现次数或频率，从而进行数据分析和处理。



```py
housing.describe()
```

1. `describe()` 函数是 Pandas 库中的一个方法，用于生成描述性统计信息摘要，包括计数、均值、标准差、最小值、25% 分位数、50% 分位数（中位数）、75% 分位数、最大值等。

   方法的语法如下：

   ```python
   DataFrame.describe(percentiles=None, include=None, exclude=None)
   ```

   参数说明：

   - `percentiles`：可选参数，指定要计算的分位数。可以传递一个列表，例如 `[0.25, 0.5, 0.75]`，表示计算 25%、50% 和 75% 分位数。默认为 `None`，表示计算所有分位数。
   - `include`：可选参数，指定要包含的数据类型。可以传递一个列表，例如 `['number', 'object']`，表示只包括数值类型和对象类型的列。默认为 `None`，表示包括所有数据类型的列。
   - `exclude`：可选参数，指定要排除的数据类型。可以传递一个列表，例如 `['category']`，表示排除类别类型的列。默认为 `None`，表示不排除任何数据类型的列。

   下面是一个示例，演示如何使用 `describe()` 方法生成 DataFrame 的描述性统计信息摘要：

   ```python
   import pandas as pd
   
   # 创建一个示例 DataFrame
   data = {'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
           'Age': [25, 30, 35, 40, 45],
           'Height': [165, 170, 175, 180, 185],
           'Weight': [60, 70, 80, 90, 100]}
   df = pd.DataFrame(data)
   
   # 使用 describe() 方法生成描述性统计信息摘要
   summary = df.describe()
   
   print(summary)
   ```

   输出结果：

   ```
                Age      Height      Weight
   count   5.000000    5.000000    5.000000
   mean   35.000000  175.000000   80.000000
   std     7.905694    7.905694   15.811388
   min    25.000000  165.000000   60.000000
   25%    30.000000  170.000000   70.000000
   50%    35.000000  175.000000   80.000000
   75%    40.000000  180.000000   90.000000
   max    45.000000  185.000000  100.000000
   ```

   在上述示例中，我们创建了一个示例的 DataFrame 对象 `df`。然后，我们使用 `describe()` 方法生成描述性统计信息摘要。输出结果提供了以下统计信息：

   - `count`：每列的非缺失值数量。
   - `mean`：每列的均值。
   - `std`：每列的标准差。
   - `min`：每列的最小值。
   - `25%`：每列的第 25% 分位数。
   - `50%`：每列的中位数（第 50% 分位数）。
   - `75%`：每列的第 75% 分位数。
   - `max`：每列的最大值。

   通过 `describe()` 方法，你可以快速获取 DataFrame 的描述性统计信息摘要，有助于了解数据的分布、集中趋势和离散程度。你还可以通过指定不同的参数来定制生成的统计信息，例如计算特定分位数、只包括特定数据类型的列等。



The following cell is not shown either in the book. It creates the `images/end_to_end_project` folder (if it doesn't already exist), and it defines the `save_fig()` function which is used through this notebook to save the figures in high-res for the book.

```py
# extra code – code to save the figures as high-res PNGs for the book

IMAGES_PATH = Path() / "images" / "end_to_end_project"
IMAGES_PATH.mkdir(parents=True, exist_ok=True)

def save_fig(fig_id, tight_layout=True, fig_extension="png", resolution=300):
    path = IMAGES_PATH / f"{fig_id}.{fig_extension}"                       # path最后是f"{文件名}.{扩展名}"
    if tight_layout:                                                       # 调整布局
        plt.tight_layout()
    plt.savefig(path, format=fig_extension, dpi=resolution)                # 将当前图形保存为图像文件
```

```py
import matplotlib.pyplot as plt

# extra code – the next 5 lines define the default font sizes  设置全局绘图参数
plt.rc('font', size=14)
plt.rc('axes', labelsize=14, titlesize=14)
plt.rc('legend', fontsize=14)
plt.rc('xtick', labelsize=10)
plt.rc('ytick', labelsize=10)

housing.hist(bins=50, figsize=(12, 8))
save_fig("attribute_histogram_plots")  # extra code
plt.show()
```

1. `tight_layout()` 是 Matplotlib 库中的一个函数，用于自动调整子图或图形的布局，以确保它们适合在绘图区域内正确显示，避免重叠或截断。

   当在 Matplotlib 中创建包含多个子图或图形的图像时，有时子图之间的标签、标题、刻度标签等元素可能会重叠，或者图像的边缘被截断。这时可以使用 `tight_layout()` 函数自动调整布局，使得图像在显示时更加清晰和美观。

   `tight_layout()` 函数没有参数，直接在绘图之后调用即可。它会自动计算和调整各个子图或图形的位置和大小，以便它们适合在绘图区域内显示。

   下面是一个示例，演示如何使用 `tight_layout()` 函数调整子图的布局：

   ```python
   import matplotlib.pyplot as plt
   
   # 创建两个子图
   fig, axes = plt.subplots(2, 2)
   
   # 在子图中绘制内容（省略绘图代码）
   
   # 调用 tight_layout() 调整布局
   plt.tight_layout()
   
   # 显示图像
   plt.show()
   ```

   在上述示例中，我们创建了一个包含 2x2 子图的图像，使用 `subplots()` 函数创建了 `fig` 和 `axes` 对象。然后，在每个子图中绘制了内容（省略绘图代码）。最后，调用 `tight_layout()` 函数自动调整子图的布局。

   调用 `tight_layout()` 函数后，Matplotlib 会自动计算和调整子图的位置和大小，使得它们适合在绘图区域内显示，避免了重叠或截断的问题。最后，通过 `plt.show()` 显示图像。

   使用 `tight_layout()` 函数可以提高绘图的可视化效果，确保图像的各个元素能够正确显示，从而更好地传达数据和结果。

   注意：在实际使用中，可能会根据具体情况需要对 `tight_layout()` 函数的调用位置进行调整，以便在调整布局后的子图或图形上进行其他绘图操作。

2. `tight_layout()` 是 Matplotlib 库中的一个函数，用于自动调整子图或图形的布局，以确保它们适合在绘图区域内正确显示，避免重叠或截断。

   当在 Matplotlib 中创建包含多个子图或图形的图像时，有时子图之间的标签、标题、刻度标签等元素可能会重叠，或者图像的边缘被截断。这时可以使用 `tight_layout()` 函数自动调整布局，使得图像在显示时更加清晰和美观。

   `tight_layout()` 函数没有参数，直接在绘图之后调用即可。它会自动计算和调整各个子图或图形的位置和大小，以便它们适合在绘图区域内显示。

   下面是一个示例，演示如何使用 `tight_layout()` 函数调整子图的布局：

   ```python
   import matplotlib.pyplot as plt
   
   # 创建两个子图
   fig, axes = plt.subplots(2, 2)
   
   # 在子图中绘制内容（省略绘图代码）
   
   # 调用 tight_layout() 调整布局
   plt.tight_layout()
   
   # 显示图像
   plt.show()
   ```

   在上述示例中，我们创建了一个包含 2x2 子图的图像，使用 `subplots()` 函数创建了 `fig` 和 `axes` 对象。然后，在每个子图中绘制了内容（省略绘图代码）。最后，调用 `tight_layout()` 函数自动调整子图的布局。

   调用 `tight_layout()` 函数后，Matplotlib 会自动计算和调整子图的位置和大小，使得它们适合在绘图区域内显示，避免了重叠或截断的问题。最后，通过 `plt.show()` 显示图像。

   使用 `tight_layout()` 函数可以提高绘图的可视化效果，确保图像的各个元素能够正确显示，从而更好地传达数据和结果。

   注意：在实际使用中，可能会根据具体情况需要对 `tight_layout()` 函数的调用位置进行调整，以便在调整布局后的子图或图形上进行其他绘图操作。

3. `rc()` 函数是 Matplotlib 库中的一个函数，用于设置全局的绘图参数。通过调用该函数，你可以修改 Matplotlib 的默认参数，从而自定义绘图的外观和行为。

   `rc()` 函数的语法如下：

   ```python
   rc(group, **kwargs)
   ```

   参数说明：

   - `group`：表示参数组的名称。参数组是一组相关的参数，用于定义绘图的不同方面，如线条样式、颜色映射、字体设置等。常见的参数组包括 `'lines'`（线条样式）、`'axes'`（坐标轴设置）、`'font'`（字体设置）等。你可以参考 Matplotlib 的文档以了解所有可用的参数组。
   - `**kwargs`：用于指定参数组中的具体参数及其对应的值。你可以根据参数组的要求，传递不同的参数和值来定制绘图的外观和行为。

   下面是一个示例，演示如何使用 `rc()` 函数修改线条样式的默认参数：

   ```python
   import matplotlib.pyplot as plt
   
   # 修改线条样式的默认参数
   plt.rc('lines', linewidth=2, linestyle='--', color='red')
   
   # 绘制图形（省略绘图代码）
   
   # 显示图形
   plt.show()
   ```

   在上述示例中，我们通过调用 `rc()` 函数，将线条样式的默认参数进行了修改。具体地，我们使用 `'lines'` 参数组，并传递了三个键值对作为关键字参数：`linewidth=2`（线宽为2）、`linestyle='--'`（线型为虚线）和 `color='red'`（颜色为红色）。这样，在后续的绘图中，所有的线条都会采用这些默认参数。

   通过使用 `rc()` 函数，你可以全局地修改 Matplotlib 的默认参数，从而快速定制绘图的样式和行为。这对于在整个脚本或程序中保持一致的绘图风格非常有用。

   需要注意的是，`rc()` 函数通常在绘图之前调用，以确保修改的参数在绘图时生效。另外，你也可以将 `rc()` 函数的调用放在 `matplotlibrc` 配置文件中，以便在启动 Matplotlib 时自动加载并应用这些参数设置。

   要了解更多关于 `rc()` 函数可用的参数组和具体参数，请查阅 Matplotlib 的官方文档 https://matplotlib.org/ 

   除了官方网站，你还可以在 Matplotlib 的 GitHub 代码仓库上找到更多的文档和资源 https://github.com/matplotlib/matplotlib

4. `hist()` 是 Matplotlib 库中的一个函数，用于绘制直方图。直方图是一种常用的统计图形，用于展示数据的分布情况。通过调用 `hist()` 函数，你可以将数据集划分为多个区间（或称为“箱子”），并统计每个区间内元素的数量或频率，然后将结果用柱状图的形式进行可视化。

   `hist()` 函数的语法如下：

   ```python
   hist(x, bins=None, range=None, density=False, weights=None, cumulative=False,
        bottom=None, histtype='bar', align='mid', orientation='vertical',
        rwidth=None, log=False, color=None, label=None, stacked=False,
        normed=None, *, data=None, **kwargs)
   ```

   参数说明：

   - `x`：要绘制直方图的数据。可以是一维数组、列表或其他序列。
   - `bins`：可选参数，指定直方图的区间个数或边界。可以是整数、序列或字符串。默认为 `None`，表示使用自动确定的合适区间个数。
   - `range`：可选参数，指定直方图的取值范围。默认为 `None`，表示使用数据的最小值和最大值作为范围。
   - `density`：可选参数，指定是否将直方图归一化为概率密度。默认为 `False`，表示直方图的值为样本数量。
   - `weights`：可选参数，指定每个数据点的权重。默认为 `None`，表示所有数据点的权重相等。
   - `cumulative`：可选参数，指定是否绘制累积直方图。默认为 `False`，表示绘制普通直方图。
   - 其他参数：你还可以使用其他参数来控制直方图的外观和样式，例如颜色、标签、柱状图类型、柱子宽度等。

   下面是一个示例，演示如何使用 `hist()` 函数绘制直方图：

   ```python
   import matplotlib.pyplot as plt
   import numpy as np
   
   # 生成随机数据
   data = np.random.randn(1000)
   
   # 绘制直方图
   plt.hist(data, bins=20, color='steelblue', edgecolor='black')
   
   # 显示图形
   plt.show()
   ```

   在上述示例中，我们首先使用 `numpy` 生成了一个包含 1000 个随机数的一维数组 `data`。然后，通过调用 `hist()` 函数，将 `data` 数据绘制为直方图。我们指定了 `bins=20`，表示将数据分成 20 个区间，并以蓝色的柱形图显示直方图。最后，调用 `show()` 函数显示图形。

   通过使用 `hist()` 函数，你可以可视化数据的分布情况，了解数据的频率或概率密度分布。你可以根据需求调整参数，如区间个数、范围、归一化、柱状图的样式等，以满足特定的绘图需求。

5. `show()` 是 Matplotlib 库中的一个函数，用于显示绘制的图形窗口。当你完成了绘图的设置和配置后，调用 `show()` 函数将图形显示在屏幕上。

   `show()` 函数的语法如下：

   ```python
   show(*args, **kw)
   ```

   参数说明：

   - `*args` 和 `**kw`：可选参数，用于传递给底层的 GUI 框架。大多数情况下，你不需要显式地传递参数给 `show()` 函数。

   下面是一个示例，演示如何使用 `show()` 函数显示绘制的图形：

   ```python
   import matplotlib.pyplot as plt
   
   # 绘制图形（省略绘图代码）
   
   # 显示图形
   plt.show()
   ```

   在上述示例中，我们首先调用 Matplotlib 的绘图函数（如 `plot()`、`scatter()`、`hist()` 等）绘制了图形。然后，通过调用 `show()` 函数，将绘制的图形显示在屏幕上。注意，`show()` 函数通常是在所有绘图代码的最后一行调用。

   在图形窗口显示后，你可以与图形进行交互，例如放大、缩小、保存图像等操作。关闭图形窗口后，程序将继续执行后续的代码。

   需要注意的是，当使用 Jupyter Notebook 等交互式环境时，有时候不需要显式地调用 `show()` 函数，绘图会自动显示在输出单元格中。

   总之，`show()` 函数是 Matplotlib 中的重要函数，用于显示绘制的图形。它将图形窗口显示在屏幕上，使用户能够查看和与图形进行交互。





#### Create a Test Set

```py
import numpy as np

def shuffle_and_split_data(data, test_ratio):
    shuffled_indices = np.random.permutation(len(data))
    test_set_size = int(len(data) * test_ratio)
    test_indices = shuffled_indices[:test_set_size]
    train_indices = shuffled_indices[test_set_size:]
    return data.iloc[train_indices], data.iloc[test_indices]
```

```py
train_set, test_set = shuffle_and_split_data(housing, 0.2)
len(train_set)
```

```py
len(test_set)
```

1. `numpy.random.permutation()` 函数是 NumPy 库中的一个函数，用于对给定的序列或数组进行随机重排。它返回一个新的随机排列的数组，包含原始序列或数组中的所有元素，但顺序是随机的。

   `numpy.random.permutation()` 函数的语法如下：

   ```python
   numpy.random.permutation(x)
   ```

   参数说明：

   - `x`：要进行随机重排的序列或数组。可以是一维数组、列表或其他序列。

   下面是一个示例，演示如何使用 `numpy.random.permutation()` 函数进行随机重排：

   ```python
   import numpy as np
   
   # 创建一维数组
   arr = np.array([1, 2, 3, 4, 5])
   
   # 随机重排数组
   permuted_arr = np.random.permutation(arr)
   
   # 打印结果
   print("原始数组:", arr)
   print("随机重排后的数组:", permuted_arr)
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   原始数组: [1 2 3 4 5]
   随机重排后的数组: [5 1 4 3 2]
   ```

   在上述示例中，我们首先创建了一个一维数组 `arr`，包含元素 `[1, 2, 3, 4, 5]`。然后，通过调用 `numpy.random.permutation()` 函数，对数组进行随机重排，并将结果存储在 `permuted_arr` 中。最后，我们打印原始数组和随机重排后的数组，以观察结果。

   `numpy.random.permutation()` 函数对于数据的随机化和洗牌操作非常有用。你可以使用该函数来打乱数据集、随机选择样本或进行随机采样等操作。它在机器学习、数据分析和模拟实验等领域都有广泛的应用。

2. 如果将 `numpy.random.permutation()` 函数的参数传递为 `len()` 函数的结果，它将返回一个随机排列的整数数组，该数组的长度与给定的序列或数组的长度相同，但元素顺序是随机的。

   下面是一个示例，演示如何使用 `numpy.random.permutation()` 函数传递 `len()` 函数的结果作为参数：

   ```python
   import numpy as np
   
   # 创建一个列表
   lst = [1, 2, 3, 4, 5]
   
   # 使用 len() 获取列表长度，并将其传递给 permutation()
   permuted_lst = np.random.permutation(len(lst))
   
   # 打印结果
   print("原始列表:", lst)
   print("随机重排后的列表:", permuted_lst)
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   原始列表: [1, 2, 3, 4, 5]
   随机重排后的列表: [2 4 3 1 0]
   ```

   在上述示例中，我们首先创建了一个包含整数的列表 `lst`，其中包含了元素 `[1, 2, 3, 4, 5]`。然后，通过将 `len(lst)` 作为参数传递给 `numpy.random.permutation()` 函数，对列表进行随机重排。`len(lst)` 返回列表的长度，这样 `permutation()` 函数就知道要生成一个相同长度的随机排列数组。我们将结果存储在 `permuted_lst` 中，并打印原始列表和随机重排后的列表。

   使用 `numpy.random.permutation(len())` 的一个常见用途是对索引进行随机化，以便在数据集中进行随机采样或打乱数据的顺序。通过生成一个随机排列的索引数组，可以在后续操作中使用这些索引来获取随机样本或对数据进行重排。

3. `iloc` 是 Pandas 库中的一个函数，用于通过整数位置（索引）选择和访问数据框（DataFrame）或序列（Series）中的元素。它提供了一种基于位置的索引方式，与 `loc` 函数不同，`iloc` 使用的是基于零的整数位置，而不是标签或条件。

   `iloc` 函数的语法如下：

   对于数据框（DataFrame）：

   ```python
   dataframe.iloc[row_indexer, column_indexer]
   ```

   对于序列（Series）：

   ```python
   series.iloc[indexer]
   ```

   参数说明：

   - `row_indexer`：用于选择行的整数位置或布尔数组或切片（slice）。
   - `column_indexer`：（仅适用于数据框）用于选择列的整数位置或布尔数组或切片（slice）。
   - `indexer`：用于选择元素的整数位置或布尔数组或切片（slice）。

   下面是一些示例，演示如何使用 `iloc` 函数进行数据访问和选择：

   ```python
   import pandas as pd
   
   # 创建示例数据框
   df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'C': [7, 8, 9]})
   
   # 使用 iloc 选择单个元素
   element = df.iloc[0, 1]
   print("单个元素:", element)
   
   # 使用 iloc 选择多行和多列
   subset = df.iloc[0:2, 1:3]
   print("子集:")
   print(subset)
   
   # 使用 iloc 选择单列（作为 Series）
   column = df.iloc[:, 2]
   print("单列:")
   print(column)
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   单个元素: 4
   子集:
      B  C
   0  4  7
   1  5  8
   单列:
   0    7
   1    8
   2    9
   Name: C, dtype: int64
   ```

   在上述示例中，我们首先创建了一个示例数据框 `df`，包含了三列（A、B、C）的数据。然后，通过使用 `iloc` 函数，我们演示了几种用法：

   - 使用 `iloc` 选择单个元素：`df.iloc[0, 1]` 选择了第一行、第二列的元素，返回值为 4。
   - 使用 `iloc` 选择多行和多列：`df.iloc[0:2, 1:3]` 选择了前两行和第二、第三列的子集数据框。
   - 使用 `iloc` 选择单列（作为 Series）：`df.iloc[:, 2]` 选择了第三列数据作为一个序列对象。

   总之，`iloc` 函数是 Pandas 库中用于基于整数位置进行数据访问和选择的函数。它允许你根据整数位置选择数据框或序列中的元素、子集或列，并返回相应的结果。





To ensure that this notebook's outputs remain the same every time we run it, we need to set the random seed:

```py
np.random.seed(42)
```

Sadly, this won't guarantee that this notebook will output exactly the same results as in the book, since there are other possible sources of variation. The most important is the fact that algorithms get tweaked over time when libraries evolve. So please tolerate some minor differences: hopefully, most of the outputs should be the same, or at least in the right ballpark.

Note: another source of randomness is the order of Python sets: it is based on Python's `hash()` function, which is randomly "salted" when Python starts up (this started in Python 3.3, to prevent some denial-of-service attacks). To remove this randomness, the solution is to set the `PYTHONHASHSEED` environment variable to `"0"` *before* Python even starts up. Nothing will happen if you do it after that. Luckily, if you're running this notebook on Colab, the variable is already set for you.

```py
from zlib import crc32

def is_id_in_test_set(identifier, test_ratio):
    return crc32(np.int64(identifier)) < test_ratio * 2**32

def split_data_with_id_hash(data, test_ratio, id_column):
    ids = data[id_column]
    in_test_set = ids.apply(lambda id_: is_id_in_test_set(id_, test_ratio))
    return data.loc[~in_test_set], data.loc[in_test_set]
```

```py
housing_with_id = housing.reset_index()  # adds an `index` column
train_set, test_set = split_data_with_id_hash(housing_with_id, 0.2, "index")
```

```py
housing_with_id["id"] = housing["longitude"] * 1000 + housing["latitude"]
train_set, test_set = split_data_with_id_hash(housing_with_id, 0.2, "id")
```

```py
from sklearn.model_selection import train_test_split

train_set, test_set = train_test_split(housing, test_size=0.2, random_state=42)
```

```py
test_set["total_bedrooms"].isnull().sum()
```

1. `numpy.random.seed()` 函数是 NumPy 库中的一个函数，用于设置随机数生成器的种子。种子是一个整数值，用于初始化随机数生成器的状态，从而确定随机数生成的序列。

   在使用随机数生成器生成随机数时，如果设置了种子，那么每次运行程序时都会得到相同的随机数序列。这对于需要可重复性的实验、调试和测试非常有用。

   `numpy.random.seed()` 函数的语法如下：

   ```python
   numpy.random.seed(seed=None)
   ```

   参数说明：

   - `seed`：可选参数，用于设置随机数生成器的种子。可以是整数或 None。如果不提供种子值，则使用系统时间作为默认种子值。

   下面是一个示例，演示如何使用 `numpy.random.seed()` 函数设置随机数生成器的种子：

   ```python
   import numpy as np
   
   # 设置种子
   np.random.seed(42)
   
   # 生成随机数
   random_numbers = np.random.rand(5)
   
   # 打印结果
   print(random_numbers)
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   [0.37454012 0.95071431 0.73199394 0.59865848 0.15601864]
   ```

   在上述示例中，我们首先调用 `numpy.random.seed(42)`，将种子值设置为 42。然后，通过调用 `np.random.rand(5)` 生成了一个包含 5 个随机数的一维数组 `random_numbers`。由于设置了种子，因此无论何时运行这段代码，都会得到相同的随机数序列。

   需要注意的是，设置种子的作用范围是在当前的 NumPy 随机数生成器中。如果在多个地方都使用了不同的随机数生成器，那么需要在每个生成器中分别设置种子。

   总之，`numpy.random.seed()` 函数用于设置随机数生成器的种子，以确定随机数生成的序列。通过设置种子，可以实现随机数的可重复性，确保在相同的种子下生成相同的随机数序列。这对于实验、调试和测试等需要可靠性和可重复性的场景非常有用。

2. `reset_index()` 是 Pandas 库中的一个函数，用于重置数据框（DataFrame）或序列（Series）的索引。它会将原始的索引重新设置为默认的整数索引，并将原始索引作为一个新的列添加到数据框中。

   `reset_index()` 函数的语法如下：

   对于数据框（DataFrame）：

   ```python
   dataframe.reset_index(level=None, drop=False, inplace=False)
   ```

   对于序列（Series）：

   ```python
   series.reset_index(drop=False, inplace=False)
   ```

   参数说明：

   - `level`：可选参数，用于指定要重置的索引级别。默认为 `None`，表示重置所有索引级别。
   - `drop`：可选参数，指定是否丢弃原始索引。默认为 `False`，表示将原始索引保留为新的列。
   - `inplace`：可选参数，指定是否在原始对象上直接修改，而不是创建一个副本。默认为 `False`，表示创建一个新的对象。

   下面是一些示例，演示如何使用 `reset_index()` 函数进行索引重置：

   ```python
   import pandas as pd
   
   # 创建示例数据框
   df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'C': [7, 8, 9]})
   
   # 打印原始数据框
   print("原始数据框:")
   print(df)
   
   # 重置索引
   reset_df = df.reset_index()
   
   # 打印重置索引后的数据框
   print("重置索引后的数据框:")
   print(reset_df)
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   原始数据框:
      A  B  C
   0  1  4  7
   1  2  5  8
   2  3  6  9
   重置索引后的数据框:
      index  A  B  C
   0      0  1  4  7
   1      1  2  5  8
   2      2  3  6  9
   ```

   在上述示例中，我们首先创建了一个示例数据框 `df`，包含了三列（A、B、C）的数据。然后，通过调用 `reset_index()` 函数，我们将数据框的索引重置为默认的整数索引。重置索引后的数据框存储在 `reset_df` 中，并打印原始数据框和重置索引后的数据框。

   `reset_index()` 函数在数据处理和分析中经常用于重置索引，特别是在对数据框进行分组、筛选或合并操作后，可以恢复默认的整数索引，并方便后续的分析和操作。

3. `apply()` 是 Pandas 库中的一个函数，用于在数据框（DataFrame）或序列（Series）的行或列上应用自定义函数或操作。它可以将函数应用于数据框的每一行或每一列，或者将函数应用于序列的每个元素，并返回结果。

   `apply()` 函数的语法如下：

   对于数据框（DataFrame）：

   ```python
   dataframe.apply(func, axis=0, raw=False, result_type=None, args=(), **kwargs)
   ```

   对于序列（Series）：

   ```python
   series.apply(func, convert_dtype=True, args=())
   ```

   参数说明：

   - `func`：要应用的函数或操作。
   - `axis`：可选参数，指定应用函数的轴。`0` 表示按列应用，`1` 表示按行应用。默认为 `0`。
   - `raw`：可选参数，在数据框上应用函数时，指定是否将每一行或列作为一维数组传递给函数。默认为 `False`，表示将每个元素作为参数传递给函数。
   - `result_type`：可选参数，指定返回结果的类型。默认为 `None`，表示返回一个数据框（DataFrame）。
   - `args`：可选参数，用于传递给函数的额外参数。

   下面是一些示例，演示如何使用 `apply()` 函数应用函数或操作：

   ```python
   import pandas as pd
   
   # 创建示例数据框
   df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'C': [7, 8, 9]})
   
   # 定义一个函数，用于计算每一行的和
   def row_sum(row):
       return row.sum()
   
   # 应用函数到每一行
   row_sums = df.apply(row_sum, axis=1)
   
   # 打印结果
   print("每行的和:")
   print(row_sums)
   
   # 应用函数到每一列
   col_sums = df.apply(lambda col: col.sum(), axis=0)
   
   # 打印结果
   print("每列的和:")
   print(col_sums)
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   每行的和:
   0    12
   1    15
   2    18
   dtype: int64
   每列的和:
   A     6
   B    15
   C    24
   dtype: int64
   ```

   在上述示例中，我们首先创建了一个示例数据框 `df`，包含了三列（A、B、C）的数据。然后，我们定义了一个名为 `row_sum` 的函数，用于计算数据框每一行的和。接下来，我们使用 `apply()` 函数将 `row_sum` 函数应用于数据框的每一行，通过指定 `axis=1` 参数来实现。结果存储在 `row_sums` 中，它是一个包含每行和的序列。

   然后，我们使用匿名函数（lambda 函数）将 `sum()` 函数应用于数据框的每一列，通过指定 `axis=0` 参数来实现。结果存储在 `col_sums` 中，它是一个包含每列和的序列。

   `apply()` 函数在数据分析和数据转换中非常有用，可以将自定义的函数应用于数据框的行或列，或者对序列中的每个元素进行操作。它提供了一种灵活的方式来处理数据，使得我们可以根据自己的需求进行定制化的操作。

4. `train_test_split()` 是 Scikit-Learn（sklearn）库中的一个函数，用于将数据集划分为训练集和测试集。它是机器学习中常用的数据预处理步骤之一，用于评估模型在未见过的数据上的性能。

   `train_test_split()` 函数的语法如下：

   ```python
   train_test_split(*arrays, test_size=None, train_size=None, random_state=None, shuffle=True, stratify=None)
   ```

   参数说明：

   - `*arrays`：待划分的数据集，可以是一个或多个数组（特征矩阵或目标向量）。
   - `test_size`：可选参数，指定测试集的大小。可以是浮点数（表示比例）或整数（表示样本数）。默认为 `None`，表示将数据集划分为相等大小的训练集和测试集。
   - `train_size`：可选参数，指定训练集的大小。可以是浮点数（表示比例）或整数（表示样本数）。默认为 `None`，表示将数据集划分为相等大小的训练集和测试集。
   - `random_state`：可选参数，指定随机数种子。用于控制数据集的随机划分。设置相同的种子将确保每次运行时划分结果的一致性。
   - `shuffle`：可选参数，指定是否在划分数据集之前对数据进行洗牌。默认为 `True`，表示进行洗牌操作。
   - `stratify`：可选参数，用于进行分层抽样。如果指定了 `stratify`，则返回的划分数据集将保持原始数据集中各类别样本的比例。

   下面是一个示例，演示如何使用 `train_test_split()` 函数划分数据集：

   ```python
   from sklearn.model_selection import train_test_split
   import numpy as np
   
   # 创建示例特征矩阵和目标向量
   X = np.array([[1, 2], [3, 4], [5, 6], [7, 8]])
   y = np.array([0, 1, 0, 1])
   
   # 划分数据集
   X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
   
   # 打印划分结果
   print("训练集特征矩阵:")
   print(X_train)
   print("测试集特征矩阵:")
   print(X_test)
   print("训练集目标向量:")
   print(y_train)
   print("测试集目标向量:")
   print(y_test)
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   训练集特征矩阵:
   [[1 2]
    [3 4]
    [7 8]]
   测试集特征矩阵:
   [[5 6]]
   训练集目标向量:
   [0 1 1]
   测试集目标向量:
   [0]
   ```

   在上述示例中，我们首先创建了一个示例特征矩阵 `X` 和目标向量 `y`。然后，通过调用 `train_test_split()` 函数，将数据集划分为训练集和测试集。我们指定了 `test_size=0.2`，表示将数据集划分为 80% 的训练集和 20% 的测试集。另外，我们设置了 `random_state=42`，以确保每次运行时划分结果的一致性。

   划分后的训练集特征矩阵存储在 `X_train` 中，测试集特征矩阵存储在 `X_test` 中。同样，训练集目标向量存储在 `y_train` 中，测试集目标向量存储在 `y_test` 中。

   `train_test_split()` 函数在机器学习中广泛应用于模型的训练和评估过程中，它可以将给定的数据集划分为独立的训练集和测试集，以便在训练模型时使用训练集进行参数估计，并在测试集上评估模型的性能。这样可以更好地了解模型的泛化能力，即在未见过的数据上的表现如何。

   划分数据集是为了避免模型在训练过程中过拟合（overfitting），即过度适应训练集而在未见过的数据上表现不佳。通过将数据集划分为训练集和测试集，可以在模型训练过程中通过测试集的性能评估来监控模型的表现，并进行调整和改进。

   除了划分训练集和测试集之外，还可以使用交叉验证（cross-validation）来更全面地评估模型的性能。Scikit-Learn 提供了 `cross_val_score()` 函数来执行交叉验证，可以在不同的数据子集上多次训练和测试模型，并返回对应的性能指标。

   总结起来，`train_test_split()` 函数是 Scikit-Learn 中用于划分数据集的一个方便工具。它可以将数据集划分为训练集和测试集，使我们能够更好地评估模型在未见过的数据上的性能，从而进行模型选择和调优。

   

```py
housing["income_cat"] = pd.cut(housing["median_income"],
                               bins=[0., 1.5, 3.0, 4.5, 6., np.inf],
                               labels=[1, 2, 3, 4, 5])
```

```py
strat_train_set, strat_test_set = train_test_split(
    housing, test_size=0.2, stratify=housing["income_cat"], random_state=42)
```

```py
housing["income_cat"].value_counts()
```

```py
housing["income_cat"].hist()
```

```py
from sklearn.model_selection import StratifiedShuffleSplit

split = StratifiedShuffleSplit(n_splits=1, test_size=0.2, random_state=42)
for train_index, test_index in split.split(housing, housing["income_cat"]):
    strat_train_set = housing.loc[train_index]
    strat_test_set = housing.loc[test_index]
```

```py
strat_test_set["income_cat"].value_counts() / len(strat_test_set)
```

```py
housing["income_cat"].value_counts() / len(housing)
```

```py
def income_cat_proportions(data):
    return data["income_cat"].value_counts() / len(data)

train_set, test_set = train_test_split(housing, test_size=0.2, random_state=42)

compare_props = pd.DataFrame({
    "Overall": income_cat_proportions(housing),
    "Stratified": income_cat_proportions(strat_test_set),
    "Random": income_cat_proportions(test_set),
}).sort_index()
compare_props["Rand. %error"] = 100 * compare_props["Random"] / compare_props["Overall"] - 100
compare_props["Strat. %error"] = 100 * compare_props["Stratified"] / compare_props["Overall"] - 100
```

```py
compare_props
```

```py
for set_ in (strat_train_set, strat_test_set):
    set_.drop("income_cat", axis=1, inplace=True)
```

1. `cut()` 是 Pandas 库中的一个函数，用于将连续数据分成离散的区间（bins）。它可以将一列数据按照指定的区间划分成不同的类别或分组，通常用于数据的分析、可视化和建模过程。

   `cut()` 函数的语法如下：

   ```python
   pandas.cut(x, bins, right=True, labels=None, retbins=False, precision=3, include_lowest=False, duplicates='raise')
   ```

   参数说明：

   - `x`：要划分的一维数组、Series 或 DataFrame 的列。
   - `bins`：划分的区间。可以是一个整数（表示等宽的区间数量），也可以是一个列表、数组（表示自定义的区间边界）。
   - `right`：可选参数，指定区间的开闭。默认为 `True`，表示区间右边为闭区间，即包含右边界值；设置为 `False` 表示区间右边为开区间，不包含右边界值。
   - `labels`：可选参数，用于标记划分后的类别。可以是一个列表或数组，长度与划分后的区间数相同。如果未指定，则将返回整数编码的类别。
   - `retbins`：可选参数，指定是否返回划分后的区间边界。默认为 `False`，表示不返回区间边界；设置为 `True` 表示返回区间边界。
   - `precision`：可选参数，指定区间边界的小数精度。默认为 `3`。
   - `include_lowest`：可选参数，指定是否将最低值包含在第一个区间中。默认为 `False`。
   - `duplicates`：可选参数，处理区间边界的重复值。默认为 `'raise'`，表示遇到重复的边界值时抛出异常；设置为 `'drop'` 表示删除重复的边界值。

   下面是一个示例，演示如何使用 `cut()` 函数对数据进行区间划分：

   ```python
   import pandas as pd
   import numpy as np
   
   # 创建示例数据
   data = pd.Series([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
   
   # 划分数据为三个区间
   bins = [0, 4, 7, 10]
   categories = ['Low', 'Medium', 'High']
   result = pd.cut(data, bins, labels=categories)
   
   # 打印划分结果
   print(result)
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   0       Low
   1       Low
   2       Low
   3       Low
   4    Medium
   5    Medium
   6    Medium
   7      High
   8      High
   9      High
   dtype: category
   Categories (3, object): ['Low' < 'Medium' < 'High']
   ```

   在上述示例中，我们首先创建了一个示例数据 `data`，包含了一列连续的数值。然后，我们使用 `cut()` 函数将数据划分为三个区间：`[0, 4)`、`[4, 7)` 和 `[7, 10]`。我们还指定了对应的类别标签为 `'Low'`、`'Medium'` 和 `'High'`。

   调用 `cut()` 函数后，返回的是一个 Pandas 的 Categorical 类型对象，它是一个带有类别标签的序列。每个元素被划分到对应的区间，并使用指定的标签进行标记。

   `cut()` 函数在数据分析和数据预处理中非常有用，可以将连续的数值数据转换为离散的类别，便于进行统计分析、数据可视化和建模等操作。通过划分数据为不同的区间，我们可以更好地理解数据的分布和特征，并从中提取有用的信息和洞察。

2. `StratifiedShuffleSplit()` 是 scikit-learn（也称为 sklearn）库中的一个函数，用于生成分层随机划分的数据集。该函数可以用于在保持类别分布的同时，将数据集随机划分为训练集和测试集，适用于分类任务。

   `StratifiedShuffleSplit()` 函数的语法如下：

   ```python
   sklearn.model_selection.StratifiedShuffleSplit(n_splits=10, test_size=None, train_size=None, random_state=None)
   ```

   参数说明：

   - `n_splits`：表示划分的次数（默认为 10），即生成多少个不同的训练集和测试集划分。
   - `test_size`：可选参数，表示测试集的比例或绝对大小。可以是一个浮点数（0~1之间，表示比例）或整数（表示绝对大小）。如果未指定，则测试集的大小与训练集相同。
   - `train_size`：可选参数，表示训练集的比例或绝对大小。可以是一个浮点数（0~1之间，表示比例）或整数（表示绝对大小）。如果未指定，则训练集的大小与测试集相同。
   - `random_state`：可选参数，用于设置随机种子，以确保可重复的随机划分。

   下面是一个示例，演示如何使用 `StratifiedShuffleSplit()` 函数进行数据集的分层随机划分：

   ```python
   from sklearn.model_selection import StratifiedShuffleSplit
   import numpy as np
   
   # 创建示例数据
   X = np.array([[1, 2], [3, 4], [5, 6], [7, 8], [9, 10]])
   y = np.array([0, 0, 1, 1, 1])
   
   # 使用 StratifiedShuffleSplit 进行划分
   sss = StratifiedShuffleSplit(n_splits=1, test_size=0.2, random_state=42)
   train_indices, test_indices = next(sss.split(X, y))
   
   # 打印划分结果
   print("训练集索引:", train_indices)
   print("测试集索引:", test_indices)
   print("训练集数据:")
   print(X[train_indices])
   print("测试集数据:")
   print(X[test_indices])
   ```

   运行上述示例代码，可能得到类似以下的输出结果：

   ```
   训练集索引: [2 1 0]
   测试集索引: [4 3]
   训练集数据:
   [[5 6]
    [3 4]
    [1 2]]
   测试集数据:
   [[ 9 10]
    [ 7  8]]
   ```

   在上述示例中，我们首先创建了一个示例数据 `X` 和类别标签 `y`。`X` 是一个包含特征的二维数组，`y` 是对应的类别标签。

   然后，我们使用 `StratifiedShuffleSplit()` 函数进行数据集的划分。设置 `n_splits=1` 表示只进行一次划分，`test_size=0.2` 表示测试集的大小为总样本数的 20%。

   调用 `split(X, y)` 方法可生成一个迭代器，通过 `next()` 函数获取划分后的训练集和测试集的索引。然后，我们可以根据索引从原始数据中提取相应的训练集和测试集数据。

   `StratifiedShuffleSplit()` 函数的主要优势在于它可以保持原始数据集中各个类别的分布比例，从而更准确地评估分类模型的性能。例如，在不平衡的数据集中，如果直接进行随机划分，可能会导致训练集或测试集中某个类别的样本数量过少，从而影响模型的训练或评估结果。而使用分层随机划分，可以确保每个划分中的类别比例与原始数据集中相同。

   注意，`StratifiedShuffleSplit()` 函数适用于分类任务，其中类别标签需要是离散的。如果是回归任务或类别标签是连续的，可以考虑使用 `ShuffleSplit()` 函数进行随机划分。

3. 在 Pandas 中，`drop()` 是一个用于删除指定行或列的函数。它可以从 DataFrame 或 Series 中删除指定的标签（行或列），并返回一个新的对象，而不会修改原始数据。

   `drop()` 函数的语法如下：

   ```python
   DataFrame.drop(labels, axis=0, index=None, columns=None, inplace=False)
   ```

   参数说明：

   - `labels`：要删除的标签（行或列）的名称或名称列表。
   - `axis`：可选参数，指定删除的轴。默认为 `0`，表示按行删除；设置为 `1`，表示按列删除。
   - `index`：可选参数，用于指定要删除的行的名称或名称列表。与 `labels` 参数二选一。
   - `columns`：可选参数，用于指定要删除的列的名称或名称列表。与 `labels` 参数二选一。
   - `inplace`：可选参数，指定是否就地修改原始数据。默认为 `False`，表示返回一个新的对象；设置为 `True`，表示在原始数据上进行修改，并返回 `None`。

   下面是一些示例，演示如何使用 `drop()` 函数删除行或列：

   **删除行：**

   ```python
   import pandas as pd
   
   # 创建示例数据
   data = {'Name': ['Alice', 'Bob', 'Charlie', 'David'],
           'Age': [25, 30, 35, 40],
           'Gender': ['Female', 'Male', 'Male', 'Male']}
   df = pd.DataFrame(data)
   
   # 删除指定的行
   new_df = df.drop([0, 2])  # 删除索引为 0 和 2 的行
   
   # 打印删除行后的 DataFrame
   print(new_df)
   ```

   运行上述示例代码，可能得到以下输出结果：

   ```
        Name  Age Gender
   1     Bob   30   Male
   3   David   40   Male
   ```

   在上述示例中，我们创建了一个示例数据 DataFrame `df`。然后，使用 `drop()` 函数删除了索引为 0 和 2 的行，生成了一个新的 DataFrame `new_df`。

   **删除列：**

   ```python
   import pandas as pd
   
   # 创建示例数据
   data = {'Name': ['Alice', 'Bob', 'Charlie', 'David'],
           'Age': [25, 30, 35, 40],
           'Gender': ['Female', 'Male', 'Male', 'Male']}
   df = pd.DataFrame(data)
   
   # 删除指定的列
   new_df = df.drop(columns=['Age', 'Gender'])  # 删除列 'Age' 和 'Gender'
   
   # 打印删除列后的 DataFrame
   print(new_df)
   ```

   运行上述示例代码，可能得到以下输出结果：

   ```
         Name
   0    Alice
   1      Bob
   2  Charlie
   3    David
   ```

   在上述示例中，我们创建了一个示例数据 DataFrame `df`。然后，使用 `drop()` 函数删除了列 'Age' 和 'Gender'，生成了一个新的 DataFrame `new_df`。

   `drop()` 函数在数据处理和清洗过程中非常有用，可以根据需要删除不需要的行或列，从而提取或转换数据。注意，`drop()` 函数返回一个新的对象，原始数据不会被修改，除非将 `inplace` 参数设置为 `True`。





## Discover and Visualize the Data to Gain Insights

#### **Visualizing Geographical Data**

```py
housing = strat_train_set.copy()
```

```py
housing.plot(kind="scatter", x="longitude", y="latitude")
save_fig("bad_visualization_plot")

housing.plot(kind="scatter", x="longitude", y="latitude", alpha=0.1)
save_fig("better_visualization_plot")
```

1. plot函数是一种在数据可视化中常用的函数，它用于绘制二维图形，例如折线图、散点图、条形图等。plot函数能够将数据以图形的形式展示出来，帮助我们更好地理解数据的分布、趋势和关系。

   plot函数的作用可以总结为以下几点：

   1. 数据可视化：plot函数可以将数据转化为可视化的图形，帮助我们更直观地观察数据的特征和变化趋势。通过图形，我们可以更好地理解数据背后的规律和关系。
   2. 数据探索：使用plot函数可以帮助我们发现数据中的模式、异常和趋势。通过绘制不同类型的图形，比如折线图、散点图和直方图，我们可以观察数据的分布情况，发现数据中的离群点或异常值，并探索数据之间的相关性和趋势。
   3. 数据比较：plot函数还可以用于比较不同数据集之间的差异和相似性。通过在同一张图上绘制多个数据集的图形，我们可以直观地比较它们的分布、趋势和变化。
   4. 结果展示：plot函数可以将分析结果以可视化的方式呈现给他人。通过图形展示，我们可以更好地向他人传达我们的发现和结论，使得信息更易于理解和接受。

   在使用plot函数时，我们可以设置各种参数来调整图形的样式和展示方式，比如线条颜色、标记类型、坐标轴范围等，以满足我们对图形的需求。同时，plot函数通常会与其他数据处理和分析函数配合使用，如数据读取、数据清洗和统计计算等，以实现更全面的数据分析和可视化任务。

   plot函数有许多常用的参数可以设置，以下是其中一些常见的参数：

   1. x, y：要绘制的数据的x坐标和y坐标。可以是列表、数组、Series或DataFrame对象。
   2. linestyle：线条的样式，如实线('-')、虚线('--')、点线('-.')等。
   3. marker：数据点的标记样式，如圆点('o')、方块('s')、三角形('^')等。
   4. color：线条或标记的颜色，可以使用颜色名称（如'red'、'blue'）、RGB值（如(0.2, 0.4, 0.6)）或十六进制值（如'#FF0000'）。
   5. linewidth：线条的宽度。
   6. markersize：标记的大小。
   7. label：图例中显示的标签，用于区分不同的数据集。
   8. title：图表的标题。
   9. xlabel, ylabel：x轴和y轴的标签。
   10. xlim, ylim：x轴和y轴的显示范围。
   11. grid：是否显示网格线。
   12. legend：是否显示图例。
   13. figsize：图形的大小，以元组形式指定宽度和高度。

   这只是一小部分常用的参数，实际上plot函数还有更多其他参数可以用于进一步定制图形的样式和布局。通过灵活地使用这些参数，我们可以根据需求创建出各种各样的图形来展示数据。



```py
housing.plot(kind="scatter", x="longitude", y="latitude", alpha=0.4,
             s=housing["population"]/100, label="population", figsize=(10,7),
             c="median_house_value", cmap=plt.get_cmap("jet"), colorbar=True,
             sharex=False)
plt.legend()
save_fig("housing_prices_scatterplot")
```

1. legend函数用于在图形中添加图例（legend），图例是用于标识不同数据系列或图形元素的标签。它提供了一种简洁明了的方式，让读者可以快速理解图形中各个元素的含义和对应关系。

   具体来说，legend函数的作用包括：

   1. 标识不同数据系列：当在同一张图中绘制多个数据系列时，可以使用legend函数为每个数据系列添加一个标签，以区分它们。这样，读者就可以清楚地知道每个数据系列所代表的含义，从而更好地理解图形。

   1. 显示样式信息：如果在绘图过程中使用了不同的线条样式、标记样式或颜色，可以使用legend函数将这些样式信息添加到图例中。这样，读者可以通过图例了解不同样式对应的含义，进一步理解图形的特征和变化。

   1. 控制图例位置：legend函数还提供了一些参数用于控制图例的位置和布局。可以将图例放置在图形的不同位置，如右上角、左下角、右下角等，以及调整图例的大小和间距。这样可以根据实际需要进行图例的定位和调整，以使图形更清晰和易于阅读。

   在使用legend函数时，通常需要与绘图函数（如plot函数）或其他绘图相关的函数配合使用。通过在绘图过程中为每个数据系列设置label标签，并在绘图完成后调用legend函数，可以将标签显示为图例。这样就能够更好地解释图形中的数据和元素，增强图形的可读性和解释性。

   

#### **Looking for Correlations**

```py
corr_matrix = housing.corr()
```

```py
corr_matrix["median_house_value"].sort_values(ascending=False)
```

```py
# from pandas.tools.plotting import scatter_matrix # For older versions of Pandas
from pandas.plotting import scatter_matrix

attributes = ["median_house_value", "median_income", "total_rooms",
              "housing_median_age"]
scatter_matrix(housing[attributes], figsize=(12, 8))
save_fig("scatter_matrix_plot")
```

1. `corr()`函数用于计算数据集中各列之间的相关性。它可以用于DataFrame对象或Series对象，计算列与列之间的相关性矩阵或列与序列之间的相关性。

   具体来说，`corr()`函数的作用包括：

   1. 计算相关性矩阵：对于DataFrame对象，`corr()`函数可以计算数据集中各列之间的相关性。相关性矩阵是一个对称矩阵，其中每个元素表示对应两列之间的相关性系数。相关性系数的取值范围为-1到1，-1表示完全负相关，1表示完全正相关，0表示无相关性。通过相关性矩阵，可以了解数据集中各列之间的关联程度。

   1. 计算列与序列之间的相关性：对于DataFrame对象或Series对象，`corr()`函数还可以计算其中一列与另一个Series对象之间的相关性。这在分析单个列与整个数据集中其他列之间的关系时非常有用。例如，可以计算某一列与目标变量之间的相关性，以评估特征与目标之间的线性关系。

   `corr()`函数的返回结果是一个相关性矩阵或相关系数。可以进一步使用可视化工具（如热力图）来呈现相关性矩阵，以更直观地展示不同变量之间的相关性。

   以下是一个示例使用`corr()`函数的代码片段：

   ```python
   import pandas as pd
   
   # 创建DataFrame对象
   data = {'A': [1, 2, 3, 4, 5], 'B': [2, 4, 6, 8, 10], 'C': [3, 6, 9, 12, 15]}
   df = pd.DataFrame(data)
   
   # 计算相关性矩阵
   correlation_matrix = df.corr()
   
   print(correlation_matrix)
   ```

   上述代码中，我们创建了一个包含三列（A、B、C）的DataFrame对象。然后，我们使用`corr()`函数计算了这些列之间的相关性矩阵，并将结果打印输出。

2. 在数据处理和分析中，`axis`参数被广泛用于指定沿着哪个轴进行操作。它可以用于多个函数和方法中，其中最常见的是NumPy和Pandas库中的函数和方法。

   具体来说，`axis`参数的作用包括：

   1. 沿指定轴进行聚合操作：在一些聚合函数中（如`sum()`、`mean()`、`max()`、`min()`等），`axis`参数用于指定聚合操作沿着哪个轴进行。例如，`axis=0`表示沿着行（垂直）方向进行聚合，`axis=1`表示沿着列（水平）方向进行聚合。

   1. 沿指定轴进行计算：在一些计算函数中（如`sum()`、`mean()`、`std()`等），`axis`参数用于指定计算沿着哪个轴进行。通过指定不同的轴，可以沿着不同维度进行计算，例如计算每列的总和、每行的平均值等。

   1. 指定轴的方向或位置：在一些函数和方法中，`axis`参数用于指定轴的方向或位置。例如，`axis=0`表示沿着第一个轴（行轴）进行操作，`axis=1`表示沿着第二个轴（列轴）进行操作。

   需要注意的是，不同函数和方法对`axis`参数的使用方式和含义可能会有所不同。在使用时，建议查阅对应函数或方法的文档或帮助文档，以了解准确的`axis`参数用法和可选取值。

   以下是一个示例，展示了在NumPy和Pandas中使用`axis`参数的例子：

   ```python
   import numpy as np
   import pandas as pd
   
   # NumPy示例
   arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
   
   # 沿着第一个轴（行轴）计算总和
   row_sum = np.sum(arr, axis=0)
   print(row_sum)  # 输出：[12 15 18]
   
   # 沿着第二个轴（列轴）计算平均值
   column_mean = np.mean(arr, axis=1)
   print(column_mean)  # 输出：[2. 5. 8.]
   
   # Pandas示例
   df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6], 'C': [7, 8, 9]})
   
   # 沿着行轴计算总和
   row_sum = df.sum(axis=0)
   print(row_sum)
   # 输出：
   # A    6
   # B    15
   # C    24
   # dtype: int64
   
   # 沿着列轴计算平均值
   column_mean = df.mean(axis=1)
   print(column_mean)
   # 输出：
   # 0    4.0
   # 1    5.0
   # 2    6.0
   # dtype: float64
   ```

   上述代码演示了在NumPy中使用`axis`参数计算数组的总和和平均值，以及在Pandas中使用`axis`参数计算DataFrame的总和和平均值。

```py
housing.plot(kind="scatter", x="median_income", y="median_house_value",
             alpha=0.1)
plt.axis([0, 16, 0, 550000])
save_fig("income_vs_house_value_scatterplot")
```



#### Experimenting with Attribute Combinations

```py
housing["rooms_per_household"] = housing["total_rooms"]/housing["households"]
housing["bedrooms_per_room"] = housing["total_bedrooms"]/housing["total_rooms"]
housing["population_per_household"]=housing["population"]/housing["households"]
```

```py
corr_matrix = housing.corr()
corr_matrix["median_house_value"].sort_values(ascending=False)
```

```py
housing.plot(kind="scatter", x="rooms_per_household", y="median_house_value",
             alpha=0.2)
plt.axis([0, 5, 0, 520000])
plt.show()
```

```py
housing.describe()
```



## Prepare the Data for Machine Learning Algorithms

```py
housing = strat_train_set.drop("median_house_value", axis=1) # drop labels for training set
housing_labels = strat_train_set["median_house_value"].copy()
```

#### Data Cleaning

```py
housing.dropna(subset=["total_bedrooms"])    # option 1
housing.drop("total_bedrooms", axis=1)       # option 2
median = housing["total_bedrooms"].median()  # option 3
housing["total_bedrooms"].fillna(median, inplace=True)
```

1. 在数据分析和处理中，`dropna()`函数是一种用于处理缺失值的常见方法之一。它用于从DataFrame中删除包含缺失值的行或列。

   具体而言，`dropna()`函数的作用是根据设定的条件删除DataFrame中包含缺失值的行或列。缺失值可以是NaN（Not a Number）或None。

   下面是`dropna()`函数的一般用法：

   ```python
   DataFrame.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
   ```

   参数说明：

   - `axis`：指定删除行或列，`axis=0`表示删除包含缺失值的行，默认值为0。
   - `how`：指定删除行或列的条件，可选值包括：
     - `'any'`：只要某行或某列存在缺失值，就删除该行或列。
     - `'all'`：只有当某行或某列的所有元素都是缺失值时，才删除该行或列。
   - `thresh`：指定每行或每列非缺失值的最小数量。如果某行或某列的非缺失值数量小于`thresh`，则删除该行或列。
   - `subset`：指定要考虑的列或行的子集。可以是单个列名或行标签，也可以是包含多个列名或行标签的列表。
   - `inplace`：指定是否在原始DataFrame上进行就地修改，默认为`False`，表示返回一个新的DataFrame，原始DataFrame不变。

   下面是一个示例，展示如何使用`dropna()`函数删除包含缺失值的行：

   ```python
   import pandas as pd
   
   # 创建一个包含缺失值的DataFrame
   data = {'A': [1, 2, None, 4],
           'B': [5, None, None, 8],
           'C': [None, None, None, None]}
   df = pd.DataFrame(data)
   
   # 删除包含缺失值的行
   df_dropped = df.dropna()
   
   print(df_dropped)
   ```

   输出结果：

   ```
        A    B   C
   0  1.0  5.0 NaN
   ```

   在上述示例中，原始DataFrame `df` 包含缺失值。通过调用 `dropna()` 函数，删除了包含缺失值的行，得到了新的DataFrame `df_dropped`，只保留了第一行，其他行被删除了。

   需要注意的是，`dropna()`函数在处理缺失值时会删除包含缺失值的行或列，因此在使用时需要根据具体情况谨慎选择参数，以确保得到符合要求的数据集。

   

```py
from sklearn.impute import SimpleImputer
imputer = SimpleImputer(strategy="median")
```

Remove the text attribute because median can only be calculated on numerical attributes:

```py
housing_num = housing.drop("ocean_proximity", axis=1)
# alternatively: housing_num = housing.select_dtypes(include=[np.number])
```

```py
imputer.fit(housing_num)
```

Check that this is the same as manually computing the median of each attribute:

```py
housing_num.median().values
```

Transform the training set:

```py
X = imputer.transform(housing_num)
```

```py
housing_tr = pd.DataFrame(X, columns=housing_num.columns,
                          index=housing.index)
```

```py
housing_tr.loc[sample_incomplete_rows.index.values]
```

```py
imputer.strategy
```

```py
housing_tr = pd.DataFrame(X, columns=housing_num.columns,
                          index=housing_num.index)
```

```py
housing_tr.head()
```

1. `loc()`函数是Pandas库中用于基于标签进行索引和切片的函数。它用于访问和操作DataFrame中的数据，具有灵活性和强大的功能。

   `loc()`函数的主要作用是通过标签（行标签和列标签）来选择和访问DataFrame中的数据。它可以用于以下几个方面：

   1. 选择行或列：通过行标签或列标签，使用`loc()`函数可以选择指定的行或列。可以使用单个标签，也可以使用标签的切片。
   1. 条件筛选：可以使用布尔条件对DataFrame进行筛选，选择满足条件的行或列。
   1. 修改数据：通过`loc()`函数，可以直接对DataFrame中的数据进行修改或赋值操作。

   下面是`loc()`函数的一般用法：

   ```python
   DataFrame.loc[row_indexer, column_indexer]
   ```

   参数说明：

   - `row_indexer`：用于选择行的标签，可以是单个标签、标签列表或标签切片。
   - `column_indexer`：用于选择列的标签，可以是单个标签、标签列表或标签切片。

   下面是一些示例，展示了`loc()`函数的用法：

   ```python
   import pandas as pd
   
   # 创建一个示例DataFrame
   data = {'A': [1, 2, 3, 4],
           'B': [5, 6, 7, 8],
           'C': [9, 10, 11, 12]}
   df = pd.DataFrame(data, index=['a', 'b', 'c', 'd'])
   
   # 选择单个元素
   print(df.loc['a', 'A'])  # 输出: 1
   
   # 选择多行
   print(df.loc['a':'c'])  # 输出:
   #    A  B   C
   # a  1  5   9
   # b  2  6  10
   # c  3  7  11
   
   # 选择多列
   print(df.loc[:, 'A':'B'])  # 输出:
   #    A  B
   # a  1  5
   # b  2  6
   # c  3  7
   # d  4  8
   
   # 使用条件筛选
   print(df.loc[df['A'] > 2])  # 输出:
   #    A  B   C
   # c  3  7  11
   # d  4  8  12
   
   # 修改数据
   df.loc['a', 'A'] = 100
   print(df)
   # 输出:
   #      A  B   C
   # a  100  5   9
   # b    2  6  10
   # c    3  7  11
   # d    4  8  12
   ```

   上述示例展示了`loc()`函数的几种常见用法。通过指定行标签和列标签，可以选择单个元素、多行或多列。还可以使用条件筛选选择满足特定条件的行。最后，通过`loc()`函数，可以直接对DataFrame中的数据进行修改。

   需要注意的是，`loc()`函数基于标签进行索引，因此标签必须存在于DataFrame的索引或列中，否则将引发`KeyError`错误。

2. DataFrame的索引（index）是用于标识和访问DataFrame中行的标签或标识符。它提供了一种有序的方式来引用和操作DataFrame中的数据。

   索引在DataFrame中有以下几个特点：

   1. 默认索引：当创建DataFrame时，如果没有明确指定索引，Pandas会自动创建一个默认的整数索引，从0开始递增。
   1. 唯一性：索引的值必须是唯一的，每个行必须具有不同的索引值。
   1. 不可变性：索引的值是不可变的，一旦创建，就不能直接修改索引的值。
   1. 多样性：索引可以是整数、标签（字符串）、日期时间等类型，甚至可以是多级索引（层次化索引）。

   DataFrame的索引可以通过`index`属性获取，如下所示：

   ```python
   import pandas as pd
   
   data = {'A': [1, 2, 3],
           'B': [4, 5, 6]}
   df = pd.DataFrame(data)
   
   index = df.index
   print(index)
   ```

   输出结果为：

   ```
   RangeIndex(start=0, stop=3, step=1)
   ```

   在上述示例中，DataFrame `df` 的索引是一个`RangeIndex`对象，表示默认的整数索引。它的起始索引值是0，结束索引值是3（不包含），步长为1。

   可以使用不同的方法来操作DataFrame的索引，例如：

   - `reset_index()`：重置索引，将原有的索引重置为默认的整数索引。
   - `set_index()`：将某一列或多列作为新的索引，创建一个新的DataFrame。
   - 切片和选择：可以使用索引进行切片和选择操作，通过索引选择单个元素、多行或多列。

   下面是一些示例，展示了对DataFrame索引的操作：

   ```python
   import pandas as pd
   
   data = {'A': [1, 2, 3],
           'B': [4, 5, 6]}
   df = pd.DataFrame(data, index=['a', 'b', 'c'])
   
   # 重置索引
   df_reset = df.reset_index()
   print(df_reset)
   # 输出:
   #   index  A  B
   # 0     a  1  4
   # 1     b  2  5
   # 2     c  3  6
   
   # 设置新的索引
   df_set = df.set_index('A')
   print(df_set)
   # 输出:
   #    B
   # A   
   # 1  4
   # 2  5
   # 3  6
   
   # 通过索引选择单个元素
   print(df.loc['a', 'B'])  # 输出: 4
   
   # 通过索引选择多行
   print(df.loc['a':'b'])  # 输出:
   #    A  B
   # a  1  4
   # b  2  5
   
   # 通过索引选择多列
   print(df.loc[:, 'A':'B'])  # 输出:
   #    A  B
   # a  1  4
   # b  2  5
   # c  3  6
   ```

   上述示例展示了一些对DataFrame索引的常见操作。可以重置索引为默认的整数索引，也可以将某一列或多列作为新的索引。还可以使用索引进行切片和选择操作，根据索引值选择单个元素、多行或多列。

   需要根据具体需求选择适当的索引类型和操作方法，以便灵活地访问和操作DataFrame中的数据。

3. 在Pandas中，DataFrame的`values`属性用于返回DataFrame中的数据部分，以NumPy数组的形式呈现。它提取DataFrame中的所有数据值，不包括索引和列标签。

   `values`属性的返回结果是一个二维NumPy数组，其中每一行表示DataFrame中的一行数据，每一列表示DataFrame中的一个列数据。返回的数组维度是`(n_rows, n_columns)`，其中`n_rows`是DataFrame中的行数，`n_columns`是DataFrame中的列数。

   以下是一个示例，展示了如何使用`values`属性获取DataFrame中的数据：

   ```python
   import pandas as pd
   
   data = {'A': [1, 2, 3],
           'B': [4, 5, 6]}
   df = pd.DataFrame(data)
   
   array = df.values
   print(array)
   ```

   输出结果为：

   ```
   [[1 4]
    [2 5]
    [3 6]]
   ```

   在上述示例中，DataFrame `df` 包含两列（'A'和'B'）和三行数据。通过调用`values`属性，我们获取了一个二维NumPy数组，其中每一行表示一行数据，每一列表示一列数据。

   `values`属性常用于在需要使用NumPy数组进行数值计算或集成其他库时，将DataFrame转换为NumPy数组。它提供了一种方便的方式来获取DataFrame中的数据部分，以便进行进一步的分析和处理。

   需要注意的是，`values`属性返回的是原始数据的副本，而不是视图。因此，对返回的NumPy数组的任何修改都不会反映到原始的DataFrame中。

4. `SimpleImputer`是scikit-learn库中的一个类，用于对缺失值进行填充。`SimpleImputer`提供了一种简单的策略来处理缺失值，例如用均值、中位数、最频繁值或常数进行填充。

   `SimpleImputer`的`transform`函数用于对输入数据进行转换，并在其中填充缺失值。它接受一个数据集作为输入，并返回一个填充了缺失值的数据集。

   下面是`SimpleImputer`的`transform`函数的一般用法：

   ```python
   imputed_data = imputer.transform(data)
   ```

   参数说明：

   - `data`：要进行填充的数据集，可以是一个NumPy数组或Pandas DataFrame。
   - 返回值：填充了缺失值的数据集，与输入数据的类型相同。

   下面是一个示例，展示了如何使用`SimpleImputer`的`transform`函数进行缺失值填充：

   ```python
   from sklearn.impute import SimpleImputer
   import pandas as pd
   
   # 创建一个示例DataFrame，包含缺失值
   data = {'A': [1, 2, None, 4],
           'B': [5, None, 7, 8],
           'C': [9, 10, 11, None]}
   df = pd.DataFrame(data)
   
   # 创建一个SimpleImputer对象，使用均值填充缺失值
   imputer = SimpleImputer(strategy='mean')
   
   # 对DataFrame进行缺失值填充
   imputed_data = imputer.transform(df)
   
   # 转换结果为一个填充了缺失值的NumPy数组
   print(imputed_data)
   ```

   输出结果为：

   ```
   [[ 1.   5.   9. ]
    [ 2.   6.   10. ]
    [ 2.33333333 7.   11. ]
    [ 4.   8.   10. ]]
   ```

   在上述示例中，我们首先创建了一个包含缺失值的DataFrame `df`。然后，创建了一个`SimpleImputer`对象，使用均值填充缺失值。接下来，使用`transform`函数对DataFrame进行缺失值填充，并将结果存储在`imputed_data`中。

   `imputed_data`是一个填充了缺失值的NumPy数组，其中缺失值被均值填充。可以使用这个填充后的数据进行后续的分析和建模。

   需要注意的是，`SimpleImputer`的`transform`函数仅适用于填充缺失值，不会改变原始数据集。如果需要替换原始数据集中的缺失值，可以将填充后的数据存储回原始数据集中。

5. `SimpleImputer`类的`fit`函数用于计`SimpleImputer`类的`fit`函数用于计算用于填充缺失值的统计量。它接受一个数据集作为输入，并根据指定的填充策略计算相应的统计量。这些统计量将用于后续的填充操作。

   下面是`SimpleImputer`的`fit`函数的一般用法：

   ```python
   imputer.fit(data)
   ```

   参数说明：

   - `data`：用于计算统计量的数据集，可以是一个NumPy数组或Pandas DataFrame。

   `fit`函数没有返回值，但它会根据指定的填充策略计算相应的统计量，并将其存储在`SimpleImputer`对象的属性中，以备后续使用。具体的统计量取决于所选择的填充策略，例如均值、中位数、最频繁值等。

   下面是一个示例，展示了如何使用`SimpleImputer`的`fit`函数计算填充缺失值的统计量：

   ```python
   from sklearn.impute import SimpleImputer
   import pandas as pd
   
   # 创建一个示例DataFrame，包含缺失值
   data = {'A': [1, 2, None, 4],
           'B': [5, None, 7, 8],
           'C': [9, 10, 11, None]}
   df = pd.DataFrame(data)
   
   # 创建一个SimpleImputer对象，使用均值填充缺失值
   imputer = SimpleImputer(strategy='mean')
   
   # 计算填充缺失值的统计量
   imputer.fit(df)
   
   # 输出统计量
   print(imputer.statistics_)
   ```

   输出结果为：

   ```
   [2.33333333 6.66666667 10.        ]
   ```

   在上述示例中，我们首先创建了一个包含缺失值的DataFrame `df`。然后，创建了一个`SimpleImputer`对象，使用均值填充缺失值。接下来，使用`fit`函数对DataFrame进行拟合，计算均值作为填充缺失值的统计量。

   通过`statistics_`属性，我们可以访问计算得到的统计量。在本例中，`statistics_`是一个包含3个元素的数组，分别为'A'、'B'和'C'列的均值。

   请注意，`fit`函数仅用于计算填充缺失值的统计量，不会改变原始数据集。计算得到的统计量将在后续的`transform`函数中使用，用于对数据集进行填充操作。



#### Handling Text and Categorical Attributes

Now let's preprocess the categorical input feature, `ocean_proximity`:

```py
housing_cat = housing[["ocean_proximity"]]
housing_cat.head(10)
```

```py
from sklearn.preprocessing import OrdinalEncoder

ordinal_encoder = OrdinalEncoder()
housing_cat_encoded = ordinal_encoder.fit_transform(housing_cat)
housing_cat_encoded[:10]
```

```py
ordinal_encoder.categories_
```

```py
from sklearn.preprocessing import OneHotEncoder

cat_encoder = OneHotEncoder()
housing_cat_1hot = cat_encoder.fit_transform(housing_cat)
housing_cat_1hot
```

By default, the `OneHotEncoder` class returns a sparse array, but we can convert it to a dense array if needed by calling the `toarray()` method:

```py
housing_cat_1hot.toarray()
```

Alternatively, you can set `sparse=False` when creating the `OneHotEncoder`:

```py
cat_encoder = OneHotEncoder(sparse=False)
housing_cat_1hot = cat_encoder.fit_transform(housing_cat)
housing_cat_1hot
```

```py
cat_encoder.categories_
```

```py
from sklearn.preprocessing import OneHotEncoder

cat_encoder = OneHotEncoder()
housing_cat_1hot = cat_encoder.fit_transform(housing_cat)
housing_cat_1hot
```

By default, the `OneHotEncoder` class returns a sparse array, but we can convert it to a dense array if needed by calling the `toarray()` method:

```python
housing_cat_1hot.toarray()
```

Alternatively, you can set `sparse=False` when creating the `OneHotEncoder`:

```py
cat_encoder = OneHotEncoder(sparse=False)
housing_cat_1hot = cat_encoder.fit_transform(housing_cat)
housing_cat_1hot
```

```py
cat_encoder.categories_
```

1. `OrdinalEncoder`是scikit-learn库中的一个类，用于将分类变量转换为整数标签。它适用于有序的或有等级关系的分类变量，其中类别之间存在一种顺序或排序。

   `OrdinalEncoder`将每个不同的类别映射到一个整数值，从0开始递增。它可以用于将分类变量编码为机器学习算法可以直接处理的数值形式。

   下面是`OrdinalEncoder`的一般用法：

   ```python
   from sklearn.preprocessing import OrdinalEncoder
   
   encoder = OrdinalEncoder()
   encoded_data = encoder.fit_transform(data)
   ```

   参数说明：

   - `data`：要进行编码的数据集，可以是一个NumPy数组或Pandas DataFrame。

   `OrdinalEncoder`的`fit_transform`函数同时进行了拟合和转换操作。它会根据输入数据集中的类别，学习并生成一个映射规则，并将输入数据集转换为整数标签编码后的形式。

   下面是一个示例，展示了如何使用`OrdinalEncoder`对分类变量进行编码：

   ```python
   from sklearn.preprocessing import OrdinalEncoder
   import pandas as pd
   
   data = {'Category': ['Red', 'Blue', 'Green', 'Green', 'Red']}
   df = pd.DataFrame(data)
   
   encoder = OrdinalEncoder()
   encoded_data = encoder.fit_transform(df)
   
   print(encoded_data)
   ```

   输出结果为：

   ```
   [[2.]
    [0.]
    [1.]
    [1.]
    [2.]]
   ```

   在上述示例中，我们创建了一个包含分类变量的DataFrame `df`。然后，创建了一个`OrdinalEncoder`对象，并使用`fit_transform`函数对DataFrame进行编码转换。

   `encoded_data`是一个包含整数标签编码后数据的NumPy数组。在本例中，'Red'被编码为2，'Blue'被编码为0，'Green'被编码为1。

   需要注意的是，`OrdinalEncoder`要求输入数据的维度为二维。如果只有一列需要进行编码，需要将其转换为二维形式，例如使用`reshape(-1, 1)`。

   此外，对于具有无序或无等级关系的分类变量，`OrdinalEncoder`不适用。在这种情况下，可以考虑使用`OneHotEncoder`来进行独热编码。

2. `fit_transform()`方法是scikit-learn中许多预处理类的常用方法，它的作用是在一步中拟合数据并进行转换。

   具体来说，`fit_transform()`方法结合了两个步骤：

   1. **拟合（fit）**：通过观察输入数据，估计模型所需的内部参数或统计量。这些参数将根据输入数据的特征进行计算，用于后续的转换步骤。在拟合过程中，模型学习从数据中提取有用的信息。

   1. **转换（transform）**：根据拟合步骤中得到的参数，将输入数据转换为新的表示形式。转换的方式取决于具体的预处理操作，例如缩放、编码、降维等。转换过程将根据拟合步骤中学到的参数应用于输入数据，并生成转换后的数据。

   `fit_transform()`方法的优点是它可以在一次调用中完成拟合和转换，避免了多次遍历数据的开销。这对于在训练数据集上进行拟合并在相同的数据集上进行转换非常有效。然而，需要注意的是，在将模型应用于新的未见过的数据时，只需使用`transform()`方法进行转换，而不需要再次拟合。

   在`OrdinalEncoder`的例子中，`fit_transform()`方法用于拟合数据并将分类变量转换为整数标签编码。通过在一步中执行这两个操作，我们可以获取拟合后的编码结果，而无需额外的步骤。

   总结一下，`fit_transform()`方法是一个方便的方法，它结合了拟合和转换两个步骤，用于在一步中计算参数并将输入数据转换为新的表示形式。

3. `OneHotEncoder`是scikit-learn库中的一个类，用于将离散的分类变量转换为独热编码（One-Hot Encoding）。它适用于无序或无等级关系的分类变量，其中每个类别被视为一个独立的特征。

   独热编码是一种将分类变量表示为二进制向量的方法，其中每个类别被表示为一个唯一的二进制特征。对于给定的分类变量，如果它属于某个类别，则对应的二进制特征为1，否则为0。这种编码方式可以消除类别之间的偏序关系，并为机器学习算法提供更好的表示。

   下面是`OneHotEncoder`的一般用法：

   ```python
   from sklearn.preprocessing import OneHotEncoder
   
   encoder = OneHotEncoder()
   encoded_data = encoder.fit_transform(data)
   ```

   参数说明：

   - `data`：要进行编码的数据集，可以是一个NumPy数组或Pandas DataFrame。

   `OneHotEncoder`的`fit_transform`方法同时进行了拟合和转换操作。它会根据输入数据集中的类别，学习并生成一个独热编码的映射规则，并将输入数据集转换为独热编码后的形式。

   下面是一个示例，展示了如何使用`OneHotEncoder`对分类变量进行独热编码：

   ```python
   from sklearn.preprocessing import OneHotEncoder
   import pandas as pd
   
   data = {'Category': ['Red', 'Blue', 'Green', 'Green', 'Red']}
   df = pd.DataFrame(data)
   
   encoder = OneHotEncoder()
   encoded_data = encoder.fit_transform(df)
   
   print(encoded_data.toarray())
   ```

   输出结果为：

   ```
   [[0. 0. 1.]
    [1. 0. 0.]
    [0. 1. 0.]
    [0. 1. 0.]
    [0. 0. 1.]]
   ```

   在上述示例中，我们创建了一个包含分类变量的DataFrame `df`。然后，创建了一个`OneHotEncoder`对象，并使用`fit_transform`方法对DataFrame进行独热编码转换。

   `encoded_data`是一个稀疏矩阵（`scipy.sparse.csr_matrix`格式），表示经过独热编码后的数据。通过`toarray()`方法，我们可以将其转换为密集矩阵形式。

   在本例中，'Red'被编码为 \[0, 0, 1\]，'Blue'被编码为 \[1, 0, 0\]，'Green'被编码为 \[0, 1, 0\]。

   需要注意的是，`OneHotEncoder`要求输入数据的维度为二维。如果只有一列需要进行编码，需要将其转换为二维形式，例如使用`reshape(-1, 1)`。

   另外，如果输入数据中存在未见过的类别，在转换后的独热编码中将会添加新的列。如果需要对新的数据进行编码，可以使用`transform`方法，而无需再次拟合。

4. `OrdinalEncoder`和`OneHotEncoder`是用于对分类变量进行编码的两种不同方法，它们的区别在于编码的表示形式和处理方式。

   1. **编码表示形式**：`OrdinalEncoder`将分类变量编码为整数标签，其中每个类别被映射到一个整数值。它适用于有序的或有等级关系的分类变量，其中类别之间存在一种顺序或排序。`OneHotEncoder`将分类变量编码为独热编码，其中每个类别被表示为一个唯一的二进制特征。它适用于无序或无等级关系的分类变量，其中每个类别被视为一个独立的特征。

   1. **处理方式**：`OrdinalEncoder`通过为每个类别分配一个整数值来表示类别之间的顺序或排序。这种编码方式保留了类别之间的顺序信息，但在某些情况下可能会引入一种错误的偏序关系。例如，如果将"Red"编码为0，"Green"编码为1，"Blue"编码为2，则会创建一个假象的有序关系，即"Blue" > "Green" > "Red"。相反，`OneHotEncoder`将每个类别表示为一个独立的二进制特征，通过二进制向量的方式消除了类别之间的偏序关系。每个类别对应的特征只有一个位置是1，其他位置都是0。

   1. **数据表示形式**：`OrdinalEncoder`的输出是整数标签编码后的数据，通常以NumPy数组或Pandas DataFrame的形式表示。每个类别被表示为一个整数值。相比之下，`OneHotEncoder`的输出是经过独热编码的数据，通常以稀疏矩阵（sparse matrix）或密集矩阵（dense matrix）的形式表示。每个类别被表示为一个二进制特征，并且在矩阵中占据一个位置。

   选择使用哪种编码方式取决于数据的性质和机器学习算法的要求。如果类别之间存在一种顺序或排序关系，可以使用`OrdinalEncoder`来保留这种信息。如果类别之间没有明确的顺序关系，或者需要将分类变量表示为独立的特征，可以使用`OneHotEncoder`进行独热编码。

5. `toarray()`函数是用于将稀疏矩阵（sparse matrix）转换为密集矩阵（dense matrix）的方法。稀疏矩阵是一种数据结构，用于表示大多数元素为零的矩阵，而密集矩阵则是一种常规的二维数组表示。

   在机器学习中，一些操作和算法可能需要使用密集矩阵作为输入，而不是稀疏矩阵。因此，当我们使用某些函数或方法生成的结果是稀疏矩阵时，可以使用`toarray()`函数将其转换为密集矩阵。

   对于稀疏矩阵对象，例如`scipy.sparse.csr_matrix`，`toarray()`方法可以应用于该对象，将其转换为一个常规的NumPy数组（即密集矩阵）。转换后，数组将包含与稀疏矩阵相同的元素，但以常规数组的形式呈现。

   以下是一个示例，演示如何使用`toarray()`函数将稀疏矩阵转换为密集矩阵：

   ```python
   import numpy as np
   from scipy.sparse import csr_matrix
   
   sparse_matrix = csr_matrix([[0, 1, 0], [1, 0, 0], [0, 0, 1]])
   dense_matrix = sparse_matrix.toarray()
   
   print(dense_matrix)
   ```

   输出结果为：

   ```
   [[0 1 0]
    [1 0 0]
    [0 0 1]]
   ```

   在上述示例中，我们首先创建了一个稀疏矩阵对象`sparse_matrix`，它表示一个3x3的矩阵。然后，我们使用`toarray()`方法将稀疏矩阵转换为密集矩阵，并将结果存储在`dense_matrix`中。最后，我们打印出密集矩阵的内容。

   需要注意的是，稀疏矩阵转换为密集矩阵可能会占用更多的内存空间，因为密集矩阵存储了所有元素，包括零元素。因此，在处理大型矩阵时，应考虑内存消耗的问题，并确保是否真正需要将稀疏矩阵转换为密集矩阵。

6. `categories()`函数是用于获取`OneHotEncoder`对象中学习到的类别信息的方法。它返回编码器中每个特征的类别列表。

   当我们使用`fit_transform()`方法对数据进行编码时，`OneHotEncoder`会学习数据中每个特征的类别，并将其存储在编码器对象中。然后，我们可以使用`categories()`函数来检索这些类别信息。

   下面是一个示例，展示了如何使用`categories()`函数获取类别信息：

   ```python
   from sklearn.preprocessing import OneHotEncoder
   import pandas as pd
   
   data = {'Category': ['Red', 'Blue', 'Green', 'Green', 'Red']}
   df = pd.DataFrame(data)
   
   encoder = OneHotEncoder()
   encoded_data = encoder.fit_transform(df)
   
   categories = encoder.categories_
   
   print(categories)
   ```

   输出结果为：

   ```
   [array(['Blue', 'Green', 'Red'], dtype=object)]
   ```

   在上述示例中，我们创建了一个包含分类变量的DataFrame `df`。然后，创建了一个`OneHotEncoder`对象，并使用`fit_transform`方法对DataFrame进行独热编码转换。

   `categories`是一个列表，其中每个元素对应一个特征的类别。在本例中，只有一个特征"Category"，因此`categories`列表中只有一个元素。该元素是一个NumPy数组，包含了特征"Category"的类别信息。在这个例子中，类别列表为`['Blue', 'Green', 'Red']`。

   通过`categories()`函数，我们可以获取每个特征的类别信息，并了解编码器学习到的类别顺序。这对于后续的数据转换和分析非常有用。



#### Custom Transformers

Let's create a custom transformer to add extra attributes:

```py
from sklearn.base import BaseEstimator, TransformerMixin

# column index
rooms_ix, bedrooms_ix, population_ix, households_ix = 3, 4, 5, 6

class CombinedAttributesAdder(BaseEstimator, TransformerMixin):
    def __init__(self, add_bedrooms_per_room=True): # no *args or **kargs
        self.add_bedrooms_per_room = add_bedrooms_per_room
    def fit(self, X, y=None):
        return self  # nothing else to do
    def transform(self, X):
        rooms_per_household = X[:, rooms_ix] / X[:, households_ix]
        population_per_household = X[:, population_ix] / X[:, households_ix]
        if self.add_bedrooms_per_room:
            bedrooms_per_room = X[:, bedrooms_ix] / X[:, rooms_ix]
            return np.c_[X, rooms_per_household, population_per_household,
                         bedrooms_per_room]
        else:
            return np.c_[X, rooms_per_household, population_per_household]

attr_adder = CombinedAttributesAdder(add_bedrooms_per_room=False)
housing_extra_attribs = attr_adder.transform(housing.values)
```

Note that I hard coded the indices (3, 4, 5, 6) for concision and clarity in the book, but it would be much cleaner to get them dynamically, like this:

```py
col_names = "total_rooms", "total_bedrooms", "population", "households"
rooms_ix, bedrooms_ix, population_ix, households_ix = [
    housing.columns.get_loc(c) for c in col_names] # get the column indices
```

Also, `housing_extra_attribs` is a NumPy array, we've lost the column names (unfortunately, that's a problem with Scikit-Learn). To recover a `DataFrame`, you could run this:

```py
housing_extra_attribs = pd.DataFrame(
    housing_extra_attribs,
    columns=list(housing.columns)+["rooms_per_household", "population_per_household"],
    index=housing.index)
housing_extra_attribs.head()
```

1. `columns.get_loc()`函数是用于获取DataFrame中指定列的索引位置。它返回指定列的整数位置索引，可以用于在DataFrame中访问、修改或删除该列的数据。

   具体来说，`columns`是DataFrame对象的属性，它返回一个Index对象，其中包含了DataFrame的列标签。`get_loc()`方法是Index对象的方法，用于获取指定元素（列标签）的整数位置索引。

   下面是一个示例，展示了如何使用`columns.get_loc()`函数获取列的索引位置：

   ```python
   import pandas as pd
   
   data = {'Name': ['Alice', 'Bob', 'Charlie'],
           'Age': [25, 30, 35],
           'City': ['New York', 'London', 'Paris']}
   
   df = pd.DataFrame(data)
   
   column_index = df.columns.get_loc('Age')
   
   print(column_index)
   ```

   输出结果为：

   ```
   1
   ```

   在上述示例中，我们创建了一个包含姓名、年龄和城市的DataFrame `df`。然后，我们使用`columns.get_loc()`方法来获取列标签为'Age'的列的索引位置，并将结果存储在`column_index`变量中。最后，我们打印出`column_index`的值，即该列的索引位置。

   `get_loc()`函数对于需要根据列标签进行列操作的情况非常有用。例如，我们可以使用索引位置来选择特定列的数据：

   ```python
   age_column = df.iloc[:, column_index]
   
   print(age_column)
   ```

   输出结果为：

   ```
   0    25
   1    30
   2    35
   Name: Age, dtype: int64
   ```

   在上述示例中，我们使用`iloc`属性和列索引位置来选择DataFrame中的'Age'列，并将其存储在`age_column`变量中。然后，我们打印出`age_column`的值，即'Age'列的数据。

   总而言之，`columns.get_loc()`函数允许我们根据列标签获取列的索引位置，从而方便地进行列操作和数据访问。



#### Transformation Pipelines

Now let's build a pipeline for preprocessing the numerical attributes:py

```py
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler

num_pipeline = Pipeline([
        ('imputer', SimpleImputer(strategy="median")),
        ('attribs_adder', CombinedAttributesAdder()),
        ('std_scaler', StandardScaler()),
    ])

housing_num_tr = num_pipeline.fit_transform(housing_num)
```

```py
housing_num_tr
```

```py
from sklearn.compose import ColumnTransformer

num_attribs = list(housing_num)
cat_attribs = ["ocean_proximity"]

full_pipeline = ColumnTransformer([
        ("num", num_pipeline, num_attribs),
        ("cat", OneHotEncoder(), cat_attribs),
    ])

housing_prepared = full_pipeline.fit_transform(housing)
```

```py
housing_prepared
```

```py
housing_prepared.shape
```

For reference, here is the old solution based on a `DataFrameSelector` transformer (to just select a subset of the Pandas `DataFrame` columns), and a `FeatureUnion`:

```py
from sklearn.base import BaseEstimator, TransformerMixin

# Create a class to select numerical or categorical columns 
class OldDataFrameSelector(BaseEstimator, TransformerMixin):
    def __init__(self, attribute_names):
        self.attribute_names = attribute_names
    def fit(self, X, y=None):
        return self
    def transform(self, X):
        return X[self.attribute_names].values
```

Now let's join all these components into a big pipeline that will preprocess both the numerical and the categorical features:

```py
num_attribs = list(housing_num)
cat_attribs = ["ocean_proximity"]

old_num_pipeline = Pipeline([
        ('selector', OldDataFrameSelector(num_attribs)),
        ('imputer', SimpleImputer(strategy="median")),
        ('attribs_adder', CombinedAttributesAdder()),
        ('std_scaler', StandardScaler()),
    ])

old_cat_pipeline = Pipeline([
        ('selector', OldDataFrameSelector(cat_attribs)),
        ('cat_encoder', OneHotEncoder(sparse=False)),
    ])
```

```py
from sklearn.pipeline import FeatureUnion

old_full_pipeline = FeatureUnion(transformer_list=[
        ("num_pipeline", old_num_pipeline),
        ("cat_pipeline", old_cat_pipeline),
    ])
```

```py
old_housing_prepared = old_full_pipeline.fit_transform(housing)
old_housing_prepared
```

The result is the same as with the `ColumnTransformer`:

```py
np.allclose(housing_prepared, old_housing_prepared)
```



## Select and Train a Model

#### Training and Evaluating on the Training Set

```py
from sklearn.linear_model import LinearRegression

lin_reg = LinearRegression()
lin_reg.fit(housing_prepared, housing_labels)
```

```py
# let's try the full preprocessing pipeline on a few training instances
some_data = housing.iloc[:5]
some_labels = housing_labels.iloc[:5]
some_data_prepared = full_pipeline.transform(some_data)

print("Predictions:", lin_reg.predict(some_data_prepared))
```

Compare against the actual values:

```py
print("Labels:", list(some_labels))
```

```py
some_data_prepared
```

```py
from sklearn.metrics import mean_squared_error

housing_predictions = lin_reg.predict(housing_prepared)
lin_mse = mean_squared_error(housing_labels, housing_predictions)
lin_rmse = np.sqrt(lin_mse)
lin_rmse
```

**Note**: since Scikit-Learn 0.22, you can get the RMSE directly by calling the `mean_squared_error()` function with `squared=False`.

```py
from sklearn.metrics import mean_absolute_error

lin_mae = mean_absolute_error(housing_labels, housing_predictions)
lin_mae
```

```py
from sklearn.tree import DecisionTreeRegressor

tree_reg = DecisionTreeRegressor(random_state=42)
tree_reg.fit(housing_prepared, housing_labels)
```

```py
housing_predictions = tree_reg.predict(housing_prepared)
tree_mse = mean_squared_error(housing_labels, housing_predictions)
tree_rmse = np.sqrt(tree_mse)
tree_rmse
```

#### Better Evaluation Using Cross-Validation

```py
from sklearn.model_selection import cross_val_score

scores = cross_val_score(tree_reg, housing_prepared, housing_labels,
                         scoring="neg_mean_squared_error", cv=10)
tree_rmse_scores = np.sqrt(-scores)
```

```py
def display_scores(scores):
    print("Scores:", scores)
    print("Mean:", scores.mean())
    print("Standard deviation:", scores.std())

display_scores(tree_rmse_scores)
```

```py
lin_scores = cross_val_score(lin_reg, housing_prepared, housing_labels,
                             scoring="neg_mean_squared_error", cv=10)
lin_rmse_scores = np.sqrt(-lin_scores)
display_scores(lin_rmse_scores)
```

Note: we specify n_estimators=100 to be future-proof since the default value is going to change to 100 in Scikit-Learn 0.22 (for simplicity, this is not shown in the book).

```py
from sklearn.ensemble import RandomForestRegressor

forest_reg = RandomForestRegressor(n_estimators=100, random_state=42)
forest_reg.fit(housing_prepared, housing_labels)
```

```py
housing_predictions = forest_reg.predict(housing_prepared)
forest_mse = mean_squared_error(housing_labels, housing_predictions)
forest_rmse = np.sqrt(forest_mse)
forest_rmse
```

```py
from sklearn.model_selection import cross_val_score

forest_scores = cross_val_score(forest_reg, housing_prepared, housing_labels,
                                scoring="neg_mean_squared_error", cv=10)
forest_rmse_scores = np.sqrt(-forest_scores)
display_scores(forest_rmse_scores)
```

```py
scores = cross_val_score(lin_reg, housing_prepared, housing_labels, scoring="neg_mean_squared_error", cv=10)
pd.Series(np.sqrt(-scores)).describe()
```

```py
from sklearn.svm import SVR

svm_reg = SVR(kernel="linear")
svm_reg.fit(housing_prepared, housing_labels)
housing_predictions = svm_reg.predict(housing_prepared)
svm_mse = mean_squared_error(housing_labels, housing_predictions)
svm_rmse = np.sqrt(svm_mse)
svm_rmse
```

## Fine-Tune Your Model

#### Grid Search

```py
from sklearn.model_selection import GridSearchCV

param_grid = [
    # try 12 (3×4) combinations of hyperparameters
    {'n_estimators': [3, 10, 30], 'max_features': [2, 4, 6, 8]},
    # then try 6 (2×3) combinations with bootstrap set as False
    {'bootstrap': [False], 'n_estimators': [3, 10], 'max_features': [2, 3, 4]},
  ]

forest_reg = RandomForestRegressor(random_state=42)
# train across 5 folds, that's a total of (12+6)*5=90 rounds of training 
grid_search = GridSearchCV(forest_reg, param_grid, cv=5,
                           scoring='neg_mean_squared_error',
                           return_train_score=True)
grid_search.fit(housing_prepared, housing_labels)
```

The best hyperparameter combination found:

```py
grid_search.best_params_
```

```py
grid_search.best_estimator_
```

Let's look at the score of each hyperparameter combination tested during the grid search:

```py
cvres = grid_search.cv_results_
for mean_score, params in zip(cvres["mean_test_score"], cvres["params"]):
    print(np.sqrt(-mean_score), params)
```

```py
pd.DataFrame(grid_search.cv_results_)
```

#### Randomized Search

```py
from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import randint

param_distribs = {
        'n_estimators': randint(low=1, high=200),
        'max_features': randint(low=1, high=8),
    }

forest_reg = RandomForestRegressor(random_state=42)
rnd_search = RandomizedSearchCV(forest_reg, param_distributions=param_distribs,
                                n_iter=10, cv=5, scoring='neg_mean_squared_error', random_state=42)
rnd_search.fit(housing_prepared, housing_labels)
```

```py
cvres = rnd_search.cv_results_
for mean_score, params in zip(cvres["mean_test_score"], cvres["params"]):
    print(np.sqrt(-mean_score), params)
```

#### Analyze the Best Models and Their Errors

```py
feature_importances = grid_search.best_estimator_.feature_importances_
feature_importances
```

```py
extra_attribs = ["rooms_per_hhold", "pop_per_hhold", "bedrooms_per_room"]
#cat_encoder = cat_pipeline.named_steps["cat_encoder"] # old solution
cat_encoder = full_pipeline.named_transformers_["cat"]
cat_one_hot_attribs = list(cat_encoder.categories_[0])
attributes = num_attribs + extra_attribs + cat_one_hot_attribs
sorted(zip(feature_importances, attributes), reverse=True)
```

#### Evaluate Your System on the Test Set

```py
final_model = grid_search.best_estimator_

X_test = strat_test_set.drop("median_house_value", axis=1)
y_test = strat_test_set["median_house_value"].copy()

X_test_prepared = full_pipeline.transform(X_test)
final_predictions = final_model.predict(X_test_prepared)

final_mse = mean_squared_error(y_test, final_predictions)
final_rmse = np.sqrt(final_mse)
```

```py
final_rmse
```

We can compute a 95% confidence interval for the test RMSE:

```py
from scipy import stats

confidence = 0.95
squared_errors = (final_predictions - y_test) ** 2
np.sqrt(stats.t.interval(confidence, len(squared_errors) - 1,
                         loc=squared_errors.mean(),
                         scale=stats.sem(squared_errors)))
```

We could compute the interval manually like this:

```py
m = len(squared_errors)
mean = squared_errors.mean()
tscore = stats.t.ppf((1 + confidence) / 2, df=m - 1)
tmargin = tscore * squared_errors.std(ddof=1) / np.sqrt(m)
np.sqrt(mean - tmargin), np.sqrt(mean + tmargin)
```

Alternatively, we could use a z-scores rather than t-scores:

```py
zscore = stats.norm.ppf((1 + confidence) / 2)
zmargin = zscore * squared_errors.std(ddof=1) / np.sqrt(m)
np.sqrt(mean - zmargin), np.sqrt(mean + zmargin)
```

