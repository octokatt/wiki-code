# MatPlotLib!  The Dreaded Line Graph...

Matplotlib is the default library to create charts for data analysis with Python.  It works pretty well, and I get the satisfaction of learning how to use the code set I watched all my friends in college swear at for multiple years.  Neat!


```python
from matplotlib import pyplot as plt

# sample data
days = [0, 1, 2, 3, 4, 5, 6]
money_spent = [10, 12, 12, 10, 14, 22, 24]

plt.plot(days, money_spent)
plt.show()
```


![png](output_2_0.png)



```python
time = [0, 1, 2, 3, 4]
revenue = [200, 400, 650, 800, 850]
costs = [150, 500, 550, 550, 560]

plt.plot(time, revenue)
plt.plot(time, costs)
plt.show()
```


![png](output_3_0.png)


These are pretty basic examples, and don't show off the strength of being able to generate a chart with a couple hundred points of data very quickly.  This library can chew what Excel chokes on -- nothing is worse than sending over a good chart and finding out the CFO with a 4GB Surface Pro has no idea what chart you're talking about.

### Charting with Style

Matplotlib can get much fancier.  Below are charts demonstrating some bells and whistles, and a more complete list can be found in the docs, linked [here](https://matplotlib.org/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D)


```python
from matplotlib import pyplot as plt

x = list(range(1,6))
y1 = [3.5, 3.5, 7, 7, 10.5]
y2 = [5.5, 6.5, 12, 13, 18.5]
legend_labels = ['Rogue Damage', 'Cleric Healing']

plt.plot(x, y1, color='red', linestyle='--', marker='o')
plt.plot(x, y2, color='blue', linestyle=':', marker='s')
plt.title('Two Lines on One Graph')
plt.xlabel('Level')
plt.ylabel('Damage')
plt.legend(legend_labels, loc=4)
plt.show()
```


![png](output_6_0.png)



```python
from matplotlib import pyplot as plt

x = range(7)
straight_line = [0, 1, 2, 3, 4, 5, 6]
parabola = [0, 1, 4, 9, 16, 25, 36]
cubic = [0, 1, 8, 27, 64, 125, 216]

plt.subplot(2, 1, 1)
plt.plot(x, straight_line)

plt.subplot(2, 2, 3)  # The positioning is as if the table was created and the index, even if all of that index isn't used.
plt.plot(x, parabola)

plt.subplot(2, 2, 4)
plt.plot(x, cubic)

plt.subplots_adjust(wspace=0.35, bottom=0.2)
plt.show()
```


![png](output_7_0.png)



```python
from matplotlib import pyplot as plt

month_names = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep","Oct", "Nov", "Dec"]

months = range(12)
conversion = [0.05, 0.08, 0.18, 0.28, 0.4, 0.66, 0.74, 0.78, 0.8, 0.81, 0.85, 0.85]

plt.xlabel("Months")
plt.ylabel("Conversion")

ax = plt.subplot(1, 1, 1)
plt.plot(months, conversion)
ax.set_xticks(months)
ax.set_xticklabels(month_names)
ax.set_yticks([0.10, 0.25, 0.5, 0.75])
ax.set_yticklabels(['10%', '25%', '50%', '75%'])

plt.show()
```


![png](output_8_0.png)


### Generally Useful Things

* To save a figure, use ```plt.figure(figsize=(3,3))``` and ```plt.savefig('example_name.png')```
* To remove all figures, use ```plt.close('all')```


```python

```
