## Overflow and Underflow
- When rounding values, the two main problems that can occur in a computer's memory is overflow and underflow
	- Underflow is when very small numbers are rounded down to zero
	- Overflow occurs when very large numbers are approximated as $\infty$ or $-\infty$
- The softmax function is vulnerable to overflow/underflow issues
	- The softmax function is defined as
$$\text{softmax}(x)_i= \frac{e^{x_i}}{\sum _{j=1} ^{n} e ^{x_j}}$$
- To resolve this, the softmax is evaluated as $\text{softmax}(z) = x - \text{max}_i x_i$
	- The largest term in the numerator will have an exponent of 0 and at least one term in the denominator will be 1 which prevents numerator overflow and denominator underflow
	- This method is still vulnerable to underflow in the numerator
- Underflow in the numerator can cause $log(softmax(x)) = -\infty$ however, this can be solved in the same way as the original softmax
- Conditioning is how fast a function's output changes with small changes in its input
	- Poor conditioning is problematic because functions are more vulnerable to overflow and underflow
- 
## Conditioning
