# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:28.08.26

NAME:HEMANATH S

REG NO: 212224230094

DATASET:BME SALES(2010-2024)

### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_csv("/content/BMW sales data (2010-2024).csv")

data.columns = data.columns.str.strip()

yearly = data.groupby('Year')['Sales_Volume'].sum().to_frame()

years = yearly.index.tolist()
sales = yearly['Sales_Volume'].tolist()

X = [i - years[len(years)//2] for i in years]

n = len(X)

x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, sales)]

b = (
    n * sum(xy) - sum(sales) * sum(X)
) / (
    n * sum(x2) - sum(X)**2
)

a = (sum(sales) - b * sum(X)) / n

linear = [a + b*x for x in X]

x3 = [i**3 for i in X]
x4 = [i**4 for i in X]

x2y = [i*j for i, j in zip(x2, sales)]

A = np.array([
    [n, sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
])

B = np.array([
    sum(sales),
    sum(xy),
    sum(x2y)
])

a2, b2, c2 = np.linalg.solve(A, B)

poly = [
    a2 + b2*x + c2*(x**2)
    for x in X
]

print("Trend Equations\n")

print(
    f"Linear Trend: y = {a:.2f} "
    f"{'+' if b >= 0 else '-'} {abs(b):.2f}x"
)

print(
    f"\nPolynomial Trend: y = {a2:.2f} "
    f"{'+' if b2 >= 0 else '-'} {abs(b2):.2f}x "
    f"{'+' if c2 >= 0 else '-'} {abs(c2):.2f}x²"
)

plt.figure(figsize=(7, 5))

plt.plot(
    years,
    sales,
    color='blue',
    marker='o',
    linewidth=2,
    label='Actual'
)

plt.plot(
    years,
    linear,
    color='black',
    linestyle='--',
    linewidth=2,
    label='Linear Trend'
)

plt.title("Linear Trend Estimation")
plt.xlabel("Year")
plt.ylabel("Sales Volume")
plt.legend()
plt.grid(False)
plt.show()

plt.figure(figsize=(7, 5))

plt.plot(
    years,
    sales,
    color='blue',
    marker='o',
    linewidth=2,
    label='Actual'
)

plt.plot(
    years,
    poly,
    color='black',
    linestyle='--',
    linewidth=2,
    label='Polynomial Trend'
)

plt.title("Polynomial Trend Estimation (Degree 2)")
plt.xlabel("Year")
plt.ylabel("Sales Volume")
plt.legend()
plt.grid(False)
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION

<img width="629" height="470" alt="image" src="https://github.com/user-attachments/assets/392dd0b4-001e-4797-b247-5cdb990edecc" />

B- POLYNOMIAL TREND ESTIMATION

<img width="628" height="472" alt="image" src="https://github.com/user-attachments/assets/9b6336e3-d49a-4488-9438-50a596c0f481" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
