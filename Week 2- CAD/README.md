# CAD 

Computer Aided Design (CAD) allows you to create 3D models, and then export files that allow you to create them using various tools- laser cutters, mills and 3D printers.

#### MAKE SURE TO SIGN UP FOR PPMS AND BOOK FDM TRAINING AS SOON AS POSSIBLE!

It's really common for applications to be delayed, sometimes even over a week. Don't leave it until the week before and end up wasting your designs! 

[Trust me, I've seen many an intricate design reduced to hot melt glue and cardboard by a delayed training session. Make sure this is the robot you're shoving off the board, and not the robot you're driving.](https://github.com/UBRoboticsWorkshop/Sumobots/blob/main/Week%202-%20CAD/WhatForgettingPPMSDoesToAMember.md)

---

<a href="./Parts.zip" download>Download link: parts.zip</a>

You can download CAD models of all the components here. To use them, simply open them with Fusion360 and then save each one as a seperate parts.

---

## 1. Save And Import 


https://github.com/user-attachments/assets/639b02d2-5283-46aa-ad57-7f734216328b


One of the most effective methods to create a robot frame is to make models of each component, then position them in your CAD software. This allows for easy construction of structure, using the models to generate interfaces. 

---

## 2. Position Parts 


https://github.com/user-attachments/assets/3b1d4ad5-a41f-42a7-bfa0-d5953052794a


Hide parts in order to make sure they don’t get in the way of what you’re working on by clicking the “eye” symbol. The isolate tool, found by right clicking a part, can hide everything except that part too.  

Select the move tool, and make sure to use the “component” mode. The move tool is very versatile, and can position sketch objects, bodies, component and faces. Here, using component mode makes sure that a body is not accidentally disjointed from others in the same component. 

Rotate the breadboard model, and move it out of the way of the battery holder. Likewise, move the TT motors below the battery carrier and give it enough clearance to fit wheels later. When moving the TT motors set pivot can be used to make sure that when the motors rotate, they stay central. 

When setting pivot, clicking on an arc/circle will select its centre. 

Finally, use the move tool to position the MG996R servo motor. Again, setting pivot can be used to keep the motor’s output shaft central. 

---

## 3. Draw Base 


https://github.com/user-attachments/assets/23fefd9d-9b40-441e-9e7b-ec61fd4506a5


Hide the motors, and look at the bottom of the robot. Use new sketch, and select “capture position”. This creates a sketch where components are visible in the positions you moved them to. The camera will move to be perpendicular to the sketch plane. 

Draw a rectangle. Here, I used a three point rectangle but any type could be used. When drawing the bottom line, a faint blue icon is displayed. This is an inferred constraint- Fusion can see that the line is close to orthogonal, and will lock it as such. Here, this is useful but sometimes it can get in the way. If it’s unwanted, just click the icon after the line is drawn and press delete. 

Make the rectangle roughly the size of the components, but don’t worry about accuracy. Now select the line tool, and switch to construction mode. Construction lines can be used to position sketch objects, but don’t affect anything outside the sketch. Position the end of the line so that a midpoint icon (small triangle) appears. Do the same on the other side, where another midpoint icon appears. There should also be a small square- a perpendicular constraint. 

The rectangle isn’t centred, so we’ll need to manually add a constraint to achieve this. By clicking the origin and the construction line, the coincident constraint can be used to align the centre line of the rectangle and the origin. 

Press D to use the dimension tool. This tool can also be found under the “create” menu. This tool is contextual- clicking two parallel lines will set width, a circle will set radius, two lines will set angle and so on. Use this to set the width and height of the rectangle. Finally select the origin and the bottom of the rectangle, and place a dimension. This will allow you to position the base vertically. 

As you’ve added dimensions and constraints, the lines have become black. This means that they’re fully constrained- some people view this as necessary to avoid unexpected behaviour later on, but it’s not mandatory to create a part. 

---

## 4. Extrude Base 


https://github.com/user-attachments/assets/aec9cec1-18d9-4a66-8277-cfbc73a2986c


One of the most used tools to create a body from a sketch is the extrude tool. Select the base, but leave the bolt holes of the battery carrier unselected. Drag out the arrow to 6mm- Fusion adjusts increments based on zoom, so finer adjustments can be made by zooming in. Alternatively, type 6mm into the “distance” field. 

This part will be laser cut, so it must stay 2D. 

Finally, rotate the camera to ensure that the clearance between the base and the motors is sufficient. 

---

## 5. Draw Motor Mount 


https://github.com/user-attachments/assets/02d344b3-a7bf-45ae-952e-6c2b28ae56a7


Create a new sketch, this time on the symmetry plane down the middle of the robot. Click the mounting face of the motor, and press P in order to project it onto the sketch plane. As with the base plate, create an L bracket and constrain it to fit the parts. This time, we’ll make use of the colinear constraint, which makes lines lock along the same axis. If a part gets in the way of the sketch, hide it with the browser. You can also make an existing object a construction line by selecting it, then hitting the construction icon. 

---

## 6. Create Motor Mount 


https://github.com/user-attachments/assets/949330ef-d430-4ceb-9f19-bdbdcfdaedf4


Now we’ll make a body from the motor mount. However, the projection lines complicate the extrude. Here, it’s easy to fix but in complex models it can be annoying. We’ll go back into the sketch to make these lines construction, so they won’t affect the extrude. 

Select the extrude, and then set “start” to object. Set the motor face to the offset and extrude 5mm.  

In the next step, we’ll be using the join function but the extrude we’re creating will be touching both- if left unchecked, this will fuse our motor mount and baseplate into one body. This can be avoided by setting the baseplate to invisible. 

Extrude again, this time setting “extent” to “to object”. Select the part of the motor mount you just created to link them. 

We’ll now use the mirror tool to create a symmetric part, set to join in order to make a single unit. 

---

## 7. Draw Skid 


https://github.com/user-attachments/assets/7a36d591-be89-4525-9300-86a57ac64530


Create a sketch on the baseplate. Draw a circle for the skid, and a plate around it before adding a construction line to distance it from the edge of the base. Add a second circle to work as a mounting hole, with a construction line to position it. Then use the mirror tool to create a second symmetric mounting hole. 

Make sure the construction lines are constrained as vertical or horizontal, and that they are correctly dimensioned. 

---

## 8. Create Skid 


https://github.com/user-attachments/assets/0dcfb21b-2952-4a39-9129-8597b8d9225e


Use an offset again, to draw on the bottom of the base. Set the extrude to “new body” to avoid fusing incorrectly. On the next extrude, we want the pin and plate to fuse but not the base- again, hide the base during this operation. Finally, we’ll use the fillet tool on the bottom of the skid, so that it won’t catch on the floor (as much). 

---

## 9. Servo Tabs 


https://github.com/user-attachments/assets/d40b921b-1298-4f98-8add-bed2dfb16a0e


https://github.com/user-attachments/assets/c04225de-6162-4b9c-8af1-a8aaaf2137e7


Project the relevant parts of the servo, and draw the outline of a mount. Faces, vertices and edges can all be projected by clicking them and pressing P. 

---

## 10. Servo Mount 


https://github.com/user-attachments/assets/f9f3ec7d-113f-4399-91ac-bbe65dab8c2d


Add some blocks with holes to mount the servo tabs, again centring the bolt holes with construction lines. 

---

## 11. Base Mounts 

https://www.youtube.com/embed/rZymE3rAf0g?si=ihMdaTOgnB4uJXNo

Project and construct mounting holes to attach parts to the base using M3 bolts. 

---

## 12. TimeTravel


https://github.com/user-attachments/assets/5c08a4b6-1fe5-4cc2-8c11-aa181c6386e6


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


https://github.com/user-attachments/assets/a7ab1835-38e9-42d5-9a15-f4f4c6fbe3ae


So you’ve printed your part, but it’s not quite right- something doesn’t quite fit, a bolt is too loose or tight etc. While this can be fixed physically with a file or hacksaw or digitally by using the timeline, this can be quite complicated or cause issues in some designs. In these cases, go go gadget press pull. 

The press pull is a contextual tool that can modify tolerances by offsetting faces while preserving features like fillets and chamfers. Here, we’ll use it to adjust the hole sizes on the servo mount to tightly hold an M4 bolt by moving the walls inwards 0.25mm. 

---

## 14. Reinforcement 


https://github.com/user-attachments/assets/29334cce-5f80-4e3f-8d77-d9a13b7fd026


The motor mount is far too weak around the bolts (and in general). We can simply add another extrude to add a little extra material around the holes. 

---

## 15.	How strong are my parts?

### 15A. Not very lol.


https://github.com/user-attachments/assets/4b7dc0df-5bf5-4b74-bd07-0ea5808da53d


The design has a lot of sharp corners, which concentrate stress. These can combine with layer lines and part defects, causing parts to fail under very little loading. Careful consideration must be taken, especially with FDM 3D printing, to minimize this.

### 15B. But how weak are they?


https://github.com/user-attachments/assets/9724a752-f9d4-416e-8224-46e2aa02d700


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


https://github.com/user-attachments/assets/96ae8f42-ba89-4cf4-971f-56c132441ed4


To use the printers in the makerspace, you’ll need a PPMS account and also an STL of the part.
 Switch to the utilities tab, and select the printer icon in the “make” section. Select the part you want to fabricate, and then hit OK. I have my Fusion linked to a specific slicer, so I have to uncheck a tickbox. You can use 3MF files as well, which carry additional benefits over STLs but may not work on all slicers.
You can also see the process of loading it into Cura and getting it ready to print. When you get your printer training by booking through PPMS, we’ll go over this in greater depth.

### 17A.	Fabrication- Install shaper Utilities


https://github.com/user-attachments/assets/10396867-1b24-453f-8858-340aa456ac66


To use the laser cutter, you’ll need an SVG file. Fusion doesn’t have a great way to export these, and the export SVG plugin is paid for. To get around this, we’ll use a plug in for the Shaper routing tool. 
Under the utilities tab, select the Fusion app store under add ins. Search Shaper Utilities, and download it before running the .msi file. Finally, restart fusion 360.

### 17B.	Fabrication- Laser Cutting (Using Shaper)


https://github.com/user-attachments/assets/bf0e4c1e-d095-4fd5-b159-40f73db0ac7d


You should now have a triangular icon available under “Make”. Select the face you want to cut, and hit OK to make an SVG. You can view this file by opening it- the laser cutter will cut along the edges seen in the file. Only flat stuff, and no pocketing on the laser cutter. I tried to pocket on a laser cutter once, and the Mechanical Engineers laughed at me.
