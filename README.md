################################################################
################################################################
################################################################
#############
############# Lemon Protein 
#############
################################################################
################################################################
import math
import random
import turtle as d


############################################### Functions begin here! ###############################################

## 1. Define the (bubbles) function, which will draw an assigned number (bubblenumber) of unfilled circles using cool pastel colours, also taking a parameter for size (rads).
##      The bubbles will be placed "randomly" acround the drawing, although they will start near the turtle's mouth and later placement is biased get closer and closer to the upper left hand of the drawing window after their first 3 iterations.
##          Makes it look like there are bubbles coming out of the turtle's mouth.
## 2. Lift pen up and end fill before anything else in the function, to prevent drawing a line across whatever they came from or accidentally filling a non-shape.
## 3. Use a for loop to place each "bubble" in the sequence.
## 4. Randomly assign colour from a list of five pre-chosen (from GIMP) cool pastels.
## 5. Use if and else statements to determine the movement and size of the bubbles based upon their number in the sequence.
##      I want the first THREE bubbles to be smaller and slightly more regular than later ones, but still a random size.
##          Randomize the size (rads) parameter to make the first three bubbles 1/10th to 4/5ths of the assigned size.
##          Face the drawing turtle in a random direction anywhere between 0-180 degrees from where it is currently facing.
##      I want the later bubbles to be more random in size and less random in direction.
##          Randomize the size to be between 3/10ths and twice as big as the (rads) parameter.
##          The turtle could be facing any possible direction, so use the d.heading() method to obtain the turtle's orientation, and turn the turtle right by that amount, subtracting 180.
##              Once the orientation has been reset to this position, randomize the direction of movement within a cone of 100 degrees.
##              This biases the movement to be towards the upper left corner once the turtle moves forward, but still within an amount of random variation
## 6. Move the turtle forward by a random amount based upon the (rads) parameter.
##      I found that between 2-5 radius lengths just "looks" the best.

def bubbles(rads, bubblenumber):
    d.penup()
    d.end_fill()
    for k in range(bubblenumber):
        rollbubblecolour=("#dedeff", "#deffff", "#dee7ff", "#caccde", "#b0fffa")
        d.pen(pencolor=(random.choice(rollbubblecolour)))
        if k<3:
            d.right((random.randrange(0,180)))
            d.pendown()
            d.circle(random.randrange((rads*.1),(rads*.8)))
            d.penup()
        else:
            d.right((d.heading()-180))
            d.right((random.randrange(0,100)))
            d.pendown()
            d.circle(random.randrange((rads*.3),(rads*2)))
            d.penup()
        d.forward(random.randrange((rads*2),(rads*5)))

## The clockwisecircle() function creates a circle going clockwise rather than counterclockwise.
##      Python's turtle.circle() will already do this if the parameters are negative, but I needed more for loops to meet the criteria of the assignment.
## 1. The parameter (degrees) is how many degrees will be completed. 360 makes a full circle.
## 2. The parameter (size) is how long each "step" of the function is.
## 3. This will draw a circle based on turning by an increment of 1 degree every time it moves forward.
##      This moves much more slowly than the built in negative circle function, even at max pen speed, so USE SPARINGLY or the drawing will take a million years.

def clockwisecircle(degrees, size):
    for i in range (degrees):
        d.forward(size)
        d.right (1)

## 1. Define a function to draw the turtle's eyes. Take only one parameter (big), which determines the size of the eyes.
## 2. The first circle will be the sclera, so set the pen colour to dark blue and the fill to very light blue.
##      The eyes will be smaller than the rest of the drawing, so make the pen thinner so the details show up better.
##      Picked a blue tints rather than solid black or white to make it look like the turtle is underwater.
## 3. Move towards the center of the circle by a tenth of the initial circle's radius.
##      By using a fraction of the radius, the turtle will appear to be looking at something rather than just derpalerping off into space.
## 4. Call the filledcircle() function to draw a solid circle for the iris, 2/3rds of the initial circle's size.
##      The filledcircle() iris will use the eyecolour variable assigned earlier as its colour parameter, which rolls a random hexadecimal value between #000000 (black) and #FFFFFF (white).
## 5. Move the drawing forward by 20% to put the pupil just *slightly* off-center
## 6. Call the filledcircle() function, set the radius to 1/3 of the original circle, and fill the pupil with black.


