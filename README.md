Module 1: An Introduction to Maximum Likelihood Estimation
================
Brad Price, Ph.D. and Joshua Meadows
January 9, 2023

## Introduction

[Maximum Likelihood Estimation YouTube
Video](https://youtu.be/iDXliogltsc)

[BUDA 530: Module1 - Page4 YouTube Video](https://youtu.be/86BYwnrke5k)

The BUDA program is set up with a focus on the application of
statistical methodology and how to interpret and understand the
methodology. It’s our goal to understand strengths and weaknesses of
these methods. In this course we will look at methodology that uses
statistical theory to generate models and their assumptions. Sometimes
these assumptions don’t need to be met, and it’s just one way to derive
a model. You should still understand where these methods come from and
both how and why we use them.

This section is math intensive, but requires no more than an
understanding of basic calculus, and the very basics of probability.

## Reminders

- Random Variable- A variable whose value is a numerical outcome of a
  random phenomenon. For our purposes we will assume that this random
  phenomena is defined by some probability distribution.

- Minimizing Convex functions with one variable- We are going to assume
  the function is differentiable everywhere for right now. This process
  is simple for a single variable of interest. Take the first derivative
  of the function, set it equal to 0 and solve for the variable.

- Probability Mass Function (pmf)– Assume we have a discrete random
  variable, X, then this is the $Pr(X=x)=g(x)$, we say the pmf is $g$

- Probability Density Function (pdf) – Assume we have a continuous
  random variable, X, then we say it has pdf $f$ such that

$$
\int_{-\infty}^x f(z)dz=P(X\leq x)
$$

## Basic Derivatives, log rules, and notation.

[BUDA 530: Module 1 - Page 5 YouTube
Video](https://youtu.be/USSCZ53DBho)

This sections contains some reminders on derivatives, which are the key
to maximum likelihood. This is just a basic review of what you need to
remember.

### Notation and log rules

- Multiplication $$
  \Pi_{i=1}^n x_i=x_1x_2\ldots x_n
  $$

- Basics log rules

$$
x=\log\left(\exp(x)\right)
$$ $$
\log(x_1x_2)=\log(x_1)+\log(x_2)
$$ $$
\log(\frac{x_1}{x_2})=\log(x_1)-\log(x_2)
$$ $$
\log(x^b)=b\log(x)
$$ $$
\log(\Pi_{i=1}^n x_i)=\sum_{i=1}^n\log(x_i)
$$

### Derivatives

For this modules we need to understand the functional form of a
derivative and some of the basic rules. For this discussion let $x,y$ be
variables we are interested in and let $a,b$ be known constants. We’ll
let $\frac{df(x)}{dx}$ be the derivative of the function $f(x)$ with
respect to $x$. You’ll also sometimes see this written as
$\triangledown_x f(x)$, or $f'(x)$

- Power rule

$$
f(x)=ax^b
$$ $$
\frac{df(x)}{dx}=abx^{b-1}
$$

Example: $$
f(x)=3x^2
$$ $$
\frac{df(x)}{dx}=2*3x=6x
$$

- Chain Rule

$$
f(x)=g(x)^b
$$ $$
\frac{df(x)}{dx}=bg(x)^{b-1}\frac{dg(x)}{dx}
$$

Example:

$$
f(x)=(4x+3)^2
$$ $$
\frac{df(x)}{dx}=2(4x+3)(4)=8(4x+3)
$$

- Derivative of a log

$$
f(x)=\log(g(x))
$$ $$
\frac{df(x)}{dx}=\frac{\frac{dg(x)}{dx}}{g(x)}
$$

Example:

$$
f(x)=log(x)
$$ $$
\frac{df(x)}{dx}=\frac{1}{x}
$$

## What is a “Likelihood Function”?

[BUDA 530: Module1 - Page6 YouTube Video](https://youtu.be/93ectMfxRkg)

You’ve may have heard the term likelihood in casual conversation, but in
this context we are discussing a likelihood function. A likelihood
function is how “likely” is it that data came from a probability model
(or model or distribution). We say it is $L(\theta|x)$. We say that
$\theta|x$ is the parameter of the distribution given the data. So
moving forward, think of this as a function of the parameter. We’re
interested in estimating the parameter given the data is something we
have available. Think of it as how can you best estimate the parameters
given your sample data.

Let $x_1,\ldots, x_n$ be a sample from a distribution that has a pdf
$f(x|\theta)$, where $\theta$ is the set of parameters in the
distribution. For example $\theta$ in the case of a normal distribution
would correspond to specific means and variances. We define the
likelihood function, or likelihood as:

$$
L(\theta|x_1,\ldots, x_n)=L(\theta|x)=\Pi_{i=1}^n f(x_i|\theta).  
$$

## Maximum Likelihood Estimation (MLE)

[BUDA 530: Module1 - Page7 YouTube Video](https://youtu.be/es3Y9M-dJ4w)

Given we have our likelihood:

$$
L(\theta|x_1,\ldots, x_n)=L(\theta|x)=\Pi_{i=1}^n f(x_i|\theta).  
$$

We define the *maximum likelihood estimator (MLE)* as the $\hat{\theta}$
that maximizes the likelihood of the parameter, given then sample
$x_1,\ldots,x_n$.

We define the log likelihood as:

$$
l(\theta)=\log(L(\theta|x_1,\ldots,x_n)),
$$ $$
=\log(\Pi_{i=1}^n f(x_i|\theta)),
$$ $$
=\sum_{i=1}^n \log(f(x_i|\theta)).
$$

The log likelihood is important because is often easier to solve for the
maximum of the log likelihood rather than the likelihood itself. You’ll
see many examples of this and typically maximizing the log likelihood is
the approach we’ll take in the examples to follow.

Just a reminder, that maximizing the log-likelihood requires that the
function is differentiable for all possible/valid values of $\theta$ and
is concave, and is the same thing as minimizing the negative
log-likelihood. We’ll see some of this as we continue to go through
these problems.

### Finidng the Minimum

[BUDA 530: Module1 - Page8 YouTube Video](https://youtu.be/tM0WNXIpfSk)

Finding the minimum of a convex or concave function that is
differentiable everywhere is relatively easy. We take the derivative
with respect to the variable of interest, holding everything else in the
function constant, set it equal to zero, and then solve.

In essence the process looks like finding the $\hat{\theta}$ such that

$$
\frac{dl(\theta)}{d\theta}\biggr\rvert_{\hat{\theta}}=0,
$$ where

$$
\frac{dl(\theta)}{d\theta}\biggr\rvert_{\hat{\theta}}
$$ is the derivative of the loglikelihood with respect to $\theta$
evaluated (plug in) $\hat{\theta}$.

Let’s take a look at a simple example of a convex (has a minimum)
function. We want to minimize

$$
g(\theta)=(\theta+3)^2
$$

with respect to $\theta$. Another way to say this is we need to find the
$\theta$ that minimizes $g(\theta)$. Now let’s take the derivative with
respect to $\theta$,

$$
\frac{dg(\theta)}{d\theta}=2(\theta+3).
$$ We then set the derivative equal to 0 and solve for $\theta$ to find
the minimium.

$$
2(\theta+3)=0
$$ $$
\theta+3=0
$$ $$
\hat{\theta}=-3
$$

So we see that $\theta=-3$ is the minimizer (the $\theta$ that
minimizes) $g(\theta)$.

### Putting It All Together: Normal Example (Mean Only)

[BUDA 530: Module1 - Page9 YouTube Video](https://youtu.be/iBQZess5Y9U)

For our first example let’s use an instance where we are interested in
estimating the mean of a normal distribution. Let’s assume the sample we
have obtained are independent draws (observations) from a $N(\mu,1)$,
that is the data comes from something with an unknown mean, and known
variance equal to 1. In the case the parameter we want to find the MLE
of is $\mu$, so from previous discussions think of $\mu$ as $\theta$.

The pdf of the $N(\mu, 1)$ is :

$$
f(x|\mu)=\frac{1}{\sqrt{2\pi}}\exp\left(\frac{(x-\mu)^2}{2}\right).  
$$

So we define the log of $f(x)$ is

$$
log(f(x|\mu))=-\log(\sqrt{2\pi})-\frac{(x-\mu)^2}{2}.
$$

Finally we define the log likelihood as

$$
l(\mu)=\sum_{i=1}^n\left(-\log(\sqrt{2\pi})-\frac{(x_i-\mu)^2}{2} \right)
$$ $$
= -n\log(\sqrt{2\pi})-\sum_{i=1}^n\frac{(x_i-\mu)^2}{2}
$$

Differentiating $l(\mu)$ with resepect to $\mu$ all parts that don’t
contain $\mu$ drop off (they differentiate to 0). That means

$$
\frac{dl(\mu)}{d\mu}=-\sum_{i=1}^n\frac{-2(x_i-\mu)}{2}
$$ $$
= \sum_{i=1}^n(x_i-\mu).
$$

We then solve

$$
\sum_{i=1}^n (x_i-\mu)=\sum_{i=1}^nx_i-n\mu=0.
$$

Using just basic algebra we get that

$$
\hat{\mu}=\bar{x}=\frac{\sum_{i=1}^n x_i}{n}.
$$

That tells us that the sample mean is the maximum likelihood estimator,
for $\mu$ under these assumptions.

### Binomial Example

[BUDA 530: Module1 - Page10 YouTube Video](https://youtu.be/4-4ToREkUxI)

Let’s now assume our data comes from a $Bin(1, p)$, where 1 is the
number of Bernoulli trials in the binomial, and p is unknown and the
probability of a success occurring in a Bernoulli trial. The pmf of this
is $$
f(x|p)=p^x(1-p)^{1-x},
$$

that means the log of the pmf is

$$
\log(f(x|p))=x\log(p)+(1-x)\log(1-p).
$$

From here we define the log likelihood as:

$$
l(p)=\sum_{i=1}^n\left(x_i\log(p)+(1-x_i)\log(1-p)\right),
$$ $$
=\log(p)\sum_{i=1}^nx_i+\log(1-p)\sum_{i=1}^n(1-x_i).
$$

Differentiating with respect to $p$ we get that

$$
\frac{dl(p)}{dp}=\frac{\sum_{i=1}^nx_i}{p}-\frac{\sum_{i=1}^n(1-x_i)}{1-p}.
$$

Setting equal to 0 and solving we have that

$$
(1-p)\sum_{i=1}^nx_i=p(n-\sum_{i=1}^nx_i)
$$ $$
\sum_{i=1}^nx_i-p\sum_{i=1}^nx_i=pn-p\sum_{i=1}^nx_i
$$ $$
\sum_{i=1}^nx_i=np
$$ $$
\hat{p}=\frac{\sum_{i=1}^nx_i}{n}
$$

### Normal Example: Mean and Standard Deviation

[BUDA 530: Module1 - Page11 YouTube Video](https://youtu.be/Whxq1a538ec)

In this example let’s set up something with two parameters. Let’s assume
our sample is $x_1,\ldots, x_n$ that comes from a $N(\mu, \sigma^2)$
where both $\mu$ and $\sigma^2>0$ are unknown. Now a few things to note
$\sigma^2$ is the parameter and not $\sigma$. That will be a key for us
moving forward. The second thing is that we have two different
parameters that need to be solved jointly. This adds a step to our
process. Once we find the MLE for one (in this case $\mu$), we need to
substitute it back in and then start the process for the next in this
case $\sigma^2$.

Again define The pdf of the $N(\mu, \sigma^2)$ is :

$$
f(x|\mu,\sigma^2)=\frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right).  
$$

So we define the log of $f(x)$ is

$$
log(f(x|\mu,\sigma^2))=-\log(\sqrt{2\pi\sigma^2})-\frac{(x-\mu)^2}{2\sigma^2}.
$$

From there the log likelihood is

$$
l(\mu,\sigma^2)=-n\log(\sqrt{2\pi\sigma^2})-\frac{1}{2}\sum_{i=1}^n(x_i-\mu)^2.
$$

The plan is to optimize with respect to $\mu$ and then plug the estimate
in and then optimize with respect to $\sigma^2$.

First let’s solve for $\mu$, treating $\sigma^2$ as a constant.

$$
\frac{dl(\mu,\sigma^2)}{d\mu}=-\sum_{i=1}^n\frac{-2(x_i-\mu)}{2\sigma^2}
$$ $$
= \frac{\sum_{i=1}^n(x_i-\mu)}{\sigma^2}
$$

Again we treat $\sigma^2$ as a constant so when seting this equal and
solving for $\mu$ it turns into the $\mu$ only problem and we get

$$
\hat{\mu}=\bar{x}=\frac{\sum_{i=1}^n}{n}x_i. 
$$

Now here’s the first time you’ve seen this step. We want to find the MLE
for $\sigma^2$, so we need to plug in $\hat{\mu}$ and solve for
$\sigma^2$.

So we have that $$
l(\hat{\mu},\sigma^2)=-n\log(\sqrt{2\pi\sigma^2})-\frac{1}{2}\sum_{i=1}^n(x_i-\hat{\mu})^2.
$$

Differentiating with respect to $\sigma^2$ we get that

$$
\frac{dl(\hat{\mu},\sigma^2)}{d\sigma^2}=\frac{-n}{2\sigma^2}+\frac{1}{2(\sigma^2)^2}\sum_{i=1}^n (x_i-{\mu})^2.
$$

Solving for the minimum we get that

$$
\frac{-n}{2\sigma^2}+\frac{1}{2(\sigma^2)^2}\sum_{i=1}^n (x_i-\hat{\mu})^2=0
$$ $$
\frac{n}{2\sigma^2}=\frac{1}{2(\sigma^2)^2}\sum_{i=1}^n (x_i-\hat{\mu})^2.
$$

From there we obtain

$$
\hat{\sigma^2}=\frac{\sum_{i=1}^n (x_i-\mu)^2}{n}.
$$

Notice this isn’t what you’re use to seeing as the sample standard
deviation, but this is the MLE. We’ll discuss shortly why this is the
case and why it matters.

## Why Does This Matter?

[BUDA 530: Module1 - Page12 YouTube Video](https://youtu.be/D4-ktNbbfMo)

“Why does this matter?” is a question I’m sure you’ve started asking
yourself already. This is suppose to be an applied program and this all
looks very theoretical. The key to doing advanced statistics well is
understanding the methodology well, and understanding where these
numbers come from. Typically these estimates (the numbers) come from
estimators (equations) derived from Maximum Likelihood Theory. So let’s
take a look back to BUDA 525 and look where the OLS estimates came from.

Let’s assume that our data comes in pairs $(y_1,x_1),\ldots, (y_n,x_n)$
such that $y_i\sim N(\beta_0+\beta_1x_i, \sigma^2)$, lets for now assume
that $\sigma^2$ is known, and we’re only interested in the intercept and
the slope.

Then the log likelihood is: $$
l(\beta_0,\beta)=-n\log(\sqrt(2\pi\sigma^2))-\frac{\sum_{i=1}^n(y_i-\beta_0-\beta_1x_i)^2}{2\sigma^2}.
$$

We take the first derivative with respect to $\beta_0$ and set it equal
to zero then we solve for $\hat{\beta}_0$.

$$
\frac{\delta l(\beta_0,\beta_1)}{\delta\beta_0}= \frac{2(\sum_{i=1}^n(y_i-\beta_0-\beta_1 x_i))}{2\sigma^2}
$$ $$
0=\sum_{i=1}^ny_i -n\beta_0-\beta_1\sum_{i=1}^nx_i
$$ $$
n\beta_0 = \sum_{i=1}^ny_i-\beta_1\sum_{i=1}^nx_i
$$ $$
\hat{\beta}_0=\bar{y}-\beta_1\bar{x}
$$

From there we plug in $\hat{\beta}_0$ to the likelihood and then solve
for the slope.

$$
l(\hat{\beta}_0,\beta_1)=-n\log(\sqrt{2\pi\sigma^2})-\frac{\sum_{i=1}^n(y_i-\hat{\beta}_0-\beta_1 x_i)^2}{2\sigma^2}
$$ $$
=-n\log(\sqrt{2\pi\sigma^2})-\frac{\sum_{i=1}^n((y_i-\bar{y})-\beta_1 (x_i-\bar{x}))^2}{2\sigma^2}.
$$

Notice how I’ve grouped the terms $(y_i-\bar{y})$ and $(x_i-\bar{x})$,
this becomes very important and we want to keep those terms together.

Taking the derivative with respsect to $\beta_1$ we get: $$
\frac{dl(\hat{\beta}_0,\beta_1)}{d\beta_1}=\frac{-2\sum_{i=1}^n(x_i-\bar{x})((y_i-\bar{y})-(x_i-\bar{x}))}{2\sigma^2}.
$$

To find the MLE we then set the derivate equal to zero and solve,

$$
\frac{-2\sum_{i=1}^n(x_i-\bar{x})((y_i-\bar{y})-(x_i-\bar{x}))}{2\sigma^2}=0
$$ $$
\sum_{i=1}^n (x_i-\bar{x})(y_i-\bar{y})-\beta_1\sum_{i=1}^n(x_i-\bar{x})^2=0
$$

This gives, $$
\hat{\beta}_1=\frac{\sum_{i=1}^n(x_i-\bar{x})(y_i-\bar{y})}{\sum_{i=1}^n(x_i-\bar{x})^2}.
$$

So now you see how we came up with the OLS estimates. There is a
theoretical assumption behind the model and that’s what creates the
model. It’s not just minimizing an objective function as you may have
seen in other classes. There is theory behind each of these models and
we want to understand the basics so we can understand where they fail
and where they are successful.

## Bias

[BUDA 530: Module1 - Page13 YouTube Video](https://youtu.be/d5sAFlBFciY)

You may have heard that only use unbiased estimators should be used. To
better understand what bias is we need to define the expected value of a
random variable as: $$
E(X)=\int^{-\infty}_\infty xf(x)dx.
$$

It’s a theoretical quantity that says if our assumptions are true then
this is what we expect our value to be. Estimators (the equations), just
like random variables have expectations. We’ll discuss more about how
they relate in a few lines. For right now we say an estimator
$\hat{\theta}$ is an unbiased estimator of $\theta$ if

$$
E(\hat{\theta})=\theta.  
$$

So we define the bias of an estimator as: $$
Bias(\hat{\theta})=E(\hat{\theta})-\theta.
$$ In laymans terms how far is our estimator from the truth. This can
tell us if we’re systematically over or undersampling. There are a few
rules of expectations that we need to know.

1)  $E(aX)=aE(X)$, where $a$ is a constant and $X$ is a random
    variable.  
2)  Let $X$ and $Y$ be independent random varaibles then $$
    E(X+Y)=E(X)+E(Y)
    $$
3)  Let $a$ be a constant and $X$ be a random variable then $$
    E(X+a)=E(X)+a
    $$

### Calculating Bias

[BUDA 530: Module1 - Page14 YouTube Video](https://youtu.be/5LusqxFwn1A)

We want to evaluate the claim, “if our estimator is unbiased, then it
means we’re estimating what we are suppose to be estimating.” In other
words, we want to see if being unbiased a property that will give better
estimates.

The best way to get use to figuring how to calculate bias is to do it.

Let’s go back to our example where we assumed $x_1,\ldots,x_n$ are
independent draws from a $N(\mu,1)$. We know the MLE for $\mu$ is
$\bar{x}$. We want figure out if $\bar{x}$ is unbiased. So above is the
assumption on the data. So we know that $E(x_i)=\mu$, based on the above
assumptions.

So the expectation is, $$
E(\bar{x})=E(\frac{\sum_{i=1}^n x_i}{n})=\frac{1}{n}E(\sum_{i=1}^nx_i)
$$ $$
=\frac{1}{n}\sum_{i=1}^n E(x_i)\,\,\, \text{(by independence)}
$$ $$
= \frac{1}{n}n\mu=\mu.
$$

Since $E(\bar{x})=\mu$ we say that $\bar{x}$ is an unbiased estimator of
$\mu$, since the $Bias(\bar{x})=0$.

The calculation for the binomial example is very similar.

Let’s now look at the other Normal example, where we assume the data
comes from a $N(\mu,\sigma^2)$. The mean is unbiased still but is the
estimate of the variance unbiased? That’s what we need to look into now.

$$
E(\hat{\sigma^2})=E(\frac{1}{n}\sum_{i=1}^n (x_i-\bar{x})^2)
$$ $$
= \frac{1/n}E(\sum_{i=1}^n x_i^2+\bar{x}^2-2\bar{x}x_i).
$$

Let’s use a couple of facts $\bar{x}=\sum{i=1}^n x_i/n$.

If we use this we get that

$$
\frac{1}{n}E\left(\sum_{i=1}^n (x_i^2+\bar{x}^2-2\bar{x}x_i)\right)=\frac{1}{n}E(\sum_{i=1}^n x_i^2 + n\bar{x}^2-2n\bar{x}^2)
$$ From there we have that

$$
\frac{1}{n}E(\sum_{i=1}^n x_i^2 + \bar{x}^2-2N\bar{x}^2)=\frac{1}{n}\left(\sum_{i=1}^nE(x_i^2)-nE(\bar{x}^2)\right)= \frac{\sum_{i=1}^nE(x_i^2)}{n}-E(\bar{x}^2)
$$

Wait do we know what The $E(X^2)$ is? So we can’t finish this off just
yet, we need to understand variance which will allow us to figure out
what the $E(X^2)$ is.

## Variance

[BUDA 530: Module1 - Page15 YouTube Video](https://youtu.be/U22_NJ-Dhwo)

The other quantity we want to understand of an estimator is variance. We
define the variance of a random variable as

$$
Var(X)=E\left((X-E(X))^2\right)
$$ $$
=E(X^2-2XE(X)+E(X)^2)
$$ $$
=E(X^2)-2E(XE(X))+E(X)^2
$$

Let’s discuss some properties of variances. Assume $X$ and $Y$ are
independent random variables and that $a,b$ are constants.

1)  $Var(X+Y)=Var(X)+Var(Y)$
2)  $Var(aX)=a^2Var(X)$
3)  $Var(b)=0$ Constants don’t have variance
4)  $Var(Y+b)=Var(Y)+Var(b)=Var(Y)$

So let’s look at an example where our data $x_1,\ldots, x_n$ are
independent draws from a $N(\mu,\sigma^2)$.

By the assumption we know $$
Var(X)=\sigma^2,
$$ So let’s use that to our advantage to find $E(X^2)$.

$$
\sigma^2=E(X^2)-2E(XE(X))+E(X)^2
$$ $$
\sigma^2=E(X^2)-2\mu E(X)+\mu^2
$$ $$
E(X^2)=\sigma^2+\mu^2
$$

We know from intro statistics, that the CLT for the sample mean gives us
$\bar{x}\sim N(\mu, \frac{\sigma^2}{n})$. That means

$$
Var(\bar{X})=\frac{\sigma^2}{n}.
$$

From there we can find $E(\bar{X}^2)$ by following a similar stragegy as
above and we get

$$
E(\bar{X}^2)=\frac{\sigma^2}{n}+\mu^2
$$

#### Is the MLE For Standard Deviation Unbiased?

So let’s continue our example on claculating the bias of
$\hat{\sigma}^2$.

$$
E(\hat{\sigma^2})=\frac{\sum_{i=1}^nE(x_i^2)}{n}-E(\bar{x}^2)
$$ $$
= \frac{n\sigma^2}{n}-\frac{\sigma^2}{n}
$$ $$
= \frac{(n-1)\sigma^2}{n}.
$$

So we can see it’s not an unbiased estimate of $\sigma^2$ . Let’s
calculate the bias directly,

$$
Bias(\hat{\sigma^2})=E(\hat{\sigma^2})-\sigma^2
$$ $$
= \frac{(n-1)\sigma^2}{n}-\sigma^2
$$ $$
= \frac{-\sigma^2}{n}.
$$

The one thing to notice is that $\hat{\sigma^2}$ is not the estimate we
normally use for $\sigma^2$. We use

$$
s^2=\frac{\sum_{i=1}^n (x_i-\bar{x})}{n-1},
$$ which is an unbiased estimate of $\sigma^2$ a fact you’ll prove in
homework.

## Where Are We Going?

Now you may really asking yourself, “where is this going?” “Why do we
need to know it?” Well here’s the punch line, the key to it all. In
machine learning/data science/ data mining we want the best prediction
accuracy we can get. What that means is we want the best estimates we
can get. Do we want a unbiased estimator? What if that unbiased
estimator has high variance ? Are you still interested? What if there is
a biased estimator, that is just slightly biased but has a much smaller
variance? Would that be ok?

This concept is known as the bias-variance trade off. We define the Mean
Square Error (MSE) as

$$
E((\hat{\theta}-\theta)^2)=Var(\hat{\theta})+Bias^2(\hat{\theta}).
$$

The MSE is an important calculation because it says on average how far
is our estimator from the truth.  
Notice it breaks down to a bias variance tradeoff. If $\hat{\theta}$ is
unbiased then the MSE is just the variance of the estimator. But if we
can find a biased estimate with a smaller variance, then we should have
a better overall estimate of $\theta$.

Now you may be wondering, “why am I worrying about this.” In this class
and BUDA 535 we start talking about higher order statistical methods
that use MLE and underlying assumptions to find different models. MLE
are a big part of how we develop the base models, but then we extend it
into the machine learning world, where there is an entire field that
develops penalized MLE’s which are biased estimators that we think can
help us predict better. When you hear people talk about machine learning
this is one area they talk about, and something we will spend time on;
learning how to develop these estimates, use them, and what they
actually do comparatively. We will talk about coordinate descent
algorithms, and then Newton’s Algorithm (made famous in the movie “21”,
and by Newton’s student Joesph Rhapson).

Maximum likelihood is the one piece of theory you should know for data
science. Everything else is going to be this same structure, use a
penalized likelihood model and then solve to find an estimator. An
estimator has certain properties which are desirable in certain
situations, its our job to understand those situations, and utilize the
correct tool.
