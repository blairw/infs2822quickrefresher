# INFS2822 Quick Refresher
This is a quick refresher of [INFS2822](https://www.business.unsw.edu.au/degrees-courses/course-outlines/archives/INFS2822-2020-T3) (_Programming for Data Analytics_) for UNSW students.

These notes will reacquaint you with some concepts that you have previously studied in depth, but these notes will not fully explain these concepts for you. For that, please refer to your notes from when you studied INFS2822.

**Contents:**

- [💻 1. Command Line](#commandline)
- [🐍 2. Python Essentials](#python)
- [💼 3. Project Management](#projectmanagement)
- [🌐 4. Web Publishing](#webpublishing)
- [🗺️ 5. Geographical Visualisations](#geovis)
- [🥣 6. Web Scraping](#webscraping)
- [🤖 7. Machine Learning](#ml)
- [⚖️ 8. Social, Legal and Ethical Issues](#socialissues)
- [💡 9. Tips and Tricks](#tipsandtricks)

_(Itemised based on concepts, not teaching weeks.)_

<a name="commandline"></a>
## 💻&nbsp;&nbsp;1. Command Line

People by and large are used to **graphical user interfaces (GUIs)**, which are easy to use. However, for precision and power, it is beneficial to use **command line interfaces (CLIs)**. There are two families of CLIs - the _DOS_-based family (DOS, `cmd.exe` on Windows, PowerShell) and the _UNIX_-based family (UNIX, macOS, Linux). We use the UNIX-based family in INFS2822 because it's pretty much the standard for science and data work.

At the command line, there are various **shells** in which you can execute commands. The most common shell for UNIX-based work is based on Bash. In this course, we use `zsh` which is an upgrade from Bash. Note that from one shell you can move to another shell, e.g. from `zsh` we can move to `python3`.

Getting started at the UNIX command line, there are a lot of useful commands:

- `date` (not to be confused with `time`)
- `ls -lah`
- `find`
- `cat` / `head` / `tail` / `less` / `nano` / `grep`

A sequence of commands can be stored in a script. For example SQL comamnds can be stored in a `.sql` file. Likewise, Bash/zsh commands can be stored in a `.sh` file.

<a name="python"></a>
## 🐍&nbsp;&nbsp;2. Python Essentials

This section of INFS2822 is based on the Software Carpentry [Programming with Python](https://swcarpentry.github.io/python-novice-inflammation/) text.

### Basics
_This section is based on [Python Software Carpentry set 1](https://swcarpentry.github.io/python-novice-inflammation/01-intro/index.html). If you are also taking INFS1609, you may wish to compare with INFS1609 [Elementary Programming](https://blairw.github.io/infs1609quickrefresher/#elementaryprogramming) for the equivalent in Java._

- Variable assignment, e.g. `weight_kg = 60` (integer), `weight_kg = 60.0` (float), `weight_kg = 'sixty'` (String)
- Printing to the command line with `print(..)`

### Working with CSV data
_This section is based on [Python Software Carpentry set 2](https://swcarpentry.github.io/python-novice-inflammation/02-numpy/index.html)._

```python
import numpy
csvdata = numpy.loadtxt(fname='file.csv', delimiter=',')

# -- Data Types --
print(type(csvdata))       # will be <class 'numpy.ndarray'>
print(type(csvdata.dtype)) # will be float64
print(type(csvdata.shape)) # will be (rowcount, colcount)

# -- Rows and Columns --
print(csvdata[0,0])        # will be value at row 0, col 0
                           # python numbering starts at 0
print(csvdata[31,41])      # will be value at row 31, col 41
print(csvdata[31, :] )      # will be all of row 31
print(csvdata[: ,41] )      # will be all of col 41

# -- Quick Stats Examples --
print(numpy.mean(csvdata))         # mean across all rows and cols
print(numpy.max(csvdata[31, :]))   # maximum value across row 31
print(numpy.min(csvdata[: ,41]))   # minimum value across col 31
print(numpy.std(csvdata))          # standard deviation across all rows and cols

# -- Array of Statistics --
print(numpy.mean(csvdata, axis=1))  # array of averages for each row
print(numpy.mean(csvdata, axis=0))  # array of averages for each column
print(numpy.diff(csvdata[31, :])    # cell minus previous cell for row 31
```

### Generating charts/graphs
_This section is based on [Python Software Carpentry set 3](https://swcarpentry.github.io/python-novice-inflammation/03-matplotlib/index.html)._

```python
import numpy
csvdata = numpy.loadtxt(fname='file.csv', delimiter=',')

import matplotlib.pyplot as pp

# heat map
pp.imshow(data)
pp.show()

# line graph
pp.plot(numpy.mean(csvdata, axis=0))
pp.set_xlabel('x axis label goes here')
pp.set_ylabel('y axis label goes here')
pp.show()

# figure with mulitple plots
fig = pp.figure(figsize = 10.0, 3.0)
part1 = fig.add_subplot(1, 3, 1) # }
part2 = fig.add_subplot(1, 3, 2) # } each of these begins with 1,3 because the grid is 1x3
part3 = fig.add_subplot(1, 3, 3) # } then the 3rd one is just the index (starts at 1 here)

part1.plot(..)
part2.plot(..) # same syntax as above
part3.plot(..)

fig.tight_layout()
pp.savefig('file.png')
pp.show()
```

### Loops and Arrays
_This section is based on [Python Software Carpentry set 4](https://swcarpentry.github.io/python-novice-inflammation/04-loop/index.html) and [Python Software Carpentry set 5](https://swcarpentry.github.io/python-novice-inflammation/05-lists/index.html). If you are also taking INFS1609, you may wish to compare with INFS1609 [Loops](https://blairw.github.io/infs1609quickrefresher/#loops) and [Arrays](https://blairw.github.io/infs1609quickrefresher/#arrays) for the equivalent in Java._

```python
# incrementing
for number in range(1, 6):
    print(number)
    # will give you 1, 2, 3, 4, 5

# arrays (lists)
foods = ["Fish Fingers", "Custard", "Grapes"]
print(len(foods))  # will give you 2
print(foods[1])    # will give you Custard
print(foods[-1])   # will give you last element = Grapes
print(foods[-2])   # will give you 2nd last element = Custard
for this_food in foods:
    print(this_food)
```

### Combine data from multiple files
_This section is based on [Python Software Carpentry set 6](https://swcarpentry.github.io/python-novice-inflammation/06-files/index.html)._
```python
import glob
import numpy

filenames = sorted(glob.glob('dataset-2020-08-*.csv'))
for filename in filenames:
    print(filename)
```

### Selections
_This section is based on [Python Software Carpentry set 7](https://swcarpentry.github.io/python-novice-inflammation/07-cond/index.html). If you are also taking INFS1609, you may wish to compare with INFS1609 [Selections](https://blairw.github.io/infs1609quickrefresher/#selections) for the equivalent in Java._

```python
# using else-if (elif)
if x > y:
    print('x is bigger than y')
elif x > z:
    print('x is not bigger than y, but it is bigger than z')
else:
    print('x is less than y and z')

# using logical operator (and, or, etc)
if (x > y) and (x > z):
    print('z is bigger than y and z')
```

### Functions
_This section is based on [Python Software Carpentry set 8](https://swcarpentry.github.io/python-novice-inflammation/08-func/index.html). If you are also taking INFS1609, you may wish to compare with INFS1609 [Methods](https://blairw.github.io/infs1609quickrefresher/#methods) for the equivalent in Java._
```python
def bmi(mass_kg, height_m):
    numerator = mass_kg
    denominator = height_m ** 2
    return numerator / denominator
```

<a name="projectmanagement"></a>
## 💼&nbsp;&nbsp;3. Project Management

CRISP-DM methodology:

- Business Understanding
- Data Understanding
- Data Preparation
- Modeling
- Evaluation
- Deployment

<a name="webpublishing"></a>
## 🌐&nbsp;&nbsp;4. Web Publishing

Web documents are written in **Hypertext Markup Language (HTML)**. This involves tags (e.g. `<p>`) that must later be closed (e.g. `</p`>). These tags are nested inside one another in a hierarchy known as the **Document Object Model (DOM)**. The visual style of the DOM when rendered in a web browser can be designed using **Cascading Style Sheets (CSS)**.

HTML example &mdash; `index.html`
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello World</title>
        <meta charset="UTF-8">
        <link rel="stylesheet" type="text/css" href="styles.css" />
    </head>
    <body>
        <h1>Hello World!</h1>
        <p>The quick brown fox jumps over the lazy dog.</p>
    </body>
</html>
```

Corresponding CSS example &mdash; `styles.css`
```css
body {
    max-width: 900px;
    margin: 0 auto;
    font-family: 'Verdana';
}

h1 {
    color: blue;
}
```

<a name="geovis"></a>
## 🗺️&nbsp;&nbsp;5. Geographical Visualisations

<a name="webscraping"></a>
## 🥣&nbsp;&nbsp;6. Web Scraping

<a name="ml"></a>
## 🤖&nbsp;&nbsp;7. Machine Learning

<a name="socialissues"></a>
## ⚖️&nbsp;&nbsp;8. Social, Legal and Ethical Issues

<a name="tipsandtricks"></a>
## 💡&nbsp;&nbsp;9. Tips and Tricks