def eyes(big):
    d.pen(fillcolor="#e3f7fb", pencolor="#3f48cc", pensize="2")
    d.begin_fill()
    d.circle(big)
    d.end_fill()
    d.penup()
    d.left(90)
    d.forward(big/10)
    d.right(90)
    filledcircle(((big)*2)/(3),(eyecolour))
    d.left(90)
    d.forward(big/5)
    d.right(90)
    filledcircle(big/3,"#262f91")
    d.left(60)
    d.forward(big/1.2)
    filledcircle((big*3)/7, "#effffe")
    d.left(170)
    d.forward(big)
    filledcircle((big/8), "#effffe")

## filledincircle() creates a circle with a radius of (radius) and a solid colour of (filling).
## This function will be used for mostly for detailing, and the pendown() and penup() should be included the function.
        
def filledcircle(radius,filling):
    d.pendown()
    d.pen(fillcolor=(filling), pencolor=(filling))
    d.begin_fill()
    d.circle(radius)
    d.end_fill()
    d.penup()



## 1. Define a function that can be used to draw half a crescent shape that take parameters for length (longness), orientation (left or right), and colour.
## 2. This function will be used to draw the turtle's tail and the turtle's mouth.
##      The turtle's mouth will need to have a matching outline and fill, but the turtle's tail must have an outline.
##      This means that the pen colour must be defined prior to calling the function, and not in the function itself.
##          Assign the parameter (colour) to the fill only, and do not assign the pen colour at all in this function.
## 3. Use if and else to determine which way the crescent will face. The directions and angles are simply inverted
## 4. Not very mathematical, but guess and test which angles and arc lengths will intersect appropriately to make a closed crescent shape.
##      They will remain functional, even when scaled up, so long as all parameters relating to length are also scaled up appropriately.
## 5. End the fill, but do not pick up the pen, as the tail lines must connect to those of the shell.

def halfcrescent(longness, orientation, colour):
    d.pen(fillcolor=(colour))
    d.pendown()
    d.begin_fill()
    if (orientation)=="left":
        d.circle((longness),-60)
        d.left(25)
        d.circle((longness),60)
        d.right(150)
        d.circle((longness*.8),30)
    else:
        d.circle((longness),60)
        d.right(25)
        d.circle((longness),-60)
        d.left(150)
        d.circle((longness)*.8,-30)
    d.end_fill()

## 1. Define a function that places and orients the pen by taking three parameters for the x position, the y position and the angle.
## 2. The pen needs to stay in the right place on the outer shell and be facing the right direction to avoid slipping off the line when it travels around the turtle drawing.
## 3. To make use of this function, print d.pos() and d.heading() when the pen is at the appropriate spots in the drawing, before any functions are called or any rotations are made.
## 4. Type those values into the placement() function after the pen is done whatever thing it is drawing.

def placement(first, second, angle):
    d.penup()
    d.goto(first, second)
    if ((str(angle)).isdigit()):
        d.right((d.heading())-(angle))
    d.pendown()

## 1. Define the function polyshell() to draw a pentagon for the turtle's shell and extrude a line at every corner, evenly bisecting the space on the outside of each corner.
## 2. Since the for loop starts on the outer edge of the circle, the turtle must first go forward.
## 3. In a regular polygon with identical sides, the internal angle is (the number of sides)-2 multiplied by 180, and then divided by the total number of sides for every corner.
##      From the drawing turtle's perspective, half of those degrees are on the left, and half are on the right.
##      To get it to make a "perfect" pentagon, it must turn that "half" amount to the right or to the left.    
## 4. For a regular polygon, the length of its sides can be calculated from its radius using the formula s=2rsin(180/n)
##      n= the number of sides, s= side length and r= radius
## 5. Use a for loop to repeat the action the appropriate amount of times to complete the polygon.
##      Use the parameter "sidenumber" for this purpose.

