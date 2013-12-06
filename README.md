ShapeReducer
============

This library has been modified from it's original usage. All credit goes to the original creator.

Why
===

I needed something that would reduce the number of points along a given path for creating a limited point polygon in a MapView. This should work for both `UIMapView` and the Google Maps SDK `GMSMapView`. I like this library, but it wasn't extensible enough for my needs. So I created some helper methods that would allow me to pass in my array of points (which I already had) rather than loop through again and create the points manually for the `Shape`.

    @interface Shape : NSObject
    - (id)initWithPoints:(NSArray *)points;

Implementation
==============

This example extracts the points from a `UIBezierPath`.

    NSMutableArray *coords = [[NSMutableArray alloc] init];
    
    for (NSValue *value in points) { // points is an array of points extracted from UIBezierPath
        CGPoint point = [value CGPointValue];
        CLLocationCoordinate2D coord = [self.mapView.projection coordinateForPoint:point];
        // CLLocation object allows us to save to the array while still keeping our actual coords
        CLLocation *loc = [[CLLocation alloc] initWithLatitude:coord.latitude longitude:coord.longitude];
        [coords addObject:loc];
    }
    Shape *shape = [[Shape alloc] initWithPoints:coords];
    ShapeReducer *reducer = [[ShapeReducer alloc] init];
    Shape *newShape = [reducer reduce:shape tolerance:.005];
    NSArray *newPoints = newShape.points;
    
The tolerance can be manipulated to suit your needs. Setting it to .005 takes 150 points and reduces it to around 15. The smaller the number, the fewer points you will get. Set it too low and you will not get enough points to create a polygon. Too high, and you aren't much better off than when you started.


Original README
===============

Path optimization using the Douglas-Peucker Line Approximation Algorithm in Objective C

http://en.wikipedia.org/wiki/Ramer-Douglas-Peucker%5Falgorithm

Written by Tomislav Filipčić <tomislav@me.com>. Ported from PHP port by Quentin Zervaas <http://www.phpriot.com/articles/reducing-map-path-douglas-peucker-algorithm>
