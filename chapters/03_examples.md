Creating Dynamic Visualizations
===============================

This chapter provides two hands-on examples of how to create dynamic data
visualizations. The examples don't go into much depth---think of them as a
first bite rather than a full meal.

Setup
-----

The examples include code for both R and Python, so you can follow along in
your preferred language. Note that outputs are not shown, because interactive
visualizations don't work well in this book format.

:::{important}
You can pick one language, you don't have to follow with both.
:::

* For R, we recommend running the code in an [R Notebook][] in [RStudio][].
  The R examples were tested with these software versions:

    - [R][] 4.2.2
    - [rmarkdown][] 2.21
    - [palmerpenguins][] 0.1.1
    - [rbokeh][] 0.5.1
    - [plotly][plotly-r] 4.10.1

* For Python, we recommend running the code in a [Jupyter Notebook][Jupyter] in
  [JupyterLab][jl]. The Python examples were tested with these software
  versions:

    - [Python][] 3.11.3
    - [jupyterlab][jl] 4.0.0
    - [pandas][] 2.0.1
    - [seaborn][] 0.12.2
    - [bokeh][] 3.1.1
    - [plotly][] 5.14.1
    - jupyter-dash 0.4.2
    - [ipywidgets][] 8.0.6

[R Notebook]: https://bookdown.org/yihui/rmarkdown/notebook.html
[RStudio]: https://posit.co/products/open-source/rstudio/
[R]: https://www.r-project.org/
[rmarkdown]: https://cran.r-project.org/web/packages/rmarkdown/index.html
[palmerpenguins]: https://allisonhorst.github.io/palmerpenguins/
[rbokeh]: https://hafen.github.io/rbokeh/
[plotly-r]: https://plotly.com/r/

[Jupyter]: https://jupyter-notebook.readthedocs.io/en/latest/
[Python]: https://www.python.org/
[jl]: https://jupyterlab.readthedocs.io/en/latest/
[pandas]: https://pandas.pydata.org/
[seaborn]: https://seaborn.pydata.org/
[bokeh]: https://docs.bokeh.org/en/latest/
[plotly]: https://plotly.com/python/
[ipywidgets]: https://ipywidgets.readthedocs.io/en/stable/


[Visual Studio Code]: https://code.visualstudio.com/

The examples use the [Palmer Penguins data set][penguins], which was collected
by [Dr. Kristen Gorman][gorman] at [Palmer Station, Antarctica][palmer], and
packaged for public use by [Alison Horst][horst]. The data set consists of
observations of hundreds of individual penguins from three different species:
[Adélie][], [Chinstrap][], and [Gentoo][].

[penguins]: https://allisonhorst.github.io/palmerpenguins/
[gorman]: https://www.uaf.edu/cfos/people/faculty/detail/kristen-gorman.php
[palmer]: https://pallter.marine.rutgers.edu/
[horst]: https://allisonhorst.com/
[Adélie]: https://en.wikipedia.org/wiki/Ad%C3%A9lie_penguin
[Chinstrap]: https://en.wikipedia.org/wiki/Chinstrap_penguin
[Gentoo]: https://en.wikipedia.org/wiki/Gentoo_penguin

The data set is provided by the `palmerpenguins` package in R and the `seaborn`
package in Python. Install the relevant package if you haven't already, and
then load the data set:

:::{tab-set-code}
```{code-block} r
# Install the `palmerpenguins` package:
# install.packages("palmerpenguins")


# Then load the penguins data.
library("palmerpenguins")
head(penguins)
```

```{code-block} python
# Install the `seaborn` package. For example:
# !conda install -c conda-forge seaborn


# Then load the penguins data.
import seaborn as sns
penguins = sns.load_dataset("penguins")
penguins.head()
```
:::

The visualizations will show the data grouped by species, so split the data
into three separate data frames, one for each species:

:::{tab-set-code}
```{code-block} r
by_species = split(penguins, penguins$species)
adelie = by_species$Adelie
chinstrap = by_species$Chinstrap
gentoo = by_species$Gentoo
```

```{code-block} python
by_species = penguins.groupby("species")
adelie = by_species.get_group("Adelie")
chinstrap = by_species.get_group("Chinstrap")
gentoo = by_species.get_group("Gentoo")
```
:::

Preparing the data by making sure it has an appropriate shape and is split into
the desired subsets is a common first step for creating visualizations. This is
especially true for dynamic visualizations because most dynamic visualization
packages provide little or no support for manipulating the data. It needs to be
ready to go before you start constructing the visualization!


Bokeh
-----

[Bokeh][] is a JavaScript library and Python package for creating client-side
interactive visualizations. The Python package also supports server-side code.
Members of the R community have created a package, rbokeh, to create Bokeh
plots from R. One of the nice things about Bokeh is that it has [excellent
documentation][bokeh-docs]. The [rbokeh package has its own
documentation][rbokeh-docs] because some of the interfaces are slightly
different.

[bokeh-docs]: https://docs.bokeh.org/en/latest/
[rbokeh-docs]: https://hafen.github.io/rbokeh/

Let's use Bokeh to make a scatter plot of penguin flipper length versus bill
length. The color and shape of each point can indicate that penguin's species.
From the description, this might sound like a static visualization, but Bokeh
adds some interactivity by default.

