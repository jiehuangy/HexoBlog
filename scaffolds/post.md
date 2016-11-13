---
title: {{ title }}
date: {{ date }}
tags:
categories:
---




<!-- more -->
## Equation
{% math %} 
\begin{aligned}
L_i  & =  \sum_{j\neq y_i}max(0,s_i - s_{y_i} +\Delta) \\
& =  \sum_{j\neq y_i}max(0,w_j^Tx_i - w_{y_i}^Tx_i +\Delta)
\end{aligned}
\label{eq:example}
{% endmath %}

Eq.\ref{eq:example}

## Image
{% img /images/avatar.jpg 200 200 This is a example image. %}

## Code
{% codeblock lang:cpp %}
#include <iostream>
int main()
{
	std::cout << "Hello World" << std::endl;
	return 0;
}
{% endcodeblock %}