# matplotlib 基础绘图

## 基础折线图

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y, label="sin(x)", color="blue", linewidth=2)
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("Basic Line Plot")
plt.legend()
plt.show()
```

## 图像属性设置

### 坐标范围与刻度

```python
plt.plot(x, y)
plt.xlim(0, 10)
plt.ylim(-1.5, 1.5)
plt.xticks([0, 2, 4, 6, 8, 10], ["0", "2π", "4π", "6π", "8π", "10π"])
plt.show()
```

### 图例和标题

```python
plt.plot(x, y, label="sin(x)")
plt.title("Sine Function")
plt.legend(loc="upper right")
plt.show()
```

### 注释

```python
plt.plot(x, y)
plt.annotate(
    "Local Max",
    xy=(np.pi / 2, 1),
    xytext=(1, 1.2),
    arrowprops=dict(facecolor="black", arrowstyle="->")
)
plt.show()
```

## 子图

### 简单子图

```python
plt.subplot(2, 2, 1)
plt.plot(x, np.sin(x))
plt.title("sin(x)")

plt.subplot(2, 2, 2)
plt.plot(x, np.cos(x))
plt.title("cos(x)")

plt.subplot(2, 2, 3)
plt.bar([1, 2, 3], [3, 4, 5])
plt.title("Bar Chart")

plt.subplot(2, 2, 4)
plt.scatter(np.random.rand(10), np.random.rand(10))
plt.title("Scatter Plot")

plt.tight_layout()
plt.show()
```

### 灵活子图布局

```python
fig, ax = plt.subplots(2, 3, figsize=(10, 6))
ax[0, 0].plot(x, np.sin(x))
ax[0, 1].bar([1, 2, 3], [4, 5, 6])
ax[0, 2].scatter([1, 2, 3], [3, 4, 5])
plt.show()
```

## 常见图表类型

### 散点图

```python
x = np.random.rand(50)
y = np.random.rand(50)
sizes = np.random.rand(50) * 1000
colors = np.random.rand(50)

plt.scatter(x, y, s=sizes, c=colors, alpha=0.6, cmap="viridis")
plt.colorbar()
plt.title("Scatter Plot")
plt.show()
```

### 直方图

```python
data = np.random.randn(1000)
plt.hist(data, bins=30, color="blue", alpha=0.7)
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.title("Histogram")
plt.show()
```

### 条形图

```python
labels = ["A", "B", "C", "D"]
values = [10, 20, 15, 25]

plt.bar(labels, values, color="green")
plt.title("Bar Chart")
plt.show()
```

### 等高线图

```python
x = np.linspace(-3, 3, 100)
y = np.linspace(-3, 3, 100)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))

plt.contourf(X, Y, Z, levels=20, cmap="RdGy")
plt.colorbar()
plt.title("Contour Plot")
plt.show()
```

### 极坐标图

```python
theta = np.linspace(0, 2 * np.pi, 100)
r = 1 + np.sin(4 * theta)

ax = plt.subplot(projection="polar")
ax.plot(theta, r)
plt.title("Polar Plot")
plt.show()
```

## 组合图表

### 填充图

```python
y1 = np.sin(x)
y2 = np.cos(x)

plt.fill_between(x, y1, y2, color="lightblue", alpha=0.5)
plt.title("Fill Between Sin and Cos")
plt.show()
```

### 饼图

```python
labels = ["A", "B", "C", "D"]
sizes = [15, 30, 45, 10]
explode = (0.1, 0, 0, 0)

plt.pie(sizes, labels=labels, explode=explode, autopct="%1.1f%%", shadow=True)
plt.title("Pie Chart")
plt.show()
```

## 高级图表

### 热力图

```python
data = np.random.rand(10, 10)
plt.imshow(data, cmap="hot", interpolation="nearest")
plt.colorbar()
plt.title("Heatmap")
plt.show()
```

### 箱线图

```python
data = [np.random.randn(100), np.random.randn(100)]
plt.boxplot(data, labels=["Group 1", "Group 2"])
plt.title("Box Plot")
plt.show()
```

## 保存图像

```python
plt.plot(x, y)
plt.title("Save Example")
plt.savefig("plot.png", dpi=300, bbox_inches="tight")
plt.show()
```

<!-- learning-journey:update-history:start -->
## 更新记录

| 日期 | 类型 | 说明 |
| --- | --- | --- |
| 2026-07-23 | 首次发布 | 整理 matplotlib 基础绘图、子图、常见图表和图像保存方法 |
<!-- learning-journey:update-history:end -->
