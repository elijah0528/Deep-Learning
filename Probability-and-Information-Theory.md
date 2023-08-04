## Marginal Probability
- The marginal probability distribution is the probability distribution over a subset of variables
- Given $P(x,y)$, $P(x)$ can be calculated with the sum rule as shown below
$$P(x) = \sum _y P(x,y)$$
- For continuous variables, integration is used instead of summation
## Conditional Probability
- Conditional probability is given by the formula:
$$P(y|x) = \frac{P(x,y)}{P(x)}$$
- Chain rule of probabilities is given by the formula:
$$P(x^{(1)},...,x^{(n)}) = P(x^{(1)}) \Pi_{i=2}^nP(x^{(i)}|x^{(1)},...,x^{(n)})$$
## Expectation, Variance and Covariance
- For discrete variables the expected value is 
$$\mathbb{E}_{x\sim P}[f(x)] = \sum_x P(x)f(x)$$
- For continuous variables, the expected value is 
$$\mathbb{E}_{x\sim P}[f(x)] = \int p(x)f(x)dx$$
- Expected values are linear such that 
$$\mathbb{E}[\alpha f(x) + \beta g(x)] = \alpha \mathbb{E}_x[f(x)] + \beta \mathbb{E}_x[g(x)]$$
- Variance is how the values of a function vary across different $x$ values in a probability distribution
$$\text{Var}(f(x)) = \mathbb{E}[(f(x)-\mathbb{E}[f(x)])^2]$$
- The standard deviation is the square root of the variance
- Covariance is how related two variables are to one another given by the formula:
$$\text{Cov}(f(x),g(y)) = \mathbb{E}[(f(x)-\mathbb{E}[f(x)])(g(y)-\mathbb{E}[g(y)])]$$
- High absolute covariance values indicate that both values deviate greatly from the mean
- Positive covariance indicate that both variables take on high values together
- Negative covariance indicates that the variables are inversely proportional
- Low absolute values of covariance indicate that the values do not deviate from the mean
- Dependence is a stronger requirement than covariance
	- All independent variables have zero covariance but not the other way around
- The covariance matrix is a matrix of covariances where the diagonal elements give the variance
$$\text{Cov}(x)_{i,j} = \text{Cov}(x_i,x_j)$$
## Probability Distributions
**- Bernoulli Distribution**
  - Distribution over a single variables controlled by $\phi \epsilon [0,1]$ and gives the probability of a variable being equal to 1
	- Bernoulli Distribution has the following properties
$$P(x = 1) = \phi$$
$$P(x = 0) = 1- \phi$$
$$P(x=x) = \phi^x (1-\phi)^{1-x}$$
$$\mathbb{E}[x] = \phi$$
$$\text{Var}(x)= \phi(1-\phi)$$
**- Multinoulli Distribution**
  - Distribution over a single variable with a finite $k$ states parameterized by $p \epsilon [0,1]^{k-1}$
  - The $k$-th state is given by $1-1^Tp$  where $1^Tp \leq 0$
  - Used to describe categorical variables
**- Gaussian Distribution**
	- Gaussian Distribution is governed by two parameters: $\mu ^2$ and $\sigma$ 
	- Gaussian Distribution has many applications for many reasons
		- Many distributions are very close to gaussian distribution
			- Central Limit Theorem shows that the sum of many independent random variables in normally distributed
		- Gaussian Distribution encodes the most amount of uncertainty over real numbers
	- Multivariate Normal Distribution is given by the following formula
$$N(x;\mu, \Sigma) = \sqrt{\frac{1}{(2\pi)^n\text{det}(\Sigma)}}\text{exp}(-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu))$$
- The parameter $\Sigma$ gives the covariance matrix
- To evaluate the covariance matrix, the precision matrix ($\beta$) is used instead
- The Isotropic Gaussian Distribution is a simplified version whose covariance matrix is a scalar times the identity matrix
**- Exponential and Laplace Distributions**
	- The exponential distribution has a sharp point at $x=0$ and assigns a probability of 0 to all values less than 0ent variables
	- The Laplace distribution places a sharp point at an arbitrary value
**- Dirac and Empirical Distributions**
	- The Dirac delta function centers all the mass of a PDF at one point
		- This function is known as a generalized function since its defined in terms of its integrated form
			- The integral is 1 but every value except a single point is 0
		- It is given by the formula $p(x) = \delta (x-\mu)$
	- The Dirac delta function is used in empirical dhe mode'istribution
	- Empirical distribution is given by the formula:
$$\hat{p}(x) = \frac{1}{m} \sum_{i=0}^m \delta (x-x^{(i)})$$
	- Forms a PDF based on the distribution of samples
		- Empirical distribution is essentially a "counter" for samples
		- Empirical distribution is used for continuous variables - when discrete variables is considered, it simplifies to a multinoulli distribution 
**- Mixtures of Distribution**
	- Mixture distribution combines different component distributions to create a richer distribution
		- An example is the empirical distribution which combines a Diract Delta Function for every training example
	- Latent variables are variables that we cannot observe directly
		- Mixture distributions help reveal latent variables
	- Gaussian mixture models combine multiple gaussian distributions with individually parameterized mean $\mu$ and covariance $\sum$ 
		- Gaussian mixture models may also have a prior probability which indicates the model's beliefs before and after viewing $x$ 
		- The posterior probability ($P(c|x)$) is computed after the model observes $x$ 
		- The Gaussian mixture model is a universal approximater of probability densities because any smooth density can be approximated
## Useful Properties of Common Functions
**- Logistic Sigmoid**
	$$\sigma(x) = \frac{1}{1+\text{exp}(-x)}$$
	- The logistic sigmoid is used to provide $\phi$ for the Bernoulli distribution since it is bounded between $(0,1)$
	- Saturates at very large or small values when it becomes flat and insensitive to changes
	- $\sigma^{-1}$ is referred to as the logit in statistics
**- Softplus Function**
	$$\zeta(x) = log(1 + exp(x))$$
	- Useful for providing the $\beta$ or $\sigma$ parameter for Gaussian distribution since the range is $(0,\infty)$
	- Softplus function is the softened version $x^+ = \text{max}(0,x)$
**- Properties of the sigmoid and softplus functions**
$$\sigma(x) = \frac{exp(x)}{exp(x) + exp(0)}$$
$$\frac{d}{dx}\sigma(x) = \sigma(x)(1-\sigma(x))$$
$$1-\sigma(x) = \sigma(-x)$$
$$log(\sigma(x)) = -\zeta(-x)$$
$$\frac{d}{dx}\zeta(x) = \sigma(x)$$
$$\sigma^{-1}(x) = log(\frac{x}{1-x}), x \epsilon(0,1)$$
$$\zeta^{-1}(x) = log(\text{exp}(x)-1), x > 1$$
$$\zeta(x) = \int \sigma(y) dy$$
$$\zeta(x) - \zeta(-x) = x$$
## Bayes' Rule
- Bayes' Theorem calculates $P(x|y)$ given $P(y|x)$ through the formula
$$P(x|y) = \frac{P(x)P(y|x)}{P(y)}$$
- Even though $P(y)$ is in the formula, it can be calculated with the formula $P(y) = \Sigma _x P(y|x)P(x)$
## Technical Details of Continuous Variables

