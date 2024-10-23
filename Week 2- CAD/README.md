# CAD 

Computer Aided Design (CAD) allows you to create 3D models, and then export files that allow you to create them using various tools- laser cutters, mills and 3D printers.

#### MAKE SURE TO SIGN UP FOR PPMS AND BOOK FDM TRAINING AS SOON AS POSSIBLE!

It's really common for applications to be delayed, sometimes even over a week. Don't leave it until the week before and end up wasting your designs! 

[Trust me, I've seen many an intricate design reduced to hot melt glue and cardboard by a delayed training session. Make sure this is the robot you're shoving off the board, and not the robot you're driving.](https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/blob/main/2-CAD/WhatForgettingPPMSDoesToAMember.md)

---

<a href="./Parts.zip" download>Download link: parts.zip</a>

You can download CAD models of all the components here. To use them, simply open them with Fusion360 and then save each one as a seperate parts.

---

## 1. Save And Import 

https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/b061d83e-8c32-4648-ac98-8f421a394825

One of the most effective methods to create a robot frame is to make models of each component, then position them in your CAD software. This allows for easy construction of structure, using the models to generate interfaces. 

---

## 2. Position Parts 

https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/97bebe43-a9bb-4df8-a728-e79ead1a39a0

Hide parts in order to make sure they don’t get in the way of what you’re working on by clicking the “eye” symbol. The isolate tool, found by right clicking a part, can hide everything except that part too.  

Select the move tool, and make sure to use the “component” mode. The move tool is very versatile, and can position sketch objects, bodies, component and faces. Here, using component mode makes sure that a body is not accidentally disjointed from others in the same component. 

Rotate the breadboard model, and move it out of the way of the battery holder. Likewise, move the TT motors below the battery carrier and give it enough clearance to fit wheels later. When moving the TT motors set pivot can be used to make sure that when the motors rotate, they stay central. 

When setting pivot, clicking on an arc/circle will select its centre. 

Finally, use the move tool to position the MG996R servo motor. Again, setting pivot can be used to keep the motor’s output shaft central. 

---

## 3. Draw Base 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/9bb56ff4-2c6b-4c89-bb6d-672482dcd047


Hide the motors, and look at the bottom of the robot. Use new sketch, and select “capture position”. This creates a sketch where components are visible in the positions you moved them to. The camera will move to be perpendicular to the sketch plane. 

Draw a rectangle. Here, I used a three point rectangle but any type could be used. When drawing the bottom line, a faint blue icon is displayed. This is an inferred constraint- Fusion can see that the line is close to orthogonal, and will lock it as such. Here, this is useful but sometimes it can get in the way. If it’s unwanted, just click the icon after the line is drawn and press delete. 

Make the rectangle roughly the size of the components, but don’t worry about accuracy. Now select the line tool, and switch to construction mode. Construction lines can be used to position sketch objects, but don’t affect anything outside the sketch. Position the end of the line so that a midpoint icon (small triangle) appears. Do the same on the other side, where another midpoint icon appears. There should also be a small square- a perpendicular constraint. 

The rectangle isn’t centred, so we’ll need to manually add a constraint to achieve this. By clicking the origin and the construction line, the coincident constraint can be used to align the centre line of the rectangle and the origin. 

Press D to use the dimension tool. This tool can also be found under the “create” menu. This tool is contextual- clicking two parallel lines will set width, a circle will set radius, two lines will set angle and so on. Use this to set the width and height of the rectangle. Finally select the origin and the bottom of the rectangle, and place a dimension. This will allow you to position the base vertically. 

As you’ve added dimensions and constraints, the lines have become black. This means that they’re fully constrained- some people view this as necessary to avoid unexpected behaviour later on, but it’s not mandatory to create a part. 

---

## 4. Extrude Base 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/4fd70ceb-de2e-4660-b4e9-392c61f11091


One of the most used tools to create a body from a sketch is the extrude tool. Select the base, but leave the bolt holes of the battery carrier unselected. Drag out the arrow to 6mm- Fusion adjusts increments based on zoom, so finer adjustments can be made by zooming in. Alternatively, type 6mm into the “distance” field. 

This part will be laser cut, so it must stay 2D. 

Finally, rotate the camera to ensure that the clearance between the base and the motors is sufficient. 

---

## 5. Draw Motor Mount 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/f1d0d11c-e017-473f-ac39-7609c4828a58


Create a new sketch, this time on the symmetry plane down the middle of the robot. Click the mounting face of the motor, and press P in order to project it onto the sketch plane. As with the base plate, create an L bracket and constrain it to fit the parts. This time, we’ll make use of the colinear constraint, which makes lines lock along the same axis. If a part gets in the way of the sketch, hide it with the browser. You can also make an existing object a construction line by selecting it, then hitting the construction icon. 

---

## 6. Create Motor Mount 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/c70d73ef-863f-414d-8fab-7d79d933d2ac


Now we’ll make a body from the motor mount. However, the projection lines complicate the extrude. Here, it’s easy to fix but in complex models it can be annoying. We’ll go back into the sketch to make these lines construction, so they won’t affect the extrude. 

Select the extrude, and then set “start” to object. Set the motor face to the offset and extrude 5mm.  

In the next step, we’ll be using the join function but the extrude we’re creating will be touching both- if left unchecked, this will fuse our motor mount and baseplate into one body. This can be avoided by setting the baseplate to invisible. 

Extrude again, this time setting “extent” to “to object”. Select the part of the motor mount you just created to link them. 

We’ll now use the mirror tool to create a symmetric part, set to join in order to make a single unit. 

---

## 7. Draw Skid 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/5bcb5695-6661-43e4-8b75-046ab7ce2389


Create a sketch on the baseplate. Draw a circle for the skid, and a plate around it before adding a construction line to distance it from the edge of the base. Add a second circle to work as a mounting hole, with a construction line to position it. Then use the mirror tool to create a second symmetric mounting hole. 

Make sure the construction lines are constrained as vertical or horizontal, and that they are correctly dimensioned. 

---

## 8. Create Skid 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/89dd2e5b-9315-4919-9e1d-19aa06611056


Use an offset again, to draw on the bottom of the base. Set the extrude to “new body” to avoid fusing incorrectly. On the next extrude, we want the pin and plate to fuse but not the base- again, hide the base during this operation. Finally, we’ll use the fillet tool on the bottom of the skid, so that it won’t catch on the floor (as much). 

---

## 9. Servo Tabs 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/4f095c24-293f-4daf-b062-c855b877bcfa



https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/0d398cac-541e-441e-ac93-8eabad2fddcb


Project the relevant parts of the servo, and draw the outline of a mount. Faces, vertices and edges can all be projected by clicking them and pressing P. 

---

## 10. Servo Mount 

https://github.com/user-attachments/assets/c3a3545d-fd50-4642-8372-6946010a16b3

Add some blocks with holes to mount the servo tabs, again centring the bolt holes with construction lines. 

---

## 11. Base Mounts 

https://www.youtube.com/embed/rZymE3rAf0g?si=ihMdaTOgnB4uJXNo

Project and construct mounting holes to attach parts to the base using M3 bolts. 

---

## 12. TimeTravel


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/23be0e64-f3bb-49fc-a562-dd14a9338b7d


Using Time Travel to Unmake Your Mistakes Before They Ever Happen 

This is a somewhat useful trick. 

So far in the design, you’ll see that the servo mount clashes with the motor mount and has put a hole in it. Luckily, I planned this out ahead to demonstrate this feature. Look at my trustworthy, competent prose. You believe me, right? 

Moving swiftly onwards, at the bottom of the Fusion 360 window is a timeline of the actions you’ve performed. The indicator can be rolled back to undo actions, and then rolled back forward to redo them (this might take a minute for complex actions though). 

Go back to before you draw the sketch for the servo tabs, and move the servo forward. It’s very important to move the servo as a component, not a body, and to tick the “capture position” box. 

Sometimes changing a past action can cause issues with future features such as removing a body that is later chamfered, destroying a face later used to create a sketch or killing your parents before you were born. In these cases, affected features in the timeline are highlighted in yellow when affected, or red when critically broken. Right click these features to fix them, for example if we had removed the base we could redefine the mounting holes sketch to be defined by the origin plane- however, in this case the cut/extrude operation on the base would no longer have any purpose becoming red and requiring deletion. 

With any issues fixed, roll the timeline back forwards, and it’s like it never happened. 

What was this section about again? Anyway. 

---

## 13. Tolerances 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/efd23bce-f5c5-4434-a478-e60d8b6f4588


So you’ve printed your part, but it’s not quite right- something doesn’t quite fit, a bolt is too loose or tight etc. While this can be fixed physically with a file or hacksaw or digitally by using the timeline, this can be quite complicated or cause issues in some designs. In these cases, go go gadget press pull. 

The press pull is a contextual tool that can modify tolerances by offsetting faces while preserving features like fillets and chamfers. Here, we’ll use it to adjust the hole sizes on the servo mount to tightly hold an M4 bolt by moving the walls inwards 0.25mm. 

---

## 14. Reinforcement 


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/788a035a-b662-4d9c-8d83-5efcbad6e125



The motor mount is far too weak around the bolts (and in general). We can simply add another extrude to add a little extra material around the holes. 

---

## 15.	How strong are my parts?

### 15A. Not very lol.
  

https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/a82118c4-61df-49d2-8141-a7bff7a15e37


The design has a lot of sharp corners, which concentrate stress. These can combine with layer lines and part defects, causing parts to fail under very little loading. Careful consideration must be taken, especially with FDM 3D printing, to minimize this.

### 15B. But how weak are they?


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/7041bd64-1900-4bfc-b937-22a2c8febaf6


For students, you can use powerful cloud computing to simulate and generatively design components for free. Whilst a lot of this is far out of scope of this session, especially when it comes to calculating dynamic loading and behaviour of non-isometric materials, you can see here how to add loads and constraints to simulate the forces on the motor bracket.

A few ways to easily improve strength:
* Bulk up the part: the most obvious option, most parts here could benefit from just being a bit wider/deeper. Saving 3g of plastic won’t win matches if your wheels are no longer connected to your robot
*	Fillets and chamfers: a gentle curve or small angle doesn’t cause stress to build up as badly as a sharp one, making features much less likely to snap off
*	Better materials: PLA is very brittle. Polymers like nylon, polycarbonate, ABS and enhanced tough PLA are much less likely to snap suddenly

---

## 16. Wheels

https://www.youtube.com/embed/XZ35LbfHFSo?si=jeg3CVB8_ogFqmTk

Create a sketch on the end of the wheel shaft, then project the end of the skid. Draw a construction line past the motor to make sure the wheel and the skid are level. Draw a circle from the centre of the shaft, which should have a snap point, and connect it tangentially to the construction line. Next, create an offset by selecting the flattened parts of the shaft and hitting “O”. This way, we can make sure that the wheels fit snugly but aren’t too small. Extrude a collar along the shaft, then extrude the disk to create the wheel. Finally, we’ll add an offset to the screw hole so that it’s easy to secure the wheel.
Tires
Create a sketch on the face of the wheel, then hit “O” to create an 8mm offset from the rim. Create two radii and link them with an arc. Hit “T” or select the trim tool to cut the radii down. Now select the circular pattern, and create 4 identical features. We’ll next extrude the tire to 6mm, and the features to 4mm with an offset of 2mm. We can then use the combine tool to cut out the tire from the hub, leaving an interlocking interface.
Why create this complex structure? This part can be created in one operation using an S5 or S3 dual nozzle 3D printer using TPU and PLA for the tire and the hub respectively. However, TPU will not bond to PLA so if printed without interlocking geometry the tire will simply slip off.

---

## 17. Fabrication - 3D printing


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/ed551442-318d-47de-8b1e-a04692fe7e87


To use the printers in the makerspace, you’ll need a PPMS account and also an STL of the part.
 Switch to the utilities tab, and select the printer icon in the “make” section. Select the part you want to fabricate, and then hit OK. I have my Fusion linked to a specific slicer, so I have to uncheck a tickbox. You can use 3MF files as well, which carry additional benefits over STLs but may not work on all slicers.
You can also see the process of loading it into Cura and getting it ready to print. When you get your printer training by booking through PPMS, we’ll go over this in greater depth.

### 17A.	Fabrication- Install shaper Utilities
  

https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/8dc738ed-42f9-42fa-b125-5820df0383f7


To use the laser cutter, you’ll need an SVG file. Fusion doesn’t have a great way to export these, and the export SVG plugin is paid for. To get around this, we’ll use a plug in for the Shaper routing tool. 
Under the utilities tab, select the Fusion app store under add ins. Search Shaper Utilities, and download it before running the .msi file. Finally, restart fusion 360.

### 17B.	Fabrication- Laser Cutting (Using Shaper)


https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/assets/20403882/1e5f3faf-af46-41b9-b2a1-b20e8f360e1c


You should now have a triangular icon available under “Make”. Select the face you want to cut, and hit OK to make an SVG. You can view this file by opening it- the laser cutter will cut along the edges seen in the file. Only flat stuff, and no pocketing on the laser cutter. I tried to pocket on a laser cutter once, and the Mechanical Engineers laughed at me.
