# 📈 Linear Regression

Linear regression is a statistical technique used to model the relationship between one (or more) input variables (features) and an output variable (label) by fitting a linear equation to observed data.

Suppose we want to predict a car’s fuel efficiency (in miles per gallon, MPG) based on its weight (in thousands of pounds). Consider the following dataset:

| Pounds (in 1000s) (feature) | Miles per Gallon (label) |
| --------------------------- | ------------------------ |
| 3.50                        | 18                       |
| 3.69                        | 15                       |
| 3.44                        | 18                       |
| 3.43                        | 16                       |
| 4.34                        | 15                       |
| 4.42                        | 14                       |
| 2.37                        | 24                       |

In algebra, a straight line can be written as:  
y = wx + b

- **y** is the output we want to predict (miles per gallon). The predicted label (output).
- **x** is the input (pounds of the car, in thousands). A feature (input).
- **w** is the slope of the line. Corresponds to the slope (w) of the line. In ML, this is a parameter learned during training.
- **b** is the y-intercept of the line. Corresponds to the y-intercept of the line. In ML, this is also a parameter learned during training.

---
