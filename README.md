# jenks_lite


Goal
---


This is my attempt to write script in native python that returns values grouped "logically" from a list of numbers. This script was written so that it could be implemented in ArcGIS' Model Builder.


Explanation and Example
---

"Jenks Natural Breaks" is a classification system widely used in showing quantitative data on [chloropleth](https://wikipedia.org/en/Choropleth_map) maps and in GIS such as ArcMap and QGIS. The goal of this system is to break a list of numbers (1-D matrix) into groups that so that the difference betwen groups is maximized.

So, for example,
```
data = [1, 2, 9, 10]
desired_groups = 2

# script returns [[1, 2], [9, 10]]
```

In this example, the possible lists with 2 groups are:
- [1], [2, 9, 10] <- not optimal
- [1, 2], [9, 10] <- optimal, largest difference between 2 groups
- [1, 2, 9], [10] <- not optimal

There's a lot of straightforward but computationally intensive math behind calculating this; it's an expensive thing to find. This script is my attempt to simplify this idea while still returning meaningful results.

A note
---

Despite being widely used, finding code (especially in python) for Jenks is really hard. 
- [The wiki page](https://wikipedia.org/en/Jenks_natural_breaks_optimization) doesn't give you a lot of info
- Esri doesn't want to tell you how to do it 
- the best source I can find is a script (Wayback Machine link to pdf)[https://web.archive.org/web/20110124052102/http://danieljlewis.org/files/2010/06/Jenks.pdf] written in some weird python. For example, floats are initialized separately (like ```v = 0.0```) and, more importantly, there are no comments. 

[This developer](https://macwright.com/2013/02/18/literate-jenks.html) talks in depth about this mystery. The the original paper was never put online, so the Jenks scripts that are available probably originate from a FORTRAN port from the 70s. As he puts it, 

> And so we have history in the oddest terms. The idea is lost but the Fortran code is resurrected in a new language every few years, along with a link to the last link to the unreachable text.

He eventually developed a port in JS, which seems to be depriciated in favor of a k-means algo. 