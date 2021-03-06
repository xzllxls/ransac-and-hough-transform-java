# RANSAC and Hough Transform

Java implementation of the Hough transform and RANSAC algorithm

## RANSAC

- The constructor reads the data points from a text file into a list
- showCanvas calls execute
	- for (maxIter iterations)
		- The execute method chooses 3 points from the data list at random. Their indices are stored in the concensusSet.
		- A circle that passes through all 3 points is chosen as the current circle model
		for (all points in the data set)
			- getoffset is responsible for calculating the difference between the points and the circumference of the circle
			- Points that are within *threshold* distance are added to the consenus set 
		- The best model so far (as determined by the highest number of points in the consenus set) is kept track on during the iteration
	- The best model is returned
- showCanvas draws the data points, the best circle and the smallest width annulus on a canvas and displays the result to the user


### Methods

- (+) showCanvas() *Displays the data points and the calculated circles on a canvas.*
- (+) execute() *Runs the RANSAC algorithm.*
- (-) getOffset() *Calculate the distance between a point and the center of a circle*
- (-) getCircle() *Find the circle that passes through the three given points*
- (-) getNPoints() *Choose n data points at random* 

### Illustrations

Points from *points.r.data* are being used.

- Cirlces (x, y, r, number of points)
  - 20, 100, 100, 100
- Noise: 900 points randomly selected between -200 and 200
- smallestRadius=92.17273473900397
- highestRadius=111.01668853035679
- 18.843953791352817

![PS1](http://i.imgur.com/fs2WgVy.png)

![PS2](http://i.imgur.com/U5HaP7R.png)

![PS3](http://i.imgur.com/RR8M50p.png)

## Hough Transform

- The constructor reads the data points from a text file into a list
- A wrapped 3D array - the accumulator - is used to store information about potential circles. A circle is identified by pixel ranges for x, y and radius
- execute()
	- for (all points)
		- all circles that could have *point* on its circumference are calculated
		- for (all circles)
			- the cell in the accumulator is incremented for the given circle
- filterNeighbours removes circles that lie too close to each other. Circles with a high count are preferred.
- showCanvas draws the points and the identified circles 

The smallest width annuli for the Hough circle suffers from some offset problems, possibly caused by rounding errors.


### Methods

- (+) execute() *Executes the Hough Transform algorithm.*
- (+) showCanvas() *Render view based on this.pixels.*
- (-) getCircles() *Finds every other circle that has @point.getY() and @point.getX() as its center*

### Illustrations

Points from *points.ht.data* are being used.

- Circles (x, y, r, number of points)
  - 0, 0, 50, 50
  - 100, 140, 110, 50
  - 0, 50, 50, 50
  - 20, 100, 100, 100
- Noise: 120 points randomly selected between -200 and 200

![PS1](http://i.imgur.com/rYqX67O.png)