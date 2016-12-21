# ripple
http://design.google.com
```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>ripple</title>
    <script src="bower_components/jquery/dist/jquery.min.js"></script>
</head>
<style>
    body {
        background: #000;
    }
    .btn {
        width: 100px;
        height: 30px;
        color: white;
        background: #00b3ee;
        padding: 10px 20px;
        cursor: pointer;
        position: relative;
    }

    .ripple {
        position: absolute;
        width: 4px;
        height: 4px;
        background: #fff;
        display: block;
        border-radius: 50%;
        animation: ripple 1.4s;
        transform: scale(100);
        opacity: 0;
    }

    @keyframes ripple {
        from {
            transform: scale(0);
            opacity: .5;
        }
        to {
            transform: scale(100);
            opacity: 0;
        }
    }
</style>
<body>
<span class="ripple"></span>
<p>大家</p>
<button class="btn">波纹按钮1</button>
<button class="btn">波纹按钮2</button>
<button class="btn">波纹按钮3</button>
</body>
<script>
    (function ($) {             //jQuery封装水波的方法
        $.fn.extend({
            "rippleBtn": function () {
                return this.each(function () {
                    $(this).on('click', function (e) {
                        var x = e.pageX, y = e.pageY
                        x = x - $(this).offset().left;
                        y = y - $(this).offset().top;
                        console.log(x, y);
                        var ripple = $('<div class="ripple"></div>');
                        ripple.css({
                            left: x - 2,
                            top: y - 2
                        });
                        $(this).append(ripple);
                        ripple.on('animationend', function () {
                            ripple.remove()
                        })
                    })
                })
            }
        })
    })(jQuery)
    $('.btn').rippleBtn()       //调用的方法
</script>
</html>
```
