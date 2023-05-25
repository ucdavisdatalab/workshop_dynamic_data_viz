Introduction
============

This chapter introduces ideas and terminology about dynamic data
visualizations. There aren't any technical examples, but these concepts are
important for understanding the rest of the material.


What Are Dynamic Visualizations?
--------------------------------

A data visualization is **dynamic** if it automatically changes over time or in
response to some input from the viewer or other sources. Any data visualization
which is not dynamic is **static**. 

:::{note}
Other sources may define dynamic data visualizations differently, and that's
okay as long as you understand what's meant! This workshop will use the
definition given above.
:::

You should already be familiar with creating static visualizations, which are
just still images. In R, you may have used ggplot2, Lattice, or the built-in
plotting functions to create static visualizations. In Python, you may have
used Pandas, Seaborn, Plotnine, or Matplotlib.

Generally, dynamic visualizations require more effort to create than static
ones. In addition to designing the visualization, you have to develop the code
to update it in response to input. Depending on what you want to display, you
may also have to learn new packages, learn new programming languages, and use
specialized hardware.

For viewers, dynamic visualizations can be double-edged. A dynamic
visualization can make the message in the data easier to understand if features
are represented in an intuitive way, such as representing time through
animation. It can also give the viewer freedom to explore aspects of the data
that interest them most. On the other hand, a dynamic visualization that
presents many options can seem overwhelming or even leave the viewer wondering
what they're supposed to take away. The novelty of dynamic visualization can
also distract from the data and the intended message.

The following subsections present several different kinds of dynamic
visualizations, in approximate order from least to most sophisticated.

:::{note}
Dynamic visualizations are especially beneficial and popular for geospatial and
network data. For geospatial data, dynamic maps make it easy to identify data
points, pan and zoom to specific areas of interest, and control which details
of the data are shown. In addition, displaying map tiles (for instance, from
[OpenStreetMap][]) under the data can provide important context. For network
data, dynamic graphs make it easy to identify nodes, identify edges on nodes,
and otherwise explore.

[OpenStreetMap]: https://www.openstreetmap.org

Within the specialized world of dynamic visualization, visualizing geospatial
and network data are further specializations. There are many packages,
libraries, and other tools specifically devoted to these tasks. This workshop
focuses on dynamic visualization more generally, and doesn't cover how to
handle geospatial or network data. If you're interested in those topics, check
out these two other workshops from DataLab:

* [Building Web Maps with Leaflet][geo]
* [Network Visualization][net]

[geo]: https://ucdavisdatalab.github.io/workshop_web_maps/
[net]: https://ucdavisdatalab.github.io/workshop_network_viz/

DataLab also has many other workshops related to data visualization and to
geospatial data. You can find an up-to-date list of our workshops
[here][workshops].

[workshops]: https://ucdavisdatalab.github.io/workshop_index/
:::


### Animation

Animated visualizations can be a great way to convey how data vary as a
specific feature varies, especially if the feature is related to time. 

One example is the animation featured in Flowing Data's article [The Changing
American Diet][us-diet].

[us-diet]: https://flowingdata.com/2016/05/17/the-changing-american-diet/

Another time series example is an animation developed by Dr. Michele Tobias and the DataLab team that maps the public AB 65 data of positive COVID-19 cases on the UC Davis campus in 2020-2023. The visualization is accompanied by a narrative and a link to the code repository.

[datalab-covidmap]: https://datalab.ucdavis.edu/2021/09/23/unlocking-insights-from-public-data-a-case-study-with-covid-19-exposure-data/

If you know how to make static visualizations, then you know *almost*
everything you need to know to make animated visualizations. An animation
displays a collection of still images, called **frames**, in rapid succession.
In an animated visualization, the frames are just static visualizations!

To make an animated visualization, first write code to generate each frame.
This code will probably look a lot like static visualization code you've
written in the past, perhaps with an added loop over the frames.

After generating the frames, you have two options: you can convert the frames
to an animated file format or write code to display the frames at speed
yourself. The first approach is simpler, and best for animations which will
always play at the same speed. The second approach is more flexible, but also
requires substantially more effort and technical knowledge.

There are packages to convert still images into an animated image format such
as [GIF][] or a video format such as [MP4][] for both R and Python. Some of
them are listed in {numref}`dynamic-visualization-packages`.

[GIF]: https://en.wikipedia.org/wiki/GIF
[MP4]: https://en.wikipedia.org/wiki/MP4_file_format

Writing code to display animation frames at speed is challenging. The code must
display the frames at a constant speed---not too fast and not too slow---or
else the animation will look choppy and disjointed. This is a common
requirement of video games, but not of the kinds of tasks for which R and
Python were designed. As a consequence, for some animations it can be difficult
or impossible to write R or Python code which runs fast enough. Nevertheless,
there are some tutorials and other resources for R, and even a few packages for
Python. Some of these are also listed in
{numref}`dynamic-visualization-packages`.


(reactivity)=
### Reactivity

Dynamic visualizations are particularly well-suited to data which are
continuously or frequently updated over time. These kinds of data are called
**streaming data**. A dynamic visualization can **react** automatically to
reflect new data, so that it's always up-to-date and viewers can monitor
changes over time. For example, the plots on the U.S. National Oceanic and
Atmospheric Administration's [San Francisco weather station][sf-weather] update
in near-real-time.

[sf-weather]: https://tidesandcurrents.noaa.gov/stationhome.html?id=9414290

Dynamic visualizations can also react to inputs that change only occasionally
or aren't time-based at all. As an example, The Pudding's [Music Bubble
Map][music-bubble] automatically shows data relevant to the viewer's
location---and also updates monthly based on the latest data from online music
services.

[music-bubble]: https://pudding.cool/2021/04/music-bubble/

Creating a reactive visualization is a bigger undertaking than creating an
animation because this kind of visualization is really a small application (a
computer program). The visualization can only react to data changes if there's
code to detect those changes and to update what's displayed---code that you
have to develop. The code will typically need to run continuously while the
visualization is being viewed, which may also make it necessary to have a
computer specifically dedicated to the task. {numref}`where-will-the-code-run`
covers this last point in more detail.

As of writing, **dashboards**---applications designed to concisely communicate
information---are very popular as a medium for reactive and interactive (see
{numref}`interactivity`) visualizations. Modern dashboards typically run within
a web browser so that viewers don't have to install anything. Dashboards will
likely become more popular as web technologies improve.
{numref}`dynamic-visualization-packages` presents many of the dashboard
packages available for R and Python.


(interactivity)=
### Interactivity

A dynamic visualization is **interactive** if it changes in response to input
from the viewer (instead of or in addition to other sources). As an example,
Information is Beautiful's [Gender Pay Gap][pay-gap] visualization includes
drop-down menus so that the viewer can choose whether gaps are shown as total
salary or percentage of salary and how jobs are sorted. Another example is The
Pudding's [Map of Places in the U.S. with the Same Name][same-name], which
prompts the viewer for a city name to look up.

[pay-gap]: https://informationisbeautiful.net/visualizations/gender-pay-gap/
[same-name]: https://pudding.cool/2023/03/same-name/

Interactive visualizations are a subcategory of reactive visualizations, so the
steps to create one are almost the same (see {numref}`reactivity`). The
difference is that you must also develop an interface to collect input from the
viewer. Typically this is a **graphical user interface** (GUI, often pronounced
"gooey"), a collection of interactive elements called **widgets**. Examples of
widgets include menus, text boxes, sliders, and buttons.

:::{note}
An application's GUI and the associated code are called the **frontend**, while
an application's processing logic and code are called the **backend**. It might
help to think of these like the body and engine, respectively, of a car. Each
can be quite complicated and has specific design requirements. Thus the
difference between interactive and reactive visualizations can be restated:

> Interactive visualizations require additional frontend code.
:::

:::{note}
The terms "widget", "graphical user interface", "frontend", and "backend" come
from software engineering. They also apply to applications which require user
input but have nothing to do with data visualization.
:::

Dashboard packages usually provide a collection of common widgets you can use
to build a GUI, often as part of a web application. There are also
general-purpose GUI packages that provide widgets for building desktop
applications, but these usually aren't designed specifically for data
visualization. {numref}`dynamic-visualization-packages` lists R and Python
packages for creating GUIs, albeit with more focus on dashboard packages than
general-purpose GUI packages.


(where-will-the-code-run)=
Where Will the Code Run?
------------------------

Most dynamic visualizations are applications. The code for the dynamic behavior
has to run in the background while the visualization is being viewed. In some
cases, such as visualizations of streaming data, the code may have to run
continuously. When you develop a dynamic visualization, it's important to
consider whether the code will run on the viewer's computer or on a computer
you control. The following subsections explain several different ways to
distribute and run dynamic visualizations.


### Web Applications

A **web application** (or web app) is one where the frontend is a collection of
web pages. Examples include the visualizations linked in {numref}`reactivity`
and {numref}`interactivity`, Jupyter Notebooks, Google Office, and
OpenStreetMap. Most dashboards are web apps.

Web apps can be hosted on a **server**---an always-on internet-connected
computer---so that viewers can run the app by navigating to a URL in their web
browser. Since web browsers are available for every modern operating system and
are often built in, viewers typically won't have to install anything. This
includes operating systems for tablets, smartphones, and other portable
devices. As a result, web apps are a great way to make a dynamic visualization
easy for a large audience to access, regardless of how much technical knowledge
they have.

Web pages are written in [hypertext markup language (HTML)][html]. They can
also include [cascading style sheets (CSS)][css] for additional formatting and
[JavaScript][js] code for reactive behavior. Familiarity with these **web
languages** is helpful for developing web apps, but not always a requirement.

