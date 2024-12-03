1f)  in plot 1b, we see a very slanted decision boundary in logistic regression resulting from its aim to minimize classification error, not assuming any specific data distribution. In contrast, the GDA plot 1c has a near-vertical boundary, and is modeling the distribution of features for each class. We do see larger values plotted for the "x" class, so there may be a feature that has a large difference in mean pulling the line to be more vertical.
<div style="page-break-after: always;"></div>





1g) GDA performs worse than logistic regression on Dataset 1, possibly because the data is not normally distributed as we assume in GDA.




<div style="page-break-after: always;"></div>





1h) In Dataset 2, we see that one of the features of the x-class is quite large compared to the others. We could apply feature scaling to reduce the impact of that feature and result in a better prediction. One such method is subtracting the mean and dividing by the standard derivative where $\mu$ is the mean and $\Sigma$ is the stadard deviation of the features. $x'^{(i)} = \frac{x^{(i)} - \mu}{\Sigma}$.


