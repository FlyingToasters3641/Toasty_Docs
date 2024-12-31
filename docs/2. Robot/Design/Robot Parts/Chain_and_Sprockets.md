# Chain and Sprockets
Chain and sprockets are another method of power transmission. They are made of two main components; the sprocket and the chain. The chain is a loop of connected links of metal that engage with the sprockets, which have teeth that go into the gaps of the links. The chain is then able to pull the teeth and spin the sprocket, transferring power to a shaft/mechanism. Anyone who has ever ridden a bike is familiar with chains and sprockets. Chain and sprockets are very similar to belts and pulleys, but chain and sprockets are made out of metal, making them much bulkier, but also way more applicable to high-torque scenarios.

Chain and sprockets, however, must be tensioned, because the metal in the chains will stretch, making the chain longer than desired. This is where an object called a turnbuckle comes in. A turnbackle takes the place of a couple of links, and has a portion that is able to be turned, which will make the turnbuckle smaller, tightening the chain. These may not always be used, because they do not act like a chain, and cannot engage with a sprocket, meaning the chain could not make a complete rotation, as the sprocket would intertfere with the turnbuckle. 

Chain and sprockets are commonly used in applications such as deadaxle pivots(common for arms, as seen in the 2023 FRC game) and OTB, or over the bumper, intake deployment. 

## Chain
The two most common chain types in FRC is #25 chain and #35 chain. This size refers to the pitch - the length of each chain - where #25 chain has a pitch of .25" and #35 has a pitch of .375". The length can vary greatly , as the person making the system is able to customize the number of links on the chain specific to their needs. The only restriction is that there must be a whole number of links on the chain.

Another thing to take into consideration when designing is the chain clearance diameter, or the diameter of the sprocket with the chain wrapped around it, because you may not think about this and then you would have interferences in your design. Below is an image from WCP of the important measures of a sprocket when designing. ![image](https://github.com/user-attachments/assets/fd060f3b-5e99-4922-8760-7ba1cf657b8c)

## Sprockets
Sprockets have bores to transfer power to/from a sprocket. The most common of these are 8mm and Falcon Spline bores for motor pinions, and 1/2 inch hex for shafts. There are also pionions for 3/8 hex but those are less common. There are also larger sprockets called plate sprockets, which generally have a Spline XL bore, that you are able to bolt straight into structure pieces like 2 x 1 Aluminum tubing.

For #25 chain: The motor pinions have either 10 or 12 teeth. 1/2 Hex come with 12, 14, 16, 17, 18, 10, 22, or 24 teeth. Plate sprockets have anywhere from 24 - 84 teeth, increasing in increments of 6 teeth. (24, 30, 36 ... 84) 

For #35 chain :  1/2 Hex hex sprockets can have 9, 12, 15, or 18 teeth. Plate Sprockets have between 18 - 84 teeth, increasing in increments of 6 (18, 24, 30, ... 84)

## Design
Similar to the belts and pulleys, finding the c-c, or center to center distance, between the centers of the sprockets is important to think about when designing a system with chains and sprockets. This will determine where your sprockets will end up, and thus your shafts/pivot points will be. With chain however, you want to avoid half-links, because this will weaken your chain. Simply put, aim to have an EVEN number of chain links.

Too find the c-c of chain systems, you can either use https://www.reca.lc/chains - a chain c-c calculator, or the Origin Cube Featurescript, which allows you to calculate these values in Onshape. While dimensioning, simply type #ChainCTC_(Desired Pitch/Size of Chain)((# of desired links), (# of teeth on your first sprocket), (# of teeth on your second sprocket))

For example, If you want a #25 chain, with sprocket sizes of 18 and 60, and 80 links between them,  type : #ChainCTC_25(80, 18, 60)   This will get you a length of 4.837 inches.

## Resources 
If you want to learn more, you are encouraged to check about https://docs.wcproducts.com/frc-build-system/belts-chain-and-gears/sprockets-and-chain#double-hub-sprockets-product-page and https://www.frcdesign.org/learning-course/stage1/1B/chain/ to learn more about chain and sprocket systems and how to design them. 
