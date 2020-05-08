---
layout: post
title: 블로그 markdown 작성 룰
subtitle : 글 작성을 위한 Grape-Theme markdown 작성법
tags: [save]
author: Sohyun Kim
comments : False
---

<br>

<h2>1. HTML headings</h2>
{% highlight html %}
<h1>This is heading 1</h1>
<h2>This is heading 2</h2>
<h3>This is heading 3</h3>
<h4>This is heading 4</h4>
<h5>This is heading 5</h5>
<h6>This is heading 6</h6>
{% endhighlight %}
<h1>This is heading 1</h1>
<h2>This is heading 2</h2>
<h3>This is heading 3</h3>
<h4>This is heading 4</h4>
<h5>This is heading 5</h5>
<h6>This is heading 6</h6>

<br>

<h2>2. bold text</h2>
{% highlight html %}
<p>This is normal text - <b>and this is bold text</b>.</p>
{% endhighlight %}
<p>This is normal text - <b>and this is bold text</b>.</p>

<br>

<h2>3. list</h2>
<h3>a. unordered list</h3>
{% highlight html %}
- Coffee
- Tea
- Milk
{% endhighlight %}
- Coffee
- Tea
- Milk

<h3>b. ordered list</h3>
{% highlight html %}
1. Coffee
2. Tea
3. Milk
{% endhighlight %}
1. Coffee
2. Tea
3. Milk

<br>

<h2>4. hyperlink</h2>
{% highlight html %}
[naye0ng's blog](https://naye0ng.github.io)
{% endhighlight %}
[naye0ng's blog](https://naye0ng.github.io)

<br>

<h2>5. image</h2>
Try using `.width-30`, `.width-40`, `.width-50`, `.width-60`, `.width-70` and `.width-80` class! You can easily change the image width.

{% highlight html %}
![sample image]({{ site.baseurl }}/assets/img/koreaSunset.jpg)
![sample image]({{ site.baseurl }}/assets/img/koreaSunset.jpg){: .width-30}
![sample image]({{ site.baseurl }}/assets/img/koreaSunset.jpg){: .width-50}
![sample image]({{ site.baseurl }}/assets/img/koreaSunset.jpg){: .width-80}
{% endhighlight %}
![sample image]({{ site.baseurl }}/assets/img/koreaSunset.jpg)
<p></p>
![sample image]({{ site.baseurl }}/assets/img/koreaSunset.jpg){: .width-30}
![sample image]({{ site.baseurl }}/assets/img/koreaSunset.jpg){: .width-50}
![sample image]({{ site.baseurl }}/assets/img/koreaSunset.jpg){: .width-80}
<br>

<h2>6. table</h2>
{% highlight html %}
| Header 1  | Header 2 | Header 3 |
| :------- | :-------: | -------: |
| Content 1  | Content 2 | Content 3 |
| Content 1  | Content 2 | Content 3 |
{% endhighlight %}
| Header 1  | Header 2 | Header 3 |
| :------- | :-------: | -------: |
| Content 1 | Content 2 | Content 3 |
| Content 1 | Content 2 | Content 3 |

<br>

<h2>7. Code </h2>
You can add highlighting for code in `highlight.scss`.

{% highlight python %}
# test function
def test :
    print('hello world!')
{% endhighlight %}

<br>

<h2>8. Quotes</h2>
{% highlight html %}
> Hello World, This is quotes!
{% endhighlight %}
> Hello World, This is quotes!

<br>

<h2>9. `Backtick`</h2>
{% highlight html %}
`Grape-Theme`
{% endhighlight %}
`Grape-Theme`