[html]: https://developer.mozilla.org/en-US/docs/Web/HTML
[css]: https://developer.mozilla.org/en-US/docs/Web/CSS
[js]: https://developer.mozilla.org/en-US/docs/Web/JavaScript

When developing a web app, an important design decision is where the backend
will run. There are two options:

*  In a **server-side** web app, the backend runs on a server. The server is
   generally under your control as the app developer and distributor, so you
   can ensure that it has appropriate hardware and software for running the
   app. You can write the code for the backend in any programming language the
   server can run. A disadvantage of this approach is that it can be expensive:
   you end up paying for all of the computing your audience does, whether by
   renting a server or by buying a server and paying for its maintenance and
   electricity. This approach can also be technically challenging, especially
   for beginners.

*  In a **client-side** web app, the backend runs in the viewer's web browser
   on their computer. You have no control over the hardware, so it's important
   to consider what kinds of hardware your app's viewers might have. The code
   must be written in [JavaScript][js] or a language that can be compiled to
   [WebAssembly][wasm]. An advantage of this approach is that you don't have to
   pay for the computing your audience does. Hosting this kind of web app
   online is usually free or inexpensive.

[wasm]: https://webassembly.org/

There are several R and Python packages for creating web apps and dashboards
(see {numref}`dynamic-visualization-packages`). Most provide functions to
describe and programmatically generate the frontend. That means you can get
started without having to learn the web languages. Nevertheless, being familiar
with them is helpful for debugging and customizing your apps. Most packages
assume the backend will run on a server and be written in R or Python. The ones
that don't usually require a good understanding of [JavaScript][js].


#### As Desktop Applications

One way to get the flexibility of a server-side web app without the cost is by
distributing your web app as a desktop application. In this approach, the
viewer's computer acts as the server. The backend runs on their computer, so
the app's performance will depend on their hardware. They may also need to
install software such as R or Python before running the app. They still access
the app through a web browser.

:::{note}
Many modern desktop applications are actually web apps. Examples include
Microsoft Visual Studio Code and Slack.
:::

The disadvantage of this approach is that it requires technical knowledge on
the part of the viewers. You may have to provide them with detailed setup
instructions, and even then they may run into problems. In spite of that, if
you only plan to distribute your app to a few people, this is often the best
option.


### Desktop Applications

Creating a desktop application is the main alternative to creating a web app.
Your desktop application could simply be an executable R or Python script. For
both languages, there are packages with bindings to popular GUI toolkits for
creating application frontends.

Desktop applications have several advantages over to web apps:

* An internet connection is not required unless the application downloads data
  from the internet.
* A web browser is not required, so there's no performance penalty for running
  one.
* You can develop the application with whatever programming language and GUI
  toolkit you want.
* Your application can use hardware that may be difficult or impossible to
  access from a web app, such as graphical processing units (GPUs)---assuming
  the viewer's computer has the hardware.

However, there are also some disadvantages:

* There aren't many packages specifically for developing data visualizations
  and dashboards as desktop applications. As a consequence, you may have to
  write more code to create the frontend than you would for a web app.
* Before running the application, the viewer may have to install it. They may
  also have to install other required software, such as R or Python.
* R and Python don't have built-in tools for generating executable files, so
  the steps to run the application may be different compared to most
  applications the viewer uses.
* The performance of the application is tied to the software and hardware on
  the viewer's computer. If the application will be distributed to multiple
  viewers, it may be difficult to predict whether and how well the application
  will run.

  
Do You Need Dynamic Visualizations?
-----------------------------------

By now, you can probably see that crafting a great dynamic visualization
requires substantially more design effort, technical knowledge, programming
effort, and specialized hardware than crafting a great static visualization.
This section is a caution that while dynamic visualizations are exciting, you
might not need one to convey the information you want to convey.

Designing a dynamic visualization is challenging. In addition to all of the
design principles for static visualizations (see DataLab's [Principles of Data
Visualization][dataviz] reader for details), you must consider how your
visualization will change over time or in response to input. How will you
direct the viewer's attention to the important parts of the data? If the
visualization is interactive, how will you make sure that the viewer
understands what it's meant to communicate? Moreover, how will you ensure that
the viewer understands how to interact with the visualization?

[dataviz]: https://ucdavisdatalab.github.io/workshop_data_viz_principles/

Implementing a dynamic visualization is challenging. You'll have to learn the
programming interface for whatever dynamic visualization package you decide to
use. It's likely you'll also need to learn a little bit about animation, HTML
and JavaScript, or a widget toolkit. With so many different technologies in the
mix, debugging dynamic visualizations can be an exercise in frustration.

Distributing a dynamic visualization is challenging. You'll probably need to
provide viewers with instructions about how to set up, access, and use the
visualization. You might also have to pay for and set up a web server.

While these points may seem negative, they're intended to make you think
carefully about why you want to make a dynamic visualization before you make
one. In many cases, static visualizations work just as well or better for
summarizing data, and have a much shorter development time and easier
distribution path.
