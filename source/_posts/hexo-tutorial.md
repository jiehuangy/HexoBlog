---
title: Hexo Tutorial
date: 2016-11-06 18:40:28
tags:
categories:
---

## Equation

### Inline
{% blockquote %}
Simple inline \$a = b + c\$.
{% endblockquote %}

Simple inline $a = b + c$.

<!-- more -->

### Block
{% codeblock %}{% raw %}
\begin{equation}
  \int_0^\infty \frac{x^3}{e^x-1}\,dx = \frac{\pi^4}{15}
  \label{eq:example}
\end{equation}

引用 公式\ref{eq:example}
{% endraw %}{% endcodeblock %}


\begin{equation}
  \int_0^\infty \frac{x^3}{e^x-1}\,dx = \frac{\pi^4}{15}
  \label{eq:example}
\end{equation}

引用 公式\ref{eq:example}

## Image
{% blockquote %}{% raw %}
{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}
{% img /images/avatar.jpg 200 200 This is a example image. %}
{% endraw %}{% endblockquote %}
{% img /images/avatar.jpg 200 200 This is a example image. %}



## Code
{% codeblock "source code" %}{% raw %}
{% codeblock lang:cpp %}
#include <iostream>
int main()
{
	std::cout << "Hello World" << std::endl;
	return 0;
}
{% endcodeblock %}{% endraw %}
{% endcodeblock %}


{% codeblock lang:cpp %}
#include <iostream>
int main()
{
	std::cout << "Hello World" << std::endl;
	return 0;
}
{% endcodeblock %}


