#flask与js的模板冲突
##Question
服务器端和客户端都用模板,往往会产生问题,因为用的分隔符也就那么几种,比如现在正在用的Jinja2（Flask的默认模板）和AngularJS默认的变量分隔符都是”{{}}”，当它们一起使用的时候自然就会产生冲突。

##Solution
Django里的分割符也是”{{}}”，所以可以参考：《AngularJS with Django – Conflicting template tags》里给出的解决方案，简而言之，这个方案就是利用AngularJS的一个API改变他的分隔符：

```js

myModule.config(function($interpolateProvider) {
$interpolateProvider.startSymbol(‘{[{‘);
$interpolateProvider.endSymbol(‘{[{‘);
});

```

但这样做的缺点是如果你使用了其它的AngularJS的插件，而这个插件的模板中使用了”{{}}”这样的分隔符（写死在模板中了），那么就会出问题。
那反过来想想，我们可以不改客户端模板的分隔符，而是去改服务器模板的分隔符，当然Jinja2也是支持的：

```python

env = Environment(variable_start_string=”${“, variable_end_string=”}”)

```

这样可以把Jinja2的变量分隔符改为“${}”，当然还可以做更多的设置。但这样做不只对服务器端模板的编写者不习惯，更严重的问题是一些针对这种模板的编辑器也认不出这个符号了。
除了上述两种非此即彼的方案，也许二者的分隔符都不做修改是更好的方法。Jinja2文档里有讲原样输出一个分隔符的方法：

{{ ‘{{‘ }}

如果输出一大段文字，还有更好的方法：
```html

{% raw %}
<ul>
{% for item in seq %}
<li>{{ item }}</li>
{% endfor %}
</ul>
{% endraw %}

```html

当然这样的模板会难看些，但也是比较折中的方法了。
