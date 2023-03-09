#  Ch 9: z-Transform

## 9.1 Bilateral z-transform

z-transform: $X(z) = \sum_{n=-\infty}^\infty x(n)z^{-n}$ where $X(z)$ is a function of the complex variable $z$

looks something like $X(z) = \cdots + x(-2)z^2 + x(-1)z + \boxed{x(0)} + x(1)z^{-1} + x(2) z^{-2} + \cdots$

* bilateral because both $z$ and $z^{-1}$ appear in $X(z)$
* $-2\delta(n + 1) + 4\delta(n) + 3\delta(n-1) \longleftrightarrow -2z+4+3z^{-1}$
  * note that X(z) isn't defined for all values of z such as $0$ and $\pm\infty$ because $z^{-1}$ isnt defined, etc.

## 9.2 Region of Convergence

ROC: set of all points $z $ where the series $X(z)$ converges aka $z\in\C , |X(z)| < \infty$

* where z can be any complex number
* if, instead of sum of $x(n)z^{-n}$ we do $|x(n)z^{-n}|$ then this is absolute convergence

two kinds of sequences: 

* finite-duration: samples = 0 for all values of n outside some finite bound
  * z-transform generally is some $\pm$ powers of z
  * means that ROC is entire complex plane except maybe 0 or $\pm\infty$
    * z = 0 excluded if $x(n) \ne 0$ for $n > 0$ since $X(z)$ contains some power of $z^{-1}$ aka $X(z) = 2 - 3z^{-=5}$
    * $z = \pm\infty$ excluded if $x(n) \ne 0$ for $n < 0$ aka $X(z) = -4z^5 + 2$
* infinite-duration:
  * types:
    * Right-sided: $x(n) = 0$ for $n < n_0$ aka $x(n) = 0.5^n\cdot u(n+3)$
    * Two-sided: $x(n) = 0.5^n$
    * Left-sided: $x(n) = 0$ for $n > n_0$ aka $x(n) = 0.5^n \cdot u(-n+3)$
  * ROC is discs and rings in the complex dimension
    * Right-sided: $|z| > r$; Left-sided: $|z| < r$;  Two-sided: $r_1 < |z| < r_2$
    * prove by setting $z = \rho e^{j\theta}$ and plugging it into summation for convergence

## 9.3 Exponential Sequences

* right sided exponential sequence: $x(n) = \alpha^n u(n)$
  * increasing if $\alpha > 1$; decreasing if $\alpha < 1$
  * z-transform gives $X(z) = \dfrac{z}{z - a}$ by geometric series equation
  * ROC = {$z\in \C$ such that $|z| > |\alpha|$}

* left sided exponential sequence: $x(n) = -\alpha^n u(-n-1)$
  * remember this is upside down because negative magnitude
  * z-transform: $X(z) = \dfrac{z}{z - \alpha}$ for $|z| < |\alpha|$
  * same as right sided but different ROC
* if given a z-transform like $X(z) = \dfrac{z}{z - 1/2}$ there are 2 possible sequences
  * $x(n) = 0.5^n u(n)$ or $x(n) = -0.5^n u(-n-1)$
  * only with a ROC like $|z| > 0.5$ allows us to determine which side sequence $x(n) = 0.5^n u(n)$
* for something like $x(n) = \alpha^n u(n) + \beta^n u(-n-1)$ aka a two-sided sequence
  * $X(z) = \dfrac{z}{z - \alpha} - \dfrac{z}{z - \beta}$
  * use finite geo series to determine ROC, aka $|\alpha| < |z| < |\beta|$

## 9.4 Properties of Z-transform

ROC is represented in the form $R_x\cup R$ where $R$ represents a subset of ${0, \infty, -\infty}$ and $R_x$ is the ring or disk representing convergence area

Properties: 

* Linearity: $ax(n) + by(n) \longleftrightarrow aX(z) + bY(z)$
  * ROC is $z\in R_x\cap R_y$ but for the $R = {0, \pm\infty}$ we have to reconsider since terms in X and Y might cancel out
  * if we want to find the inverse z-transform, we look at the ROC and all possible combos of sequences for each linear part (page 217-218 Ex: 9.6)
  * Ex 9.7 also important
* Time shifts: $x(n - n_0) \longleftrightarrow z^{-n_0}X(z)$
* Exponential modulation: $a^nx(n) \longleftrightarrow X(z / a)$
  * ROC of $a^nx(n)$ is $z\in\C$ such that $|a|r_1 < |z| < |a|r_2$ union with $R$
  * a can be complex
* Time reversal: $x(-n) \longleftrightarrow X(1 / z)$
  * ROC = {$z\in\C$ such that $1/r_2 < |z| < 1/r_1$} in union with $R$
* Linear modulation: $nx(n) \longleftrightarrow -z\dfrac{dX(z)}{dz}$
  * ROC is still the same but must union with new R
* Complex conjugation: $x^*(n) \longleftrightarrow [X(z^*)]^*$
  * ROC is still the same but must union with new $R$ aka $R_x\cup R$
* Linear convolution: $x(n)\star y(n) \longleftrightarrow X(z)Y(z)$ with new ROC = $R_x \cup R$

Transform a running sum: if $w(n) = \sum_{k=0}^n x(k)$ then $\sum_{k=0}^n x(k) = w(n) = x(n)\star u(n)$  so $\sum_{k=0}^n x(k) = w(n) \longleftrightarrow \dfrac{X(z)}{1 - z^{-1}}$ with ROC ${|z| > \max(1, r)}$

## 9.5 Evaluating series

given a series, find the nearest Z-transform, evaluated at a certain value of z, then make sure that value of z is in ROC. then, use the closed form of that z-transform to evaluate the sum

## 9.6 Initial value theorem

To determine value of **causal** sequence $x(n)$ at time 0 without doing inverse z-transform, we use the initial value theorem:

If x(n) is causal aka $x(n) = 0$ for $n < 0$, $\lim_{z\rarr\infty} X(z) = x(0)$ where $z = \infty$ belongs to ROC because x(n) is causal

## 9.7 Upsampling and Downsampling

Upsampling: $y(n) = x(n/L)$ if $n/L$ is an integer otherwise $y(n) = 0$.

* $y(n)$ is time expansion of $x(n)$: block diagram is a box with an up arrow followed by L
* inserting $L - 1$ zeros between each sample
* corresponding z-transform is $Y(z) = X(z^L)$
  * ROC of y(n) is $z\in\C$ such that $r_1^{1/L} < |z| < r_2^{1/L}$  union with R'

Downsampling: $y(n) = x(Mn)$

* $y(n)$ is time compression of $x(n)$: block diagram is box with down arrow followed by M
* corresponding z-transform is not as simple
  * $Y(z) = \dfrac{1}{M}\sum_{k=0}^{M-1}X(W_M^k z^{1/M})$ where $W_M = e^{-j2\pi / M}$
    * ROC = $z\in\C$ such that $r_1^M < |z| < r_2^M$ in union with R'

**tables on Page 247-248 of textbook**

