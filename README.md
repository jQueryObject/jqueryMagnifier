# jquery放大镜jqueryMagnifier

效果如下：
![](images/img.gif)

all code:
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>放大镜效果</title>
	<style>
		*{margin: 0px;padding:0px;}
		#con_box{width: 750px;height: 400px;margin-top:40px;position: relative;margin-left: 20px;}
		#small{width: 400px;height: 400px;}
		#big{width: 300px;height: 300px;overflow: hidden;position: absolute;top:50%;left: 420px;z-index: 999;margin-top:-150px;display: none;}
		#big img{position: absolute;top: 0px;left: 0px;}
		.move_div{width: 100px;height: 150px;background: rgba(0,0,0,.5);position: absolute;top: 0px;left: 0px;display: none;}
	</style>
</head>
<body>
	<div id="con_box">
		<div id="small">
			<img src="images/simg.jpg" />
			<div class="move_div"></div>
		</div>
		<div id="big">
			<img src="images/bimg.jpg" />
		</div>
	</div>		
</body>
</html>
<script src="js/jquery.js"></script>
<script>
	$(document).ready(function(){
		$('#small').hover(function(event){
			$('#big').css('display','block');
			$('.move_div').css('display','block');
		},function(){
			$('#big').css('display','none');
			$('.move_div').css('display','none')
		});
		$('#small').mousemove(function(event){
			var $X = event.clientX;//获取鼠标与浏览器X轴的坐标
			var $Y = event.clientY;//获取鼠标与浏览器Y轴的坐标
			var $T = $('#con_box').offset().top;//获取#con_box距离顶部的距离
			var $L = $('#con_box').offset().left;//获取#con_box距离左面的距离
			var $W = $('.move_div').width()/2;//获取move_div的宽度一半
			var $H = $('.move_div').height()/2;//获取move_div的高度一半
			var $w = $('#small').width();//获取small的宽度
			var $h = $('#small').height();//获取small的高度
			$('.move_div').css({'left':$X-$L-$W,'top':$Y-$T-$H});   //$X-$L-$W为move_div移动的宽度 $Y-$T-$H为move_div移动的高度
			if($X-$L-$W<0){
				$('.move_div').css({'left':0});
			}
			if($X+$W>$w+$L){
				$('.move_div').css({'left':($w-$W*2)});
			}
			if($Y-$H<0+$T){
				$('.move_div').css({'top':0});
			}
			if($Y+$H>$h+$T){
				$('.move_div').css({'top':($h-$H*2)});
			}
			var $bW = $('#big').width();
			var $bH = $('#big').height();
			var _w =  $w-$W*2;//move_div移动最大宽度
			var _h =  $h-$H*2;//move_div移动最大高度
			var _bw = ($X-$L-$W)/_w;//获取滑动宽度的比例
			var _bh = ($Y-$T-$H)/_h;//获取滑动高度的比例
			$('#big img').css({'left':-($('#big img').width() - $bW)*_bw,'top':-($('#big img').height() - $bH)*_bh})
		});
	})
</script>
```
