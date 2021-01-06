---
author: Hugo Authors
title: Math Typesetting
date: 2019-03-08
description: A brief guide to setup KaTeX
math: true
---

Mathematical notation in a Hugo project can be enabled by using third party JavaScript libraries.
<!--more-->

In this example we will be using [KaTeX](https://katex.org/)

- Create a partial under `/layouts/partials/math.html`
- Within this partial reference the [Auto-render Extension](https://katex.org/docs/autorender.html) or host these scripts locally.
- Include the partial in your templates like so:  

```bash
{{ if or .Params.math .Site.Params.math }}
{{ partial "math.html" . }}
{{ end }}
```

- To enable KaTex globally set the parameter `math` to `true` in a project's configuration
- To enable KaTex on a per page basis include the parameter `math: true` in content files

**Note:** Use the online reference of [Supported TeX Functions](https://katex.org/docs/supported.html)

{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}
<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}

### Examples


Inline math: \\(\varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887…\\)

Block math:
$$
 \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } } 
$$

# 2階線形微分方程式の定数変化法（メモ）

###### tags: `解説`

2階線形微分方程式

:::info
$$
\frac{d^2y}{{dx}^2} + P(x)\frac{dy}{dx} + Q(x)y = R(x)    \tag{★}\label{eq-first}
$$
:::

上記の場合（非同次），右辺を0とおいた次の式

$$
\frac{d^2y}{{dx}^2} + P(x)\frac{dy}{dx} + Q(x)y = 0
$$

の一般解が

$$
y = uF(x) + v G(x)    \tag{1}\label{eq-1}
$$

と求められているとする．

例えば，$y = ue^x+ve^{-x}$なら$F(x)=e^x$，$G(x)= e^{-x}$．

大多数の問題は，未定係数法によって特殊解を1つ求め，$\eqref{eq-1}$に加えれば完了するが， ==R(x)の形によっては未定係数法が使えない==ので，この場合に定数変化法を用いることができる．

ここからは，1変数の場合と同様，$u$,$v$を $x$の関数として，$\eqref{eq-first}$式の一般解を求めることを考える．

まず，$\eqref{eq-1}$を$x$で微分すると，

$$
y^\prime = u^\prime F(x) + uF^\prime (x) + v^\prime G(x) + v G^\prime(x)    \tag{2}\label{eq-2}
$$

ここで次の条件を設定する（大事）

:::danger
$$
u^\prime F(x) + v^\prime G(x) = 0 \tag{a}\label{eq-a}
$$
:::

この条件を$\eqref{eq-2}$に適用すると，

$$
y^\prime =  uF^\prime (x) + v G^\prime(x)    \tag{3}\label{eq-3}
$$

さらに$\eqref{eq-3}$を$x$で微分すると

$$
y^{\prime\prime} = u^\prime F^\prime(x) + uF^{\prime\prime} (x) + v^\prime G^\prime(x) + v G^{\prime\prime}(x)    \tag{4}\label{eq-4}
$$

ここで，基本解について以下が成り立つことに注意して，

* $F^{\prime\prime}(x) + P(x)F\prime(x) + Q(x)F(x) = 0$
* $G^{\prime\prime}(x) + P(x)G\prime(x) + Q(x)G(x) = 0$


$y^\prime$と$y^{\prime\prime}$を$\eqref{eq-first}$に代入すると，

$$
u^\prime F^\prime (x) + v^\prime G^\prime (x) = R(x) \tag{b}\label{eq-b}
$$

が得られる．$\eqref{eq-a}$と$\eqref{eq-b}$を連立方程式として解き$u^\prime$と$v^\prime$を求める．

$$
\left\{\begin{array}{l}u^\prime F(x) + v^\prime G(x) = 0\\u^\prime F^\prime (x) + v^\prime G^\prime (x) = R(x)\end{array}\right.
$$


これを行列にすると，

$$
\displaystyle
\begin{pmatrix} F(x) & G(x) \\ F^\prime(x) & G^\prime(x)\end{pmatrix}\begin{pmatrix} u^\prime \\ v^\prime \end{pmatrix}=\begin{pmatrix} 0 \\ R(x) \end{pmatrix}
$$

ここで，==ロンスキアン==を$W(x)$で定義する．（$W(x) \neq 0$を意識）
$$
W(x) = \begin{vmatrix} F(x) & G(x) \\ F^\prime(x) & G^\prime(x)\end{vmatrix}
$$

これより，

$$
\left\{\begin{array}{l}u^\prime = \dfrac{- G(x)R(x)}{W(x)} \\v^\prime = \dfrac{F(x)R(x)}{W(x)}\end{array}\right.
$$

だから，

$$
\left\{\begin{array}{l}u = \displaystyle　\int \dfrac{- G(x)R(x)}{W(x)} dx \\v = \displaystyle \int \dfrac{F(x)R(x)}{W(x)} dx \end{array}\right.
$$

よって，$\eqref{eq-first}$の一般解は，

:::success
$$
y = uF(x) + vG(x) = F(x)\displaystyle \int \dfrac{- G(x)R(x)}{W(x)} dx + G(x) \displaystyle \int \dfrac{F(x)R(x)}{W(x)} dx 
$$
:::

と表される．積分項が2つあるので任意定数も2つ登場する．計算を用意にするためにあえて$\eqref{eq-a}$の条件を設定するところがポイント．



