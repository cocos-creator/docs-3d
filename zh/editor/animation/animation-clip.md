# 编辑动画序列

在节点上挂载了动画剪辑后，点击`进入动画编辑模式`就可以进入动画编辑模式了，之后便可以在动画剪辑中创建一些动画帧数据。

首先需要了解一下动画属性，动画属性包括了节点自有的 `position`、`rotation` 等属性，也包含了组件 Component 中自定义的属性。
组件包含的属性前会加上组件的名字，比如 `cc.Sprite.spriteFrame`。
属性轨道上对应的蓝色棱形就是关键帧。

Animation（动画） 组件可以以动画方式驱动所在节点和子节点上的节点和组件属性，包括用户自定义脚本中的属性。根据这个特性，可以灵活实现各种动画需求。具体的动画实现依不同的动画需求，步骤不同，案例可以参考官方的 example-3d.这里主要介绍一些常见的编辑操作方法，便于快速的编辑实现效果

## 关键帧常见操作

### 选中关键帧
点击我们创建的关键帧后关键帧会呈现选中状态，此时关键帧由蓝变白，目前有以下方式可以选中
- 右键点击关键帧即可选中，按下 Ctrl 再右击可多选
- 直接在关键帧区域拖动框选关键帧

### 添加关键帧
- 选中对应节点和对应的属性，移动时间控制线到需要添加关键帧的位置，按下 enter 键
- 移动时间控制线到需要添加关键帧的位置，在对应的属性列表项里，点击 ![添加关键帧按钮](animation-clip/add-key-button.png)即可
- 在对应的属性轨道位置上右键，选择`添加关键帧`
- 添加属性轨道后，直接在属性检查器的对于位置修改属性即可自动生成关键帧（如果是位置等亦可以在场景内直接拖拽）

### 移除关键帧
- 选中需要删除的关键帧，按下 delete / Cmd + backspace 键
- 在需要删除的关键帧位置右键，弹出菜单后，选中`移除关键帧`
- 拖动时间控制线到需要移除关键帧的位置或者直接双击关键帧后，在对应的属性列表项里，点击 ![移除关键帧按钮](animation-clip/del-key-button.png)即可

### 修改关键帧数据
在时间轴上双击需要修改的关键帧，时间控制线将会移动到该位置或者直接拖动时间控制线，直接在 **属性检查器** 内修改相对应的属性即可（确保动画编辑器处于编辑状态）。例如属性列表中有 position、x、y 三个属性轨道，选中关键帧之后，则可以修改 **属性检查器** 中的 position、x、y 属性。

在动画编辑模式下，将时间控制线移动到时间轴上没有关键帧的位置，然后在属性检查器中修改相对应的属性，也会自动插入一帧。

### 移动关键帧
- 选中关键帧后，在选中的关键帧上后右键按住不放进行拖动，松开即移动完成
移动过程中会有移动距离和最终位置帧数的提示![移除关键帧按钮](animation-clip/move-tips.png)

### 复制/粘贴关键帧
- 选中关键帧后，按照常规快捷键 C / V 即可进行复制粘贴
- 选中关键帧后，在选中的关键帧上右键，选择`复制关键帧`，之后选择其他位置右键，选择`粘贴关键帧`即可
- 选中关键帧后，按下 Alt 键，在选中的关键帧上按住不放进行拖动，松开鼠标后关键帧将会复制到移动的对应位置

## 属性轨道数据常见操作

一个动画剪辑内可能包含了多个节点，每个节点上挂载多个动画属性，每个属性内的数据才是实际的关键帧。
### 添加属性轨道
- 点击属性列表旁边的 `+` 小按钮，弹出可添加的属性菜单后，点击需要添加的属性即可

### 移除属性轨道
- 右键点击属性列表项，选择移除属性轨道

### 清空轨道数据
-  右键点击属性列表项，选择清空属性轨道

## 节点数据常见操作

动画剪辑通过节点的名字定义数据的位置，本身忽略了根节点，其余的子节点通过与根节点的**相对路径**索引找到对应的数据。

### 清空节点数据
- 在动画编辑器的节点项位置右键，选择`清空数据`，在弹窗提示后选择`清除`即可

### 迁移节点数据
有时候我们会在制作完成动画后，将节点重命名，这样会造成动画数据所以出现问题，如下图：
![丢失节点图示](animation/missing_node.png)

这时候我们可以在丢失节点上右键点击`迁移数据`，之后再去点击其他节点，将数据迁移上去。如果点击迁移数据后不想迁移了，直接在时间轴区域点击或者是在点击其他节点后的弹窗点击取消即可。
![迁移节点图示](animation/moving_node.gif)

## 修改 clip 常见属性

**sample**： 定义当前动画数据每秒的帧率，默认为 60，这个参数会影响时间轴上每两个整数秒刻度之间的帧数量（也就是两秒之内有多少格）。

**speed**： 当前动画的播放速度，默认为 1。

**duration**： 当动画播放速度为 1 的时候，动画的持续时间。

**real time**： 动画从开始播放到结束，真正持续的时间，对应编辑器右下角括号内的数字。

**wrap mode**： 循环模式。

修改对应属性后，焦点离开后即生效。