:::{tab-set-code}
```{code-block} r
# Install the `rbokeh` package.
# install.packages("rbokeh")


# Make the plot.
library("rbokeh")

p = figure(
    title = "Dimensions for Penguins at Palmer Station LTER",
    xlab = "Flipper length (mm)", ylab = "Bill Length (mm)")
p = ly_points(
    p, adelie$flipper_length_mm, adelie$bill_length_mm,
    glyph = "circle", color = "orange", legend = "Adelie")
p = ly_points(
    p, chinstrap$flipper_length_mm, chinstrap$bill_length_mm,
    glyph = "triangle", color = "purple", legend = "Chinstrap")
p = ly_points(
    p, gentoo$flipper_length_mm, gentoo$bill_length_mm,
    glyph = "square", color = "turquoise", legend = "Gentoo")
p
```

```{code-block} python
# Install the `bokeh` package.


# Setup to display plots in Jupyter.
from bokeh.io import output_notebook
output_notebook()

# Make the plot.
from bokeh.plotting import figure, show

p = figure(
    title = "Dimensions for Penguins at Palmer Station LTER",
    x_axis_label = "Flipper length (mm)", y_axis_label = "Bill Length (mm)")
p.circle(
    adelie.flipper_length_mm, adelie.bill_length_mm,
    color = "orange", legend_label = "Adelie")
p.triangle(
    chinstrap.flipper_length_mm, chinstrap.bill_length_mm,
    color = "purple", legend_label = "Chinstrap")
p.square(
    gentoo.flipper_length_mm, gentoo.bill_length_mm,
    color = "turquoise", legend_label = "Gentoo")
show(p)
```
:::

Bokeh also provides functions to create widgets for collecting user input. The
widgets can be connected to various aspects of a visualization, from the layout
to which data are displayed. Unfortunately, rbokeh hasn't added support for
Bokeh widgets yet, so you can only use them from Python.


Plotly
------

[Plotly][] is a JavaScript library, as well as a collection of packages for R,
Python, Julia, and a few other languages. The Plotly developers also provide a
library called [Dash][] for creating server-side dashboards in R or Python.

[Dash]: https://plotly.com/dash/

Much of the Plotly documentation is programmatically-generated, so sometimes
it's confusingly vague or light on details and examples. The [documentation for
Python][plotly-py-docs] seems slightly better than the [documentation for
R][plotly-r-docs].

[plotly-py-docs]: https://plotly.com/python/
[plotly-r-docs]: https://plotly.com/r/

Let's use Plotly to again create a scatter plot of penguin flipper length
versus bill length. However, this time the plot will only show one species at a
time and include a slider widget to control which species is visible.

Plotly calls an independent component or layer of a plot a **trace**. It may
help to think of traces like they are ggplot2 geometries or Matplotlib Artists.

When you create a widget that controls a Plotly plot, you have to specify which
JavaScript method should be called when the widget is manipulated. The Plotly
[documentation for JavaScript][plotly-js-docs] describes these methods.

[plotly-js-docs]: https://plotly.com/javascript/plotlyjs-function-reference/

:::{tab-set-code}
```{code-block} r
# Install the `plotly` package.
# install.packages("plotly")


# Make the plot.
library("plotly")

# Create a figure.
fig = plot_ly()

# Create slider steps and add markers to plot.
steps = list()
for (i in seq_along(by_species)) {
    name = names(by_species)[[i]]
    species = by_species[[i]]
  
    # Each step should make its trace visible.
    visible = (i == (1:3))
    # The method is important! This is the JavaScript method called when the
    # slider is moved.
    steps[[i]] = list(
        method = "restyle",
        args = list("visible", visible),
        label = name)
  
    # Initially, only first trace should be visible.
    fig = add_markers(
        fig, x = species$flipper_length_mm, y = species$bill_length_mm,
        name = name, type = "scatter", mode = "markers", showlegend = FALSE,
        visible = i == 1)
}

# Add slider to plot.
slider = list(
    active = 0,
    currentvalue = list(prefix = "Species: "),
    steps = steps)
fig = layout(fig, sliders = list(slider))

fig
```

```{code-block} python
# Install the `plotly` package.
# Install the `jupyter-dash` package.
# Install the `ipywidgets` package.
# It may be necessary to restart the notebook or even JupyterLab.


# Make the plot.
import plotly.graph_objects as go

# Create a figure.
fig = go.Figure()

# Create slider steps and add markers to plot.
steps = []
names = list(by_species.groups.keys())
for i in range(len(by_species)):
    name = names[i]
    species = by_species.get_group(name)

    # Each step should make its trace visible.
    visible = [False] * len(by_species)
    visible[i] = True
    # The method is important! This is the JavaScript method called when the
    # slider is moved.
    steps.append({
        "method": "restyle",
        "args": [{"visible": visible}],
        "label": name})

    fig.add_trace(
        go.Scatter(
            x = species.flipper_length_mm,
            y = species.bill_length_mm,
            name = name, mode = "markers",
            visible = False))

# Initially, only first trace should be visible.
fig.data[0].visible = True

# Add slider to plot.
slider = {
    "active": 0,
    "currentvalue": {"prefix": "Species: "},
    "steps": steps
}

fig.update_layout(sliders = [slider], height = 800)
fig.show()
```
:::
