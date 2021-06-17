# MatPlotLib Qualitative Graphing Notes

So, last time was all of the line graphs.  Now for all those other silly kinds of graphs.

The good news is most of the labeling and fiddling is the same across any kind of graph, but some labels are more necessary than others.  Bar graphs without a labeled x-axis are particularly useless, as are pie charts without legends.


```python
from matplotlib import pyplot as plt

drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
sales =  [91, 76, 56, 66, 52, 27]

plt.bar(range(len(drinks)), sales)
ax = plt.subplot(1, 1, 1)
ax.set_xticks(range(len(drinks)))
ax.set_xticklabels(drinks)

plt.show()
```


![png](output_1_0.png)


# Bar Graphs with more than One Bar

Making a two-bar plot is annoying enough that Excel will sound nice.  Still, if it's a large dataset, this is still nicer, it just takes a little extra code.  Remember that by default bars are 2u apart, so split bars should be 0.8, etc.  The following code has a nice way of breaking down the needed widths so Python can do the really annoying parts of the design.

Stacked bar graphs are a little easier, as seen in the second example.


```python
from matplotlib import pyplot as plt

drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
sales1 =  [91, 76, 56, 66, 52, 27]
sales2 = [65, 82, 36, 68, 38, 40]

n1 = 1    # Relative Number of Dataset
n2 = 2
t = 2    # Total Number of Datasets
d = 6    # Number of Dimensions
w = 0.8  # Width of the bars
store1_x = [t*element + w*n1 for element in range(d)]
store2_x = [t*element + w*n2 for element in range(d)]

plt.bar(store1_x, sales1)
plt.bar(store2_x, sales2)
plt.show()
```


![png](output_3_0.png)



```python
from matplotlib import pyplot as plt

drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
sales1 =  [91, 76, 56, 66, 52, 27]
sales2 = [65, 82, 36, 68, 38, 40]
legend_values = ['Location 1', 'Location 2']

ax_stack = plt.subplot(1, 1, 1)
ax_stack.set_xticks(range(len(drinks)))
ax_stack.set_xticklabels(drinks)

plt.bar(range(len(drinks)), sales1)
plt.bar(range(len(drinks)), sales2, bottom=sales1)
plt.legend(legend_values)
plt.show()
```


![png](output_4_0.png)



```python
from matplotlib import pyplot as plt

drinks = ["cappuccino", "latte", "chai", "americano", "mocha", "espresso"]
ounces_of_milk = [6, 9, 4, 0, 9, 0]
error = [0.6, 0.9, 0.4, 0, 0.9, 0]

ax_err = plt.subplot(1, 1, 1)
ax_err.set_xticks(range(len(drinks)))
ax_err.set_xticklabels(drinks)

plt.bar(range(len(ounces_of_milk)), ounces_of_milk, yerr=error, capsize=5)
plt.show()
```


![png](output_5_0.png)



```python
from matplotlib import pyplot as plt
import numpy as np

unit_topics = ['Limits', 'Derivatives', 'Integrals', 'Diff Eq', 'Applications']
As = [6, 3, 4, 3, 5]
Bs = [8, 12, 8, 9, 10]
Cs = [13, 12, 15, 13, 14]
Ds = [2, 3, 3, 2, 1]
Fs = [1, 0, 0, 3, 0]

x = range(5)

c_bottom = np.add(As, Bs)
d_bottom = np.add(c_bottom, Cs)
f_bottom = np.add(d_bottom, Ds)

plt.figure(figsize=(10,8))
ax = plt.subplot()
plt.bar(range(len(As)), As)
plt.bar(range(len(Bs)), Bs, bottom=As)
plt.bar(range(len(Cs)), Cs, bottom=c_bottom)
plt.bar(range(len(Ds)), Ds, bottom=d_bottom)
plt.bar(range(len(Fs)), Fs, bottom=f_bottom)

ax.set_xticks(range(len(unit_topics)))
ax.set_xticklabels(unit_topics)

plt.title('Grade distribution')
plt.xlabel('Unit')
plt.ylabel('Number of Students')

plt.show()
```


![png](output_6_0.png)



```python
from matplotlib import pyplot as plt

exam_scores1 = [62.58, 67.63, 81.37, 52.53, 62.98, 72.15, 59.05, 73.85, 97.24, 76.81, 
                89.34, 74.44, 68.52, 85.13, 90.75, 70.29, 75.62, 85.38, 77.82, 98.31, 
                79.08, 61.72, 71.33, 80.77, 80.31, 78.16, 61.15, 64.99, 72.67, 78.94]
exam_scores2 = [72.38, 71.28, 79.24, 83.86, 84.42, 79.38, 75.51, 76.63, 81.48,78.81,
                79.23,74.38,79.27,81.07,75.42,90.35,82.93,86.74,81.33,95.1,86.57,
                83.66,85.58,81.87,92.14,72.15,91.64,74.21,89.04,76.54,81.9,96.5,80.05,
                74.77,72.26,73.23,92.6,66.22,70.09,77.2]

plt.figure(figsize=(10, 8))

plt.hist(exam_scores1, bins=12, normed=1, histtype='step', linewidth=2)
plt.hist(exam_scores2, bins=12, normed=1, histtype='step', linewidth=2)

legend_values = ['1st Yr Teaching', '2nd Yr Teaching']
plt.legend(legend_values)

plt.title('Final Exam Score Distribution')
plt.xlabel('Percentage')
plt.ylabel('Frequency')

plt.show()
```


![png](output_7_0.png)


### Line Graphs with Neat Features


```python
from matplotlib import pyplot as plt

months = range(12)
month_names = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
revenue = [16000, 14000, 17500, 19500, 21500, 21500, 22000, 23000, 20000, 19500, 18000, 16500]

ax = plt.subplot(1, 1, 1)
ax.set_xticks(months)
ax.set_xticklabels(month_names)

y_lower = [i*0.9 for i in revenue]
y_upper = [i*1.1 for i in revenue]

plt.plot(months, revenue)
plt.fill_between(months, y_lower, y_upper, alpha=0.2)

plt.show()
```


![png](output_9_0.png)


### Pie Charts

Yay pie charts!  Almost as good as cake.

Note, always use the ```plt.axis('equal')``` statement, as otherwise the pie chart will default to weirdly tilted.  No one likes tilted pie charts.  


```python
from matplotlib import pyplot as plt

payment_method_names = ["Card Swipe", "Cash", "Apple Pay", "Other"]
payment_method_freqs = [270, 77, 32, 11]

plt.pie(payment_method_freqs, autopct='%0.1f%%')
plt.axis('equal')
plt.legend(payment_method_names)

plt.show()
```


![png](output_11_0.png)

