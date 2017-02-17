### FileReader && Blob小记录

MDN连接：[FileReader](https://developer.mozilla.org/en-US/docs/Web/API/FileReader) [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)

下面是个简单的小例子，用了filereader的readAs...函数，并且测试读取Blob对象以及file文件，都能读取到内容。

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>FILE API</title>
	<style>
		#input {
			width: 200px;
			height: 40px;
		}
	</style>
</head>
<body>
	<input type=file id=input >
</body>
<script>
	let input = document.querySelector('#input');
	let fr = new FileReader();
	var loginfoStyle = 'font-size:18px;color: red;';
	var blob = new Blob(['哈哈哈，你去死吧，嘎嘎嘎'], {type: 'text/html;charset=UTF-8'})
	fr.onloadstart = function() {
		console.log('%c start load file data.', loginfoStyle)
	};
	fr.onload = function(e) {
		console.log(e.target.result)
	};
	fr.onloadend = function() {
		console.log('%c load file data ended!', loginfoStyle)
	};
	input.onchange = function() {
		console.log(arguments);
		// fr.readAsText(input.files[0]);
		fr.readAsText(blob);
	};
</script>
</html>
```
<div style="display: flex; flex-flow: column;float: right;margin-top: 20px;">
  <div style="text-align: center;">张泽木</div>
  <div>2017-02-17 10:34</div>
</div>
