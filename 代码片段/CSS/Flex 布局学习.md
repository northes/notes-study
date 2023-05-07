
![](assets/Pasted%20image%2020230507150243.png)

- 主轴（main axis）：如果子元素沿X轴排列，那么X轴为主轴，Y轴为交叉轴（cross axis）。如果子元素沿Y轴排列，那么Y轴为主轴，X轴为交叉轴
- 同理，子元素的大小也不以长宽论，子元素的大小以占主轴、交叉轴的长短来计算


❗全部基于 `tailwindcss` 进行学习，原生 css 配置一样

# 设置在父对象

## 默认



![](assets/Pasted%20image%2020230507152129.png)

```html
<div class="bg-amber-600 w-96">  
	<div class="bg-blue-500 h-16 w-56">1</div>  
	<div class="bg-blue-500 h-16 w-56">2</div>  
	<div class="bg-blue-500 h-16 w-56">3</div>  
	<div class="bg-blue-500 h-16 w-56">4</div>  
</div>
```

由于div是块级元素，因此每个div默认占据一行

## 设置 Flex

![](assets/Pasted%20image%2020230507152243.png)

```html
<div class="flex bg-amber-600 w-96">  
	<div class="bg-blue-500 h-16 w-56">1</div>  
	<div class="bg-blue-500 h-16 w-56">2</div>  
	<div class="bg-blue-500 h-16 w-56">3</div>  
	<div class="bg-blue-500 h-16 w-56">4</div>  
</div>
```

可以看到 div 已经沿着X轴排列

> flex 默认设置为 X轴 排列


## 指定排列顺序

```html
<div class="flex flex-row-reverse bg-amber-600 w-96">  
	<div class="bg-blue-500 h-16 w-56">1</div>  
	<div class="bg-blue-500 h-16 w-56">2</div>  
	<div class="bg-blue-500 h-16 w-56">3</div>  
	<div class="bg-blue-500 h-16 w-56">4</div>  
</div>
```

![](assets/Pasted%20image%2020230507152556.png)

> 横向反方向排序

其他的排列方式还有
- flex-row：横向顺序，默认
- flex-row-reverse：横向反方向
- flex-col：纵向顺序
- flex-col-reverse：纵向反方向

## 元素的大小

- 父元素的宽度如果比所有子元素的加起来短，那么会平均每个子元素都会相应的缩短
- 子元素如果没有设置宽度，不会自动伸展，仅占据子元素内内容的宽度

## 换行(flex-wrap)显示

```html
<div class="flex flex-row flex-wrap bg-amber-600 w-96">
    <div class="bg-blue-500 h-16 w-56">1</div>
    <div class="bg-blue-500 h-16 w-56">2</div>
    <div class="bg-blue-500 h-16 w-56">3</div>
    <div class="bg-blue-500 h-16 w-56">4</div>
</div>
```

从上面的测试可知，当子元素的大小超过了父元素，会被平均地缩小，以充分展示，当我们不想让子元素被缩小时，可以设置换行，通过多行来充分地展示子元素

- flex-wrap：换行
- flex-wrap-reverse：反方向换行
- flex-nowrap：不换行，默认

## 简写

```css
#div{
	display: flex;
	flex-flow: row wrap;
}
```

等同于

```css
#div{
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
}
```

## 间距（Justify Content）

当父元素的宽度大于子元素的总宽度时，就会有还剩下的空间还未被分配。此时可以通过设置间距来利用上剩余的空间。

- justify-start：子元素沿着主轴起点排序
- justify-end：子元素沿着主轴终点排序
- justify-center：子元素沿着主轴的中心点对齐
- justify-between：沿着主轴排列，每个子元素之间的距离相等（顶到起点和终点）
- justify-around：沿着主轴排列，每个元素两侧的距离相等（不顶到起点和终点）
- justify-evenly：沿着主轴排列，每个元素两侧的距离相等，但是两个相邻的元素之间的距离仅计算一次（不顶到起点和终点）

## 控制交叉轴的对齐方式

将多行的每一行单独处理

- items-start：从交叉轴起点开始
- items-end：从交叉轴终点开始
- items-center：从交叉轴中心点开始
- items-baseline：(暂未理解)


将多行视作一个整体进行处理，与上面的语义一样

- content-center
- content-start
- content-end
- content-between
- content-around


# 设置在子对象

