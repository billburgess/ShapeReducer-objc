ShapeReducer
============

This library has been modified from it's original usage. All credit goes to the original creator.

Why
===

I needed something that would reduce the number of points along a given path for creating a limited point polygon in a MapView. This should work for both UIMapView and the Google Maps SDK GMSMapView.

Implementation
==============

This example extracts the points from a `UIBezierPath`


Original README
===============

Path optimization using the Douglas-Peucker Line Approximation Algorithm in Objective C

http://en.wikipedia.org/wiki/Ramer-Douglas-Peucker%5Falgorithm

Written by Tomislav Filipčić <tomislav@me.com>. Ported from PHP port by Quentin Zervaas <http://www.phpriot.com/articles/reducing-map-path-douglas-peucker-algorithm>