def polyshell(length,sidenumber):
    sidelength=((2*(length)*(math.sin((math.pi)/(sidenumber)))))
    angle=((((sidenumber)-2)*180)/(sidenumber)/2)
    for i in range (sidenumber):
        d.forward(length)
        d.right(angle)
        d.forward(sidelength)
        d.right(angle)
        d.forward(length)
        d.left(180)

## 1. Define a function(rollshell) to return the random colour values of the turtle's shell.
## 2. The colour palette tool in GIMP (GNU Image Manipulation Program) can be used to choose colours and will return hexidecimal values for any colour picked.
##    Pick a range of two colours that would not look horrific in the turtle's shell.
##          A cool desaturated colour palette is used for the rest of the fills and pen colours, so I chose values between a dull purple (897AC1) and a green (8bc17a).
##          When these values are converted to decimal they are 9009857 and 9159034 respectively.
## 3. Plug these numbers into randrange and assign to the rolledshellcolour variable.

def rollshell():
    return((random.randrange(9009857, 9159034)))
rolledshellcolour=(rollshell())

## 1. Define a function to draw the front flippers. They are longer and narrower than the hind flippers
## 2. Take two parameters for the orientation and the size.
## 3. Use an if/else statement so that a "right" orientation multiplies the radius of every circle by -1, flipping them on the y axis.
## 4. The (size) parameter multiplies the radius of each circle by whatever it happens to be.
## 5. Draw the flippers with partial circles to make them look organic.

def front_flipper(orientation, size):
    d.pendown()
    if orientation=="right":
        loright=-1*(size)
    else:
        loright=1*(size) 
    d.begin_fill()
    d.circle(60*(loright), 60)
    d.circle(-100*(loright), 60)
    d.circle(100*(loright),30)
    d.circle(-100*(loright),30)
    d.circle(-5*(loright),110)
    d.circle(-300*(loright), 20)
    d.circle(-50*(loright),10)
    d.circle(-400*(loright),15)
    d.circle(-80*(loright),70)
    d.end_fill()
    d.penup()

## This function draws the hind flippers.
## It is basically the same as the front flippers, but with different dimensions.

def back_flipper(oriented, size):
    d.pendown()
    if oriented=="right":
        leftright=-1*(size)
    else:
        leftright=1*(size) 
    d.begin_fill()
    d.circle(100*(leftright),20)
    d.circle(-100*(leftright),20)
    d.circle(-9*(leftright),30)
    d.circle(-100*(leftright),15)
    d.circle(-70*(leftright),60)
    d.circle(-20*(leftright),80)
    d.circle(-120*(leftright),50)
    d.circle(100*(leftright),30)
    d.end_fill()
    d.penup()


############################################### Functions end here! ###############################################

## Some random values to be used later.

## Colour can be expressed as a value from 0 to ((16^6)-1).
## 1. Assign a variable to the eye colour and use the random module to get a value between 0 and ((16^6)-1)
## 2. Convert the value to hexadecimal so that it may be used as a colour in drawing operations.
## 3. Convert to a string so that the "0x" can be removed via splitting.
## 4. The Python hexidecimal converter does not return empty digits at the start of the number, but hexidecimal values must have be six digits long to be used as colours.
##    Subtract the length of the string from 6 and repeat "0" by the result.
##         This will fill in any empty digits at the left side of the number to make the hexidecimal value the full six digits long.
## 5. Concatenate the "#" symbol with the number of missing zeroes and the hexidecimal string that resulted from the operations in the first "eyecolour".
## 6. The final result will be a random 6 digit hexidecimal value between 0 and ((16^6)-1) starting with a "#" that can be plugged into turtle methods to display a random colour. 

eyecolour=((str(hex(random.randrange(0,16777215)))[2:]))
eyecolour=("#"+(int(6-(len(eyecolour))))*"0"+(eyecolour))


## 1. To ensure all the colours of the different parts of the shell are different (but not too much), do not reroll colour. Just add 1500 to their decimal value before converting to hexadecimal.
## 2. Convert the decimal values to hexadecimal.
## 3. Do the same things with this value that were done with eye colour.

