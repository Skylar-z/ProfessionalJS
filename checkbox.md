checkbox的value和checked属性详解
2019年02月27日 18:52:25 如何在3年拿到50K 阅读数 2003
版权声明： https://blog.csdn.net/kouryoushine/article/details/87984749
一 、checked属性
checked属性代表的是当前checkbox是否被选中，如果选中返回true，未选中返回false。和value值无关。

<p><input type="checkbox" name="vehicle" checked/> I have a car</p>

document.getElementById("checkbox1").checked
1
2
3
知识点：
checked只代表页面刷新时，checkbox处于选中状态。checked的属性返回true;
此时，点击checkbox使其处于非选中状态，html代码没有变化（checked依然源码上）。但checked的属性返回false;

html中出现checked字样，代表刷后新选，和checked=“任意值”无关。哪怕checked=“false”,刷新时，checkbox仍然是选中状态。可以理解为checked之后的属性值都是没意义的。

结论：
html中checked意味着页面加载时，让该checkbox元素的checked属性为true,页面显示选中状态。
在提交表单时判断表单是否选中的标准是document.getElementById(“checkbox1”).checked返回true还是false。和html页面内容无关。
二 、value属性
<p><input type="checkbox" name="vehicle" id="checkbox1" /> I have a car</p>

alert(document.getElementById("checkbox1").value);
1
2
3
value的属性代表checkbox提交给表单的值。

value如果没有设置，则默认value的值是“on”。如果设置，自然value就是设置的值。
value的值和表单是否选中无关。 无论表单是否选中，checkbox的值都是一样的。
※这个点是包括我在内很多人都有误解。
三、表单提交对checkbox处理
请问下面这个表单提交后，提交的name和value是什么呢？

<p><input type="checkbox" name="vehicle" id="checkbox1" checked/> I have a car</p>
1
答案是不确定

解释：
要点1: 当checkbox处于选中状态时，该checkbox的数据才会被提交。否则，数据不提交。
什么叫做选中状态？
唯一准确的答案是document.getElementById(“checkbox1”).checked返回true;
我已经解释过，html的checked只代表刷新后的状态，不代表提交时的状态。
我如果通过js把该属性设置成false，有的浏览器看到的还是打对号选中的状态。实际checked属性是false。

要点2： 表单提交的value是value属性的值。默认是“on”，否则是设置值。无论是否勾选都是一个值。

总结：
上面的表单，如果处于选中状态，提交给server的name-value是"vehicle=on".
如果是非选中状态，提交的是空，也就是不提交该数据。

四、实际工作中遇到的问题：
checkbox未选中状态，表单的数据没有提交到后台。
预期checkbox选中提交1，未选中提交0。但发现数据库没有更新，通过以上明白了为什么。

解决方法：
在表单提交前，扫描所有的checkbox状态，如果checkbox是checked=true。
把value设置为1.。如果checkbox=false，把value设置为0.

具体代码，大家可以百度，有很多人遇到类似问题。解决方法可以有很多种，重点是理解了chebox的原理是什么。