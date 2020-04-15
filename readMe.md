# appendices
---

These documents complement the paper *Learning the Shape: Differential Machine Learning* by Brian Huge and Antoine Savine (Risk, 2020), including mathematical proofs, various extensions and considerations for an implementation in production.


[**DifferentialRegression.pdf**](https://github.com/differential-machine-learning/appendices/blob/master/DifferentialRegression.pdf) derives the svd regression formulas for standard, ridge and differential regression, based on eigenvalue decomposition. These formulas are implemented verbatim in the notebook [DifferentialRegression.ipynb](https://github.com/differential-machine-learning/notebooks/blob/master/DifferentialRegression.ipynb).

We also posted [here](https://differential-machine-learning.github.io/notebooks/) a working TensorFlow implementation, along with extensions and practical implementation details. 

***Automatic Adjoint Differentiation (AAD)***

Everything in the Risk paper and its complements relies on *differential labels*, the gradients of training labels to training inputs, fed to the machine learning model in an augmented dataset. We have seen that training on differentials offers a massive performance improvement, but, of course, the differential labels must be produced first.

In particularly simple textbook context, like a European call in Black & Scholes or a basket option in multi-dimensional Bachelier, differential labels are easily computed in explicit form. In low dimension, they could be computed by finite differences. In a general case with an arbitrary schedule of complex cash-flows simulated in an arbitrarily sophisticated model, closed form differentials are not available and finite differences are far too slow. In dimension 100, every training example must be computed 101 times to estimate differentials by finite differences. In addition, differentials approximated by finite differences may not be accurate enough for the purpose of training: we don't want the optimizer chasing imprecise differentials.

Introduced to finance by the ground breaking *Smoking Adjoints* (Giles and Glasserman, Risk 2006), AAD is a game changing technology allowing to compute differentials of arbitrary computations, automatically, with analytic precision, and for a computation cost of around 2 to 5 times one evaluation, depending on implementation, and *independently on the dimension of the gradient*. 

AAD arguably constitutes the most significant progress in computation finance of the past 20 years. It gave us real-time risk reports for complex Derivatives trading books and regulations like XVA, and instantaneous calibration. It made differentials massively available for research and development in finance. Quoting the conclusion of our Wilmott piece *Computation graphs for AAD and Machine Learning parts 1, 2 and 3* (Savine, Wilmott Magazine, 2019-2020):

*New implementations of AAD are pushing the limits of its efficiency, while quantitative analysts are leveraging them in unexpected ways, besides the evident application to risk sensitivities or calibration.*

To a large extent, differential machine learning is another strong application of AAD. It is AAD that gave us the massive number of accurate differentials necessary to implement it, for a very cheap computation cost, and is ultimately responsible for its spectacular performance improvement. 

The Risk paper or the complements do not cover AAD. Readers are referred to the (stellar) founding paper. [This textbook](https://www.amazon.com/Modern-Computational-Finance-Parallel-Simulations-dp-1119539455/dp/1119539455) provides a complete, up to date overview of AAD, its applications in finance, and a complete, professional implementation in modern C++.

The video tutorial below introduces its core ideas in 15 minutes:

<p align="center">
  
[![Watch the video](https://img.youtube.com/vi/IcQkwgPwfm4/maxresdefault.jpg)](https://youtu.be/IcQkwgPwfm4)

</p>

[github.com/differential-machine-learning](https://github.com/differential-machine-learning)
<img src="differential.png">