innershell=((str(hex(rolledshellcolour+1500)))[2:])
topshell=((str(hex(rolledshellcolour+2000)))[2:])
topshell=("#"+int(6-(len(topshell)))*"0"+(topshell))
innershell=("#"+int(6-(len(innershell)))*"0"+(innershell))
shellcolour=('#'+(int(6-len(str(hex(rolledshellcolour))[2:])))*"0"+(str(hex(rolledshellcolour))[2:]))


## Set the turtle speed to 0 to temporarily remove animation and take care of the background.

d.speed(0)
d.left(90)

## 1. Set the both the pen and fill colour to light blue in preparation for the background.
## 2. The line the pen makes is very briefly visible, even when the speed is 0, so the pen will lift before starting the while loop and go down as the loop starts.

d.pen(fillcolor="#aaeaf3", pencolor="#aaeaf3")

d.begin_fill()
d.penup()

## Use a while loop to draw a huge box around the window use a light blue fill so that the background looks like water.
## 1. Assign a variable (background) with a value of 1 and have the while loop add 1 to the variable with every iteration.
##      This creates a running counter that allows the while loop to keep track of itself.
## 2. Have the while loop run until the value of (background) reaches 7
## 3. Use if/else statements to assign different movements to the turtle based on the current iteration of the while loop.
##      During the first 2 loops, the drawing turtle is moving in half-steps, positioning itself to gtfo of the drawing window.
##          The second loop completes the right half of the top of the background square
##      Loops 3-5 are completing the left, right and bottom of the square and need to be twice as big as the first 2 loops.
##      Loop 6 is another "half-step" that completes the last half of the background square left unfinished in the second loop, and loop 7 returns to the initial position.
## Note: This can also be done with a "for" loop, substituting the (background) variable for i and setting the range to 6 and adjusting the values accordingly, but where is the fun in that?

background=1
while background<8:
    if 2<background<6:
        d.forward(2000)
    else:
        d.forward(1000)
        d.pendown()
    d.right(90)
    background=background+1
d.end_fill()

### Moving pen to a better position.

d.penup()
d.left(90)
d.forward(-180)
d.right(90)
d.forward(100)
d.left(130)

## 1. The pen is done being moved, so put the pen down to start the drawing.
## 2. Set the speed back to 10 to show animation.

d.pendown()
d.speed(10)

## Setting pen colour to a dark cyan, fill to turquoise, and pen thickness of 5:
## Used for the outlines of the turtle's tail, flippers, head and outer shell.

d.pen(fillcolor="#4bb089", pencolor="#3fd7e4", pensize=5)

## Directions for the turtle's tail. 

halfcrescent(100, "left", "#4bb089")
d.right(180)
d.end_fill()

## Move the turtle 60 degrees of a clockwise circle that has "steps" of 3 units to begin drawing the left hind flipper.

clockwisecircle(60,3)

## 1. First take the coordinates of the pen before it does anything else.
## 2. Use the placement() function to start the drawing of the left back flipper inside the shell. 
## 3. Draw the first flipper using the back_flipper function.
## 4. Use the values taken at 1. and placement() to get the pen back to where it started. 
## 5. The dimensions of the outer shell have already been determined by the clockwisecircle function that was just used.
##      The clockwisecircle function uses steps and turns to draw a circle.
##      The built in circle function uses radius to calculate size rather than step length.
##      To figure out equivalent dimensions, I must convert from step length to radius, and geometry must be used.
##          There are 3 steps per angle, and there are 360 angles in a full circle, so the circumference of the outer shell is 1080.
##          A circle's circumference is its radius*tau, so its radius must then be its circumference/tau
##      In terms of pi this is r=1080/2pi or 540/pi.
##          This can be plugged into the radius parameter of the built in circle function to recreate an identical circle.
## 6. Use -90 degrees of this circle to move the turtle across the shell to the left front flipper.

d.left(130)
placement(72.18,190, "none")
back_flipper("left", 1)
placement(72.18,198.88, 335)

d.circle(-540/(math.pi), 90)

