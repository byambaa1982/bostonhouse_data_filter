All code is here: https://github.com/byambaa1982/bostonhouse_data_filter/blob/master/apartments.ipynb

One of my customers wanted me to scrape a Boston government website to obtain all the database of Boston Housing and apply some filters on it.

From this gig you can see the following:

How to access Google Drive from Jupyter Notebook
How to use some filters using lambda function
Some simple data analysis
I addicted to using Google Colab recently. Google Colab is a free cloud service and now it supports free GPU! You can improve your Python programming language coding skills, develop deep learning applications using popular libraries such as Keras, TensorFlow, PyTorch, and OpenCV.

Additionally, I can access any file in my Google Drive from Google Colab using the following simple code.

```python
from google.colab import drive
drive.mount('/content/gdrive', force_remount=True)
root_dir = "/content/gdrive/My Drive/"
base_dir = root_dir + 'coderjs-v1/'
```

Once I run this code, it will give a link. Press the link and authorize it. That is it. 

Second, I want to see property type in a chart.

```python
my_series=df['Property type'].value_counts()
my_df=my_series.to_frame()


def barplot(x_data, y_data, x_label="", y_label="", title=""):
    _, ax = plt.subplots(figsize=(15, 8))
    # Draw bars, position them in the center of the tick mark on the x-axis
    ax.bar(x_data, y_data, color = '#539caf', align = 'center')
    # Draw error bars to show standard deviation, set ls to 'none'
    # to remove line between points
    ax.errorbar(x_data, y_data, color = '#297083', ls = 'none', lw = 2, capthick = 2)
    ax.set_ylabel(y_label, fontsize=16)
    ax.set_xlabel(x_label,fontsize=16)
    ax.set_title(title, fontsize=20, pad=30)
    plt.xticks(x_data, labels=x_data, rotation='vertical')


barplot( my_df.index, my_df['Property type'], x_label="Property Types", y_label="Total Number", title="What Property Type is the Most Popular" )
```

![Data](/images/pic1.png)

If you want see a cell in Classification Code, it will give us the following.
```python
df['Classification Code']
```

For example: 
```python
"0102 Apartment Condo"
```

But we use only the first four digits. In order to do that, we need the following functions.
```python
def only_first(mystr):
  try:
    new_str=re.split(' ', mystr)
    return new_str[0]
  except:
    np.nan
```

Let's apply only_first() function using lambda funtion on every cell. 
```python
df['filter3']=df['Classification Code'].map(lambda row: only_first(row))
```

A lot more in jupyter notebook page. 


