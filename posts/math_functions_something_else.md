[title]: <> (Math Functions Something Else)
[date]: <> (2026/03/27)
[category]: <> (general)

# Advanced Mathematical Notations

\=====================================

This document showcases various complex mathematical functions using LaTeX syntax.

## Trigonometric Functions

The sine function is defined as:

$$\sin(x) = \frac{e^{ix} - e^{-ix}}{2i}$$

where $x$ is the angle in radians. The cosine function can be expressed as:

$$\cos(x) = \frac{e^{ix} + e^{-ix}}{2}$$

The tangent function is given by:

$$\\tan(x) = \\frac{\\sin(x)}{\\cos(x)}$$

## Exponential and Logarithmic Functions

The exponential function $f(x) = e^x$ has a derivative of:

$$f'(x) = e^x$$

The natural logarithm $\ln(x)$ is the inverse function of $e^x$, with a derivative of:

$$\frac{d}{dx} \ln(x) = \frac{1}{x}$$

## Differential Equations

Consider the differential equation:

$$y'' + 4y' + 4y = 0$$

This is a second-order linear homogeneous differential equation with constant coefficients.

## Fourier Series

The Fourier series of a function $f(x)$ is given by:

$$f(x) = \sum_{n=-\infty}^{\infty} c_n e^{inx}$$

where the coefficients $c\_n$ are calculated using:

$$c_n = \frac{1}{2\pi} \int_{-\pi}^{\pi} f(x) e^{-inx} dx$$

## Special Functions

The gamma function $\\Gamma(z)$ is defined as:

$$\Gamma(z) = \int_{0}^{\infty} t^{z-1} e^{-t} dt$$

for $Re(z) > 0$. The zeta function $\zeta(s)$ is given by:

$$\zeta(s) = \sum_{n=1}^{\infty} \frac{1}{n^s}$$