# speed-check
This is a jupyter notebook that I put together when I was frustrated by all the speeding cars passing my window. I live in a rural area on a two lane road. The speed limit is 35 mph on the road, with some areas marked for slower speeds. My house in on a straight section of the road, and cars can really get going. So I built this notebook to use my USB camera and a Linux computer to host a Jupyter notebook to solve my problem.
## The primary module is speed-watch.ipynb, which does the following:
- It sets up the necessary imports: 
-    from datetime import datetime
-    import os
-    import cv2
-  Initializes some variables
-  Creates some helper functions:
-    get_filename(): This function builds a file name from a date and time stamp.
-    def speed_in_mph: This function calculates the speed by taking the x location of the rectangle that is created around a car or truck that is detected, and doing a calculation based on how fast it moves in terms of pixels, how many pixels it transverses, how many feet that represents on the road, and translates from feet per second to miles per hour. I measured the viewport in terms of feet with tape measure. I divide those feet by the portion of the field of view that the vehicle passes.
-    def found_a_car: This function converts a location data structure into pixel locations, then calls the speed_in_mph to return the speed of the vehicle.
-    def look_for_cars: This function does the bulk of the work. It defines some variables, sets up the camera video collector at 320 by 180 pixels, and calls a Haar Cascade function to return the location of a vehicle if any. If it finds one, it starts tracking it's position and recording a video file until it passes out of the field of view. It then calls the speed detection functions, puts the speed in the recorded video file, and logs a message to the terminal with the date, time, and speed. If the speed was not greater than 35 MPH then it erase the file. So it only preserves videos of the speeders. The files are stored in a directory called cars-and-trucks. 
## There are some variables that need to be tailored to your environment. 
-  distance_traveled = field_traveled * 65 # this is the measured field of view for the camera measured at the center of the pavement from one end of the field of view to the other. 
-  I found that 320 by 180 produced the fewest false positives on detecting cars. It kept seeing cars in the leaves and rocks across the street until I reduced the resolution. 
