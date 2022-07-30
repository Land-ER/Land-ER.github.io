# 导数
## 介绍
---
## 公式
| 原函数 | 导函数 |
| :-: | :-: |
| $f(x)=c$ | $f'(x)=0$ |
| $f(x)=x^n$ | $f'(x)=nx^{n-1}$ |
| $f(x)=\sin x$ | $f'(x)=\cos x$ |
| $f(x)=\cos x$ | $f'(x)=-\sin x$ |
| $f(x)=a^x$ | $f'(x)=a^x\ln a$ |
| $f(x)=e^x$ | $f'(x)=e^x$ |
| $f(x)=\log_a x$ | $f'(x)=\frac{1}{x\ln a}$ |
| $f(x)=\ln x$ | $f'(x)=\frac{1}{x}$ |
### 加法
若
$$h(x)=f(x)+g(x)$$
则有
$$h'(x)=f'(x)+g'(x)$$
### 减法
若
$$h(x)=f(x)-g(x)$$
则有
$$h'(x)=f'(x)-g'(x)$$
### 乘法
若
$$h(x)=f(x)g(x)$$
则有
$$h'(x)=f'(x)g(x)+f(x)g'(x)$$
### 除法
若
$$h(x)=\frac{f(x)}{g(x)}$$
则有
$$h'(x)=\frac{f'(x)g(x)-f(x)g'(x)}{[g(x)]^2}$$
### 复合
若
$$h(x)=f(g(x))$$
则有
$$h'(x)=f'(g)g'(x)$$
例如：
$$f(x)=\sin 3x$$
则
$$f'(x)=(\cos 3x)\times 3=3\cos 3x$$