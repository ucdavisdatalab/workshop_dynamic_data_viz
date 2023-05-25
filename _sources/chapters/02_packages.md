(dynamic-visualization-packages)=
Dynamic Visualization Packages
==============================

This chapter provides an overview of the various packages, libraries, and other
tools available for creating dynamic visualizations. The sections are organized
by language, with JavaScript first because many packages for R and Python build
on JavaScript libraries.


JavaScript
----------

There are numerous data visualization libraries for JavaScript. This is a
select list of ones that seem relevant to R and Python users:

* [D3][]
    - [Vega][]
    - [Vega-lite][]
    - [Observable][]

* [Highcharts][]

* [Bokeh][]

* [Plotly][]


[D3]: https://d3js.org/
[Vega]: https://vega.github.io/
[Vega-Lite]: https://vega.github.io/
[Observable]: https://observablehq.com/

[Chart.js]: https://www.chartjs.org/
[Highcharts]: https://www.highcharts.com/
[Bokeh]: https://bokeh.org/
[Plotly]: https://plotly.com/


R
-

Animation:

* [gganimate][]
* [magick][]
* [animation][]

[gganimate]: https://gganimate.com/
[magick]: https://docs.ropensci.org/magick/
[animation]: https://yihui.org/animation/

Desktop or client-side (and sometimes also server-side):

* [rbokeh][]
* [Plotly][r-plotly]
* [ggplotly][] (by Plotly)
* [flexdashboard][]
* [Highcharter][]

[rbokeh]: https://hafen.github.io/rbokeh/
[r-plotly]: https://plotly.com/r/
[ggplotly]: https://plotly.com/ggplot2/
[flexdashboard]: https://pkgs.rstudio.com/flexdashboard/
[Highcharter]: https://jkunst.com/highcharter/


Server-side only:

* [Shiny][]
* [Dash][] (by Plotly)

[Shiny]: https://shiny.posit.co/
[Dash]: https://plotly.com/dash/


Other:

* [htmlwidgets][]

[htmlwidgets]: http://www.htmlwidgets.org/


Python
------

Animation:

* [Matplotlib][mpl-animation]
* [Pillow][]

[mpl-animation]: https://matplotlib.org/stable/tutorials/introductory/animation_tutorial.html
[Pillow]: https://pillow.readthedocs.io/en/stable/

Desktop or client-side (and sometimes also server-side):

* [Bokeh][]
* [Plotly][py-plotly]
* [Plotly Express][plotly-express]
* [mpld3][]
* [pygal][]
* [HoloViews][]
* [Matplotlib][]
* [Altair][]

[py-plotly]: https://plotly.com/python/
[plotly-express]: https://plotly.com/python/plotly-express/
[mpld3]: http://mpld3.github.io/
[pygal]: https://www.pygal.org/en/stable/
[HoloViews]: https://holoviews.org/
[Matplotlib]: https://matplotlib.org/
[Altair]: https://altair-viz.github.io/

Server-side only:

* [ipywidgets][] (or Jupyter Widgets)
* [Streamlit][]
* [Dash][] (by Plotly)
* [Shiny][]
* [Voila][]
* [Flask][]
* [Django][]

[ipywidgets]: https://ipywidgets.readthedocs.io/en/stable/
[Streamlit]: https://streamlit.io/
[Voila]: https://voila.readthedocs.io/en/stable/
[Flask]: https://flask.palletsprojects.com/en/
[Django]: https://www.djangoproject.com/

Other (mostly GUI packages):

* [tkinter][]
* [PyGObject][]
* [PySide][]

[tkinter]: https://docs.python.org/3/library/tkinter.html
[PyGObject]: https://www.gtk.org/docs/language-bindings/python
[PySide]: https://wiki.qt.io/Qt_for_Python
