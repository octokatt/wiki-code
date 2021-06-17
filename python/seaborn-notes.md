# Seaborn

Seaborn is a package that works with dataframes from Pandas that rapidly prototypes graphs.  Once data arranging is complete, this makes life so, so easy.

In particular, Seaborn has a much easier time of plotting multiple-group bar graphs than using straight MatPlotLib.


```python
import pandas as pd
from matplotlib import pyplot as plt
import seaborn as sns

df = pd.read_csv("survey_sample.csv")

sns.barplot(data=df, x="Age Range", y="Patient ID", hue="Gender")

plt.show()
```


![png](output_1_0.png)