## Draw and complete the left front flipper using the same methods as the hind flipper.

d.left(120)
placement(120.32,-19.55, "none")
front_flipper("left", 1.2)
placement(155.32,-29.55, 245)
d.circle(-540/(math.pi), 90)


## Drawing the right front flipper.

d.left(90)
placement(-83.11,-92.69, "none")
front_flipper("right", 1.3)
placement(-73.11,-112.69, 155)
d.circle(-540/(math.pi), 70)



## Ditto for the final left flipper.

placement(-160.70,40.07, 120)
back_flipper("right", 1.1)
placement(-166.50,87.58, 75)



##Directions for the outer shell.

d.pen(fillcolor=shellcolour, pensize=10)
d.begin_fill()
d.pen()
d.right(180)
d.circle(540/(math.pi))
d.end_fill()

##Directions for inside shell

d.pen(fillcolor=(innershell), pencolor="#7682ab", pensize=7)
d.begin_fill()
d.penup()
d.left(90)
d.forward(20)
d.right(90)
d.pendown()
d.circle(150,520)
d.end_fill()

## Set the colour for the lines of the shell and reorient for drawing the geometric plates inside it.
d.pen(fillcolor=(topshell), pensize=3)
d.begin_fill()
d.left(90)

## The shell's diameter is 300 units, so the radius would be 150, and half of the radius would be 75.
## The pentagon will start at a quarter of the shell's diameter, and the pentagon's radius would be 75 units.
## Use a random integer between 5 and 10 for the number of sides of the middle plate of the shell.

polyshell(75,(random.randrange(5,10)))
d.end_fill()

## Reset the pen colour, fill and width to be consistent with the rest of the turtle.

d.pen(fillcolor="#4bb089", pencolor="#3fd7e4", pensize=5)

## Moves the pen on the outer shell.

placement(119.46,-84.90, 223)


## Drawing the head.
## 1. The head is an organic shape and must be drawn with curves.
##      No explicit math here, but partial circles of varying lengths are used to simulate curves.

d.begin_fill()
d.left(90)
d.circle(600,15)
clockwisecircle(60,1)
d.forward(20)
clockwisecircle(150,1)
d.forward(80)
d.circle(300,10)
clockwisecircle(10,5)
d.forward(8)
d.end_fill()
d.right(97)
d.circle(540/(math.pi), 20)

## Lift and move pen to prepare to draw eyes.

d.penup()
d.right(90)
d.forward(200)
d.pendown()

# Draw the turtle's left eye

eyes(20)

d.penup()
d.right(-30)
d.forward(75)
d.left(110)
d.pendown()

## Draw the turtle's right eye.
## It will be slightly bigger than the left, as the turtle's head is tilted, and it is closer to the "camera".

eyes(25)
d.left(130)

## Nostrils

d.forward(50)
filledcircle(3,"#095315")
d.left(50)
d.forward(25)
filledcircle(3,"#095315")

## Mouth

d.left(200)
d.forward(45)
d.left(30)
d.pencolor("pink")
d.left(80)
halfcrescent(10, "left", "pink")


## Make bubbles

d.speed(0)

bubbles(10, (random.randrange(10,15)))

## Initial

placement(420, -340, 150)
d.pen(pencolor="#000000", pensize=2)
d.circle(20, 180)
d.penup()
d.left(25)
d. forward(6)
filledcircle(.5,"#000000")
d.forward(15)
d.pendown()
d.left(80)
d.forward(40)
d.forward(-25)
d.right(95)
d.forward(10)
d.left(90)
d.forward(20)
d.forward(-40)
d.right(40)
d.penup()
d.forward(8)
filledcircle(.5,"#000000")
d.forward(90)

## Notes for Future Christine in order of how likely they are to come up again:
## * DO NOT try to copy paste special characters into IDLE or it will shut down without saving.
## * Use exact values for geometry. 3.14 does not cut it for pi, and integer division should not be used to split angles.
## * Return is good for storing random values that you plan on modifying later so they are not rerolled every time they are used.
## * Don't feed Walter more than a half cup of food at one time or he will throw up.



