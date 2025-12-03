# 🟦 **1. Painter 绘图（Painting）**

`Painter` 是 egui 提供的**低级绘制接口**，你可以在任何容器里获取 `Painter` 对象，然后绘制图形。

### 常用方法

```rust
ui.painter().line_segment([pos1, pos2], Stroke::new(2.0, Color32::RED));
ui.painter().rect(Rect::from_min_size(pos, size), corner_radius, fill_color, stroke);
ui.painter().circle_filled(center, radius, fill_color);
ui.painter().text(pos, Align2::CENTER_CENTER, "Hello", FontId::default(), Color32::WHITE);
```

* `line_segment` → 绘制直线
* `rect` → 绘制矩形，可以带圆角
* `circle_filled` → 绘制实心圆
* `text` → 绘制文字
* `fill_color` → 填充颜色
* `stroke` → 边框颜色和粗细

---

# 🟦 **2. 布局容器**

1. **CentralPanel** → 主区域
2. **TopPanel / BottomPanel / SidePanel** → 工具栏或侧边栏
3. **Window** → 可移动、可关闭窗口
4. **Area** → 自由浮动区域

布局控制方法：

```rust
ui.horizontal(|ui| { /* 水平排列 */ });
ui.vertical(|ui| { /* 竖直排列 */ });
Grid::new("my_grid").show(ui, |ui| { /* 表格排列 */ });
ui.add_space(10.0); // 增加空白
ui.spacing_mut().item_spacing = vec2(5.0, 5.0); // 控件间距
ui.expand_to_fill(); // 占满父容器剩余空间
```

* `horizontal` / `vertical` → 简单排列
* `Grid` → 表格排列
* `add_space` → 增加空白，用于分隔控件
* `spacing_mut()` → 修改控件间距
* `expand_to_fill()` → 控件占满父容器剩余空间

---

# 🟦 **3. 自定义控件（Custom Widgets）**

egui 的控件是可组合的，你可以：

1. **组合已有控件** → 把几个控件封装成一个新的功能控件
2. **绘制自定义图形** → 用 Painter 绘制按钮、仪表盘、进度动画

### 示例：自定义旋转按钮

```rust
use egui::{Response, Sense, Ui, Vec2, Color32, Stroke};

fn rotating_button(ui: &mut Ui, angle: f32) -> Response {
    let size = Vec2::splat(40.0);
    let (rect, response) = ui.allocate_exact_size(size, Sense::click());

    // 绘制旋转箭头
    let painter = ui.painter();
    let center = rect.center();
    let radius = 15.0;
    let end = center + egui::vec2(angle.cos(), angle.sin()) * radius;
    painter.line_segment([center, end], Stroke::new(2.0, Color32::WHITE));

    response
}
```

* `ui.allocate_exact_size` → 为控件预留空间
* `Painter` → 绘制控件外观
* 返回 `Response` → 处理点击、悬停等交互

> 这样你就可以创建 **完全自定义外观的控件**，甚至可以组合多个控件和绘图。

---

# 🟦 **4. 应用场景**

* 仪表盘 / 转盘 / 进度动画
* 游戏 UI（血条、能量条）
* 自定义图标按钮
* 高级动画控件（带旋转、缩放、颜色渐变）

Wed Dec  3 02:14:54 PM CST 2025
