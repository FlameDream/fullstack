# html设置居中常用的几种方式

Web前端开发，html居中显示也是网页设计中最基本的显示方式之一，如下有几种居中的方法。

## 一、水平居中

### 1.1 使用文本对齐属性

可以使用 text-align 属性来对 HTML 元素进行水平居中。该属性可设置在父元素上，使其中的子元素实现水平居中。

示例代码：
```html
<style>
	.contentV{
		.text-align: center;
	}

</style>

<div class="contentV">
	<p>Hello World!</p>
</div>

```

### 1.2 使用 margin 属性

同样可以使用 margin 属性来实现水平居中。需要注意的是，此方法只适用于具有固定宽度的元素。

示例代码：
```html
<style>
	.contentV{
		widows: 100px;
		margin: 0 auto;
	}

</style>

<div class="contentV">
	<p>Hello World!</p>
</div>

```

## 二、垂直居中

### 2.1 使用文本对齐属性

如果需要在 HTML 元素中实现垂直居中，在父元素上可以设置 display: table 属性，而在子元素上设置 display: table-cell 和 vertical-align: middle 属性。

示例代码：

```html

<style>
	.contentV{
		display: table;

		width: xxpx;
		height: xxpx;
	}

	.inner{
		display: table-cell;
		vertical-align: middle;
	}

</style>

<div class="contentV">
	<div class="inner">
		<p>Hello World!</p>
	</div>
</div>

```

### 2.2 使用 flex 属性

另外一个实现垂直居中的方法是使用 flex 属性。父元素上设置 display: flex，而子元素设置 align-items: center 和 justify-content: center 属性即可实现垂直居中。

示例代码：

```html
<style>
	.contentV{
		display: flex;
		align-items: center;
		justify-content: center;
	}

</style>

<div class="contentV">
	<p>Hello World!</p>
</div>

```

这两种方法都可以轻松地实现在 HTML 中进行居中显示。需要注意的是，在使用 margin 属性进行水平居中时，必须指定一个固定的宽度，并将 margin 属性的左右值设置为 auto，以实现居中显示。

总结：

本文介绍了两种水平居中和两种垂直居中的方法，其中 text-align 和 margin 属性适用于水平居中，而 display: table、display: flex 和 vertical-align 属性适用于垂直居中。无论是哪种方法，都能够轻松地实现在 HTML 中进行居中显示。



