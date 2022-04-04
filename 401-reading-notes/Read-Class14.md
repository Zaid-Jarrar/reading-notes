Reading from [Matplotlib Tutorial](https://github.com/rougier/matplotlib-tutorial)

## Introduction
matplotlib is probably the single most used Python package for 2D-graphics. It provides both a very quick way to visualize data from Python and publication-quality figures in many formats. We are going to explore matplotlib in interactive mode covering most common cases.

### IPython
IPython is an enhanced interactive Python shell that has lots of interesting features including named inputs and outputs, access to shell commands, improved debugging and much more. It allows interactive matplotlib sessions that have Matlab/Mathematica-like functionality.

### pyplot
pyplot provides a convenient interface to the matplotlib object-oriented plotting library. It is modeled closely after Matlab(TM). Therefore, the majority of plotting commands in pyplot have Matlab(TM) analogs with similar arguments. Important commands are explained with interactive examples.

### Animation
The easiest way to make a live animation in Matplotlib is to use one of the Animation classes.

- Animation
A base class for Animations.

- FuncAnimation
Makes an animation by repeatedly calling a function func.

- ArtistAnimation
Animation using a fixed set of Artist objects.

In both cases it is critical to keep a reference to the instance object. The animation is advanced by a timer (typically from the host GUI framework) which the Animation object holds the only reference to. If you do not hold a reference to the Animation object, it (and hence the timers) will be garbage collected which will stop the animation.

To save an animation use Animation.save, Animation.to_html5_video, or Animation.to_jshtml.

FuncAnimation
The inner workings of FuncAnimation is more-or-less:
```
for d in frames:
   artists = func(d, *fargs)
   fig.canvas.draw_idle()
   fig.canvas.start_event_loop(interval)
```
with details to handle 'blitting' (to dramatically improve the live performance), to be non-blocking, not repeatedly start/stop the GUI event loop, handle repeats, multiple animated axes, and easily save the animation to a movie file.

'Blitting' is a standard technique in computer graphics. The general gist is to take an existing bit map (in our case a mostly rasterized figure) and then 'blit' one more artist on top. Thus, by managing a saved 'clean' bitmap, we can only re-draw the few artists that are changing at each frame and possibly save significant amounts of time. When we use blitting (by passing blit=True), the core loop of FuncAnimation gets a bit more complicated:
```
ax = fig.gca()

def update_blit(artists):
    fig.canvas.restore_region(bg_cache)
    for a in artists:
        a.axes.draw_artist(a)

    ax.figure.canvas.blit(ax.bbox)
```
```
artists = init_func()

for a in artists:
   a.set_animated(True)

fig.canvas.draw()
bg_cache = fig.canvas.copy_from_bbox(ax.bbox)

for f in frames:
    artists = func(f, *fargs)
    update_blit(artists)
    fig.canvas.start_event_loop(interval)

```

This is of course leaving out many details (such as updating the background when the figure is resized or fully re-drawn). However, this hopefully minimalist example gives a sense of how init_func and func are used inside of FuncAnimation and the theory of how 'blitting' works.

The expected signature on func and init_func is very simple to keep FuncAnimation out of your book keeping and plotting logic, but this means that the callable objects you pass in must know what artists they should be working on. There are several approaches to handling this, of varying complexity and encapsulation. The simplest approach, which works quite well in the case of a script, is to define the artist at a global scope and let Python sort things out. For example
```
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
```
```
fig, ax = plt.subplots()
xdata, ydata = [], []
ln, = plt.plot([], [], 'ro')

def init():
    ax.set_xlim(0, 2*np.pi)
    ax.set_ylim(-1, 1)
    return ln,

def update(frame):
    xdata.append(frame)
    ydata.append(np.sin(frame))
    ln.set_data(xdata, ydata)
    return ln,

ani = FuncAnimation(fig, update, frames=np.linspace(0, 2*np.pi, 128),
                    init_func=init, blit=True)
plt.show()
```
The second method is to use functools.partial to 'bind' artists to function. A third method is to use closures to build up the required artists and functions. A fourth method is to create a class.


### Text introduction
matplotlib has extensive text support, including support for mathematical expressions, truetype support for raster and vector outputs, newline separated text with arbitrary rotations, and unicode support. Because it embeds fonts directly in output documents, e.g., for postscript or PDF, what you see on the screen is what you get in the hardcopy. FreeType support produces very nice, antialiased fonts, that look good even at small raster sizes. matplotlib includes its own matplotlib.font_manager (thanks to Paul Barrett), which implements a cross platform, W3C compliant font finding algorithm.

The user has a great deal of control over text properties (font size, font weight, text location and color, etc.) with sensible defaults set in the rc file. And significantly, for those interested in mathematical or scientific figures, matplotlib implements a large number of TeX math symbols and commands, supporting mathematical expressions anywhere in your figure.

### Basic text commands
The following commands are used to create text in the pyplot interface
```
text() - add text at an arbitrary location to the Axes; matplotlib.axes.Axes.text() in the API.
xlabel() - add a label to the x-axis; matplotlib.axes.Axes.set_xlabel() in the API.
ylabel() - add a label to the y-axis; matplotlib.axes.Axes.set_ylabel() in the API.
title() - add a title to the Axes; matplotlib.axes.Axes.set_title() in the API.
figtext() - add text at an arbitrary location to the Figure; matplotlib.figure.Figure.text() in the API.
suptitle() - add a title to the Figure; matplotlib.figure.Figure.suptitle() in the API.
annotate() - add an annotation, with
optional arrow, to the Axes ; matplotlib.axes.Axes.annotate() in the API.
```
All of these functions create and return a matplotlib.text.Text() instance, which can be configured with a variety of font and other properties. The example below shows all of these commands in action.
```
# -*- coding: utf-8 -*-
import matplotlib.pyplot as plt

fig = plt.figure()
fig.suptitle('bold figure suptitle', fontsize=14, fontweight='bold')

ax = fig.add_subplot(111)
fig.subplots_adjust(top=0.85)
ax.set_title('axes title')

ax.set_xlabel('xlabel')
ax.set_ylabel('ylabel')

ax.text(3, 8, 'boxed italics text in data coords', style='italic',
        bbox={'facecolor':'red', 'alpha':0.5, 'pad':10})

ax.text(2, 6, r'an equation: $E=mc^2$', fontsize=15)

ax.text(3, 2, u'unicode: Institut f\374r Festk\366rperphysik')

ax.text(0.95, 0.01, 'colored text in axes coords',
        verticalalignment='bottom', horizontalalignment='right',
        transform=ax.transAxes,
        color='green', fontsize=15)


ax.plot([2], [1], 'o')
ax.annotate('annotate', xy=(2, 1), xytext=(3, 4),
            arrowprops=dict(facecolor='black', shrink=0.05))

ax.axis([0, 10, 0, 10])

plt.show()
```

![image](https://matplotlib.org/2.0.2/_images/text_commands.png)


## Ticks
Well formatted ticks are an important part of publishing-ready figures. Matplotlib provides a totally configurable system for ticks. There are tick locators to specify where ticks should appear and tick formatters to give ticks the appearance you want. Major and minor ticks can be located and formatted independently from each other. By default minor ticks are not shown, i.e. there is only an empty list for them because it is as NullLocator (see below).

### Tick Locators
There are several locators for different kind of requirements:


- NullLocator	
No ticks.

![image](https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-NullLocator.png)

- IndexLocator	
Place a tick on every multiple of some base number of points plotted.

![image](https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-IndexLocator.png)


- FixedLocator	
Tick locations are fixed.

![image](https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-FixedLocator.png)

- LinearLocator	
Determine the tick locations.

![image](https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-LinearLocator.png)

- MultipleLocator	
Set a tick on every integer that is multiple of some base.

![image](https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-MultipleLocator.png)


- AutoLocator	
Select no more than n intervals at nice locations.

![image](https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-AutoLocator.png)

- LogLocator	
Determine the tick locations for log axes.

![image](https://github.com/rougier/matplotlib-tutorial/raw/master/figures/ticks-LogLocator.png)


All of these locators derive from the base class matplotlib.ticker.Locator. You can make your own locator deriving from it. Handling dates as ticks can be especially tricky. Therefore, matplotlib provides special locators in matplotlib.dates.


## Artist
There are three layers to the matplotlib API. The matplotlib.backend_bases.FigureCanvas is the area onto which the figure is drawn, the matplotlib.backend_bases.Renderer is the object which knows how to draw on the FigureCanvas, and the matplotlib.artist.Artist is the object that knows how to use a renderer to paint onto the canvas. The FigureCanvas and Renderer handle all the details of talking to user interface toolkits like wxPython or drawing languages like PostScript®, and the Artist handles all the high level constructs like representing and laying out the figure, text, and lines. The typical user will spend 95% of their time working with the Artists.

There are two types of Artists: primitives and containers. The primitives represent the standard graphical objects we want to paint onto our canvas: Line2D, Rectangle, Text, AxesImage, etc., and the containers are places to put them (Axis, Axes and Figure). The standard use is to create a Figure instance, use the Figure to create one or more Axes or Subplot instances, and use the Axes instance helper methods to create the primitives. In the example below, we create a Figure instance using matplotlib.pyplot.figure(), which is a convenience method for instantiating Figure instances and connecting them with your user interface or drawing toolkit FigureCanvas. As we will discuss below, this is not necessary – you can work directly with PostScript, PDF Gtk+, or wxPython FigureCanvas instances, instantiate your Figures directly and connect them yourselves – but since we are focusing here on the Artist API we’ll let pyplot handle some of those details for us:
```
import matplotlib.pyplot as plt
fig = plt.figure()
ax = fig.add_subplot(2,1,1) # two rows, one column, first plot
```
The Axes is probably the most important class in the matplotlib API, and the one you will be working with most of the time. This is because the Axes is the plotting area into which most of the objects go, and the Axes has many special helper methods (plot(), text(), hist(), imshow()) to create the most common graphics primitives (Line2D, Text, Rectangle, Image, respectively). These helper methods will take your data (e.g., numpy arrays and strings) and create primitive Artist instances as needed (e.g., Line2D), add them to the relevant containers, and draw them when requested. Most of you are probably familiar with the Subplot, which is just a special case of an Axes that lives on a regular rows by columns grid of Subplot instances. If you want to create an Axes at an arbitrary location, simply use the add_axes() method which takes a list of [left, bottom, width, height] values in 0-1 relative figure coordinates:
```
fig2 = plt.figure()
ax2 = fig2.add_axes([0.15, 0.1, 0.7, 0.3])
Continuing with our example:

import numpy as np
t = np.arange(0.0, 1.0, 0.01)
s = np.sin(2*np.pi*t)
line, = ax.plot(t, s, color='blue', lw=2)
```
In this example, ax is the Axes instance created by the fig.add_subplot call above (remember Subplot is just a subclass of Axes) and when you call ax.plot, it creates a Line2D instance and adds it to the Axes.lines list. In the interactive ipython session below, you can see that the Axes.lines list is length one and contains the same line that was returned by the line, = ax.plot... call:
```
In [101]: ax.lines[0]
Out[101]: <matplotlib.lines.Line2D instance at 0x19a95710>

In [102]: line
Out[102]: <matplotlib.lines.Line2D instance at 0x19a95710>
```
If you make subsequent calls to ax.plot (and the hold state is “on” which is the default) then additional lines will be added to the list. You can remove lines later simply by calling the list methods; either of these will work:
```
del ax.lines[0]
ax.lines.remove(line)  # one or the other, not both!
```
The Axes also has helper methods to configure and decorate the x-axis and y-axis tick, tick labels and axis labels:
```
xtext = ax.set_xlabel('my xdata') # returns a Text instance
ytext = ax.set_ylabel('my ydata')
```
When you call ax.set_xlabel, it passes the information on the Text instance of the XAxis. Each Axes instance contains an XAxis and a YAxis instance, which handle the layout and drawing of the ticks, tick labels and axis labels.


![image](https://matplotlib.org/2.0.2/_images/fig_axes_labels_simple.png)



