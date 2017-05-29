---
layout: post
title:  "Introdução ao JQuery"
date:   2017-05-29
---


<p class="intro"><span class="dropcap">N</span>esse post vou dar uma breve introdução ao JQuery, um poderoso framework javascript capaz de criar animações, manipular eventos e simplificar o processo de criação com javascript.</p>
<figure>
  <img src="http://www.vikaskbh.com/wp-content/uploads/2014/01/jquery_logo.png" width="400px" alt="JQuery logo">
  <figcaption>Fig1. - Logo do JQuery.</figcaption>
</figure>

<p>Não é atoa que o slogan do JQuery é "Write less, do more.", ele surgiu para simplificar a maneira como escrevemos JavaScrip, veja o exeplo de um código escrito em JavaScript puro e o código escrito em JQuery.</p>

<p>Pegar o conteúdo de uma div com o id="content" e armazear em uma variável usando JavaScript puro.</p>

{% highlight ruby %}
var content = document.getElementById("#content").innerHTML;
{% endhighlight %}

<p>O mesmo código escrito usando JQuery</p>
{% highlight ruby %}
var content = $("#content").innerHTML;
{% endhighlight %}
