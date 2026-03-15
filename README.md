# Android 布局基础演示

## 简介

本 Demo 演示 Android 布局的基本概念，展示如何使用 include 标签复用布局。

## 基本原理

Android 布局是 UI 开发的基础，通过不同的布局管理器可以控制子元素的排列方式。良好的布局设计可以提高代码复用性和可维护性。

常用的布局类型：

1. **LinearLayout（线性布局）**
   - 按方向（水平/垂直）依次排列子元素
   - 支持权重（weight）分配空间

2. **RelativeLayout（相对布局）**
   - 子元素相对于父容器或其他元素定位
   - 可以实现复杂的 UI 结构

3. **ConstraintLayout（约束布局）**
   - 通过约束关系定位元素
   - 支持链式布局和百分比布局
   - 推荐作为首选布局

4. **FrameLayout（帧布局）**
   - 所有子元素叠放在左上角
   - 适合实现叠加效果

5. **GridLayout（网格布局）**
   - 使用行列网格定位元素
   - 支持跨行跨列

## 启动和使用

### 环境要求
- Android Studio
- JDK 17
- Gradle 8.x

### 安装和运行

1. 用 Android Studio 打开项目
2. 连接 Android 设备或模拟器
3. 点击 Run 运行

### 使用方法
- 运行后将看到由多个布局文件组合而成的界面

## 教程

### 什么是布局？

布局（Layout）定义了 UI 界面的结构，决定了各个视图（View）在屏幕上的排列方式。Android 提供了多种布局容器，每种都有其适用场景。

### include 标签

include 标签用于在布局中引用其他布局文件，实现布局复用。这是 Android 布局的重要特性，可以将重复的 UI 组件抽取为独立文件。

基本用法：

```xml
<include layout="@layout/layout_header" />
```

这样可以将 layout_header.xml 的内容嵌入到当前布局中。

### 创建可复用布局

1. 创建独立布局文件（如 layout_header.xml）：

```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Header"
    android:textSize="24sp"
    android:gravity="center"
    android:padding="16dp" />
```

2. 在主布局中使用 include：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <!-- 引用头部布局 -->
    <include layout="@layout/layout_header" />

    <!-- 引用内容布局 -->
    <include layout="@layout/layout_content" />

</LinearLayout>
```

### merge 标签

merge 标签用于减少布局层级，通常与 include 配合使用。当被 include 的布局根元素是 merge 时，会将其子元素直接添加到父容器中。

```xml
<!-- layout_header.xml -->
<merge xmlns:android="http://schemas.android.com/apk/res/android">
    <TextView ... />
    <Button ... />
</merge>
```

### 选择合适的布局

- **简单列表**：使用 LinearLayout
- **需要相对定位**：使用 RelativeLayout 或 ConstraintLayout
- **复杂网格**：使用 GridLayout 或 ConstraintLayout
- **需要居中叠加**：使用 FrameLayout

### 注意事项

1. **避免嵌套过深**：嵌套多层布局会影响性能，优先使用 ConstraintLayout
2. **合理使用 include**：将重复的 UI 组件抽取为独立布局
3. **使用 merge**：减少不必要的布局层级
4. **ConstraintLayout**：复杂布局优先使用 ConstraintLayout

## 关键代码详解

### activity_main.xml（主布局）

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- 根布局：垂直线性布局 -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <!-- 引用头部布局：复用 layout_header.xml -->
    <include layout="@layout/layout_header" />

    <!-- 引用内容布局：复用 layout_content.xml -->
    <include layout="@layout/layout_content" />

</LinearLayout>
```

### layout_header.xml（头部布局）

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- 头部 TextView -->
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Header"
    android:textSize="24sp"
    android:gravity="center"
    android:padding="16dp" />
```

### layout_content.xml（内容布局）

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- 内容 TextView -->
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Content"
    android:textSize="18sp"
    android:padding="16dp" />
```

### MainActivity.kt

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // 设置布局：加载 activity_main.xml
        // 其中包含的 include 标签会自动加载对应的布局文件
        setContentView(R.layout.activity_main)
    }
}
```
