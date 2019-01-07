---
ID: 39
post_title: Rubik Cube Solver Using Java
author: jarndt
post_excerpt: ""
layout: post
permalink: >
  https://52projects52weeks.com/2019/01/07/rubik-cube-solver-using-java/
published: true
post_date: 2019-01-07 06:47:54
---
<!-- wp:paragraph -->

This concept is one I have been thinking up for a while now, to solve a rubik's cube using a java program.  However this project has been both frustrating, eye-opening and interesting all at the same time, which has opened my eyes to the power of consistency and Test Driven Development (TDD).  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The Rubik's Cube (not Rubix Cube like I previously thought) was developed by Ernő Rubik in 1974.  Rubik was a Hungarian sculptor and professor of architecture and wanted a way to move an entire structure independently without the entire structure falling apart.  He then learned this architecture experiment would make a fun puzzle game, thus he called it the Magic Cube and licensed it to be sold by Ideal Toy Company in 1980. The magic cube was renamed a more iconic brandable name the Rubik Cube in that same year after it’s inventor.  This sparked a worldwide crazy causing it to be considered the world's’ best selling toy. In 2009 an estimated 350 million rubik's cube’s have been sold worldwide. Speedcubing started very early in its history as well as solutions. In fact, the top selling book of 1981 was The Simple Solution to Rubik's Cube by James G. Nourse, selling over 6 million copies.  Not to mention Rubik, the Amazing Cube cartoon show that was developed. But, by the end of 1983 the craze was reported as dead, cubes were still being sold but it would pick back up until the early 2000’s.  This return of the Rubik's cube was given credit to by internet video sites like YouTube. Rubik’s patent expired in 2000 and thus several knockoff brands were created, one of which fetch for 2.5 million dollars which is a fully functional diamond rubik's cube created by Diamond Cutters International.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The Rubik Cube has 43,252,003,274,489,856,000 possible orientations for the cube.  Which if you had one cube for each of the possibilities, you could layer the surface of the earth 275 times with them.  With so many possibilites, there is a good chance that by scrambling your Rubik's cube now, you’re creating a unique scramble that has never existed in the history of the Rubik's cube.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Because of the large number of permutations the Rubik Cube has, it took many years to discover God’s Number or the maximum number of moves to solve any cube configuration.  David Singmaster in 1979 simply counted the maximum number of moves for his algorithm at 277, then soon after another algorithm was found with a maximum of 160 and then soon after that another was found with no more than 94.  The next year Morwen Thistlethwaite in 1980 showed that his algorithm required no more than 85 then he improved it to 80 then to 63 and finally to 52 by 1981. In 2006 this max was lowered to 26 then 27 in 2007 then 22 in 2008 and finally in 2010 God’s number was found to be 20 as shown by supercomputers. Kociemba and Koft then later developed algorithms that are what modern Rubik Cube solvers use today which generate no more than 20 moves for any cube.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

I decided to first learn how to solve the Rubik's cube by hand and then translate it to a java program.  I learned to solve the Rubik's cube using this website <http://www.learnhowtosolvearubikscube.com/how-to-solve-a-rubiks-cube-solution-overview> which I liked because it seemed straight forward and had simple illistrations.  The only issue with this site is the constant pop ups. The hardest part was memorizing the algorithms.  Learning when to apply the algorithm wasn’t all that hard for me as it seemed straightforward and it ended up working out in the end anyways if I messed up.  See below for my simplified steps of the simple solving the cube by hand shown in the link.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

I started out by representing the cube as a 2D array where each face was the first dimension and each cube on that face was the second.  Then to better represent it I developed the print method which printed the cube like this:

<!-- /wp:paragraph -->

<!-- wp:image {"id":42} --><figure class="wp-block-image">

<img src="https://52projects52weeks.com/wp-content/uploads/2019/01/Screen-Shot-2019-01-06-at-11.42.10-PM.png" alt="" class="wp-image-42" /></figure> <!-- /wp:image -->

<!-- wp:paragraph -->

Then I developed each rotation as a swapping of 4 faces and a rotation of one face.  That was manually determined, including reverse rotations.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Then I thought about visualizing it using a 3D library.  I started working with THREE.js and got quite far, but ran into a lot of issues and decided to move back to the numbered approach shown above due to time constraints of wanting to finish the solver.

<!-- /wp:paragraph -->

<!-- wp:image {"id":43,"width":239,"height":243} --><figure class="wp-block-image is-resized">

<img src="https://52projects52weeks.com/wp-content/uploads/2019/01/Screen-Shot-2019-01-02-at-9.51.30-PM.png" alt="" class="wp-image-43" width="239" height="243" /><figcaption>My THREE.js attempt at a rubik's cube</figcaption></figure> <!-- /wp:image -->

<!-- wp:paragraph -->

I started out wanting to use A* to solve the Rubik Cube, but decided to solve it using a more human approach due to curiosity.  Curiosity for how many moves it would take and how difficult it would be to translate human steps to computer steps.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Solving it using human steps would turn out to be a great teacher in what not to do for me.  I know of TDD, but when i’m over enthusiastic or overconfident I elect to skip it and move right into coding.  This would be a huge issue for me as when bugs arose and I went back to fix them I would create bugs in other parts of the code and then have to go back and fix those again over and over again.  This would not have happened with proper TDD. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

I also learned how important consistency is.  In my code I often switch between color and face, color is the 10’s digit shown the 2D cube above and face is color -1.  This was very confusing as I went in to debug the code and couldn’t remember if I was referencing the color or the face in that scenario. Proper code comments and sticking to a consistent scheme would have fixed this issue.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

I did finish the algorithm and it is very fast, solving any cube I give it in just tens of nanoseconds.  However, that is the only compliment I can give it. The solver averages hundreds of moves to solve most cubes with some as few as 60 and some as much as 1200 moves.  Both the 60 and the 1200 are far more than God’s Number of just 20. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

All in all, a thousand lines of code and probably that many strands of hair pulled out resulted in a rather fast but efficient as far as moves go solver.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

From here, in the future i’ll visualize the cube and go back and conquer THREE.js as well as implement a 20 move solver.  Then I can move onto openCV to try and capture the colors of each face using your camera so you won’t have to input them one by one.  Then lastly create a machine which solves the cube.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

If you'd like to view the source code visit: <https://github.com/unsupo/Rubik'sCube>

<!-- /wp:paragraph -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->

<!-- wp:paragraph -->

**Solving the Cube**

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

** **The below is my simplified steps, but if you want pictures then go to the link I posted above.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Solving the cube consists of 9 steps.  Sometimes these steps can be skipped because it just so happens to line up the pieces correctly and if you get better and start to see some simple patterns you can skip the first step.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The first step is solving the white lily, which is surrounding the white centerpiece with yellow edges.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The next step is solving the white cross, which is simply moving the white pieces solved above to the correct places in the opposite face lining up one edge as white and the other edge as the other face color.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The next step is solving the white face.  This is accomplished by finding the corner pieces either on the white face side or the yellow face side with one white and one of the other matching faces in that corner then apply **R’ D’ R D **until the piece is in the correct position

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Then solve the middle section by finding a top edge which shares either the left or right face and the correct face’s colors, then use one algorithm to move it to the left and another to move it to the right.  They are the same just opposites. **U R Ui Ri Ui Fi U F **right and **Ui Li U L U F Ui Fi **left

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Then once all the first two sections are solved then solve the top yellow cross.  This is accomplished by apply this algorithm: **F R U Ri Ui Fi **one two or three times depending on the position of the yellow cubes on top.  A line then once, just line it up so that the line is horizontal. If an L shape then line it up in an upside down L shape and do the algorithm, this needs two, but you might have to flip the cube.  If neither of these two cases then perform the algorithm and you should get one of the other cases and then perform it with that cases specifications.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Now that you have a yellow cross up top and the bottom two sections solved, we need to align the top yellow cross to match the faces.  This is done using this algorithm: **R U Ri U R U U Ri . . **Perform it while looking at a correct face, this rotates the other 3 faces until all 4 are correct.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Now that the yellow cross has all 4 faces correct and the bottom two sections are solved, then you can align the yellow corners up.  Once again this rotates through the other corners, except for the top right one: **U R Ui Li U Ri Ui L **.  Because of this if none are correct, perform it once then flip to a face with a correct top right corner piece and perform it again until all 4 corners are in the correct spot but  not necessarily in the correct position.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The last step is to repeat the **R’ D’ R D **algorithm.  Line up the top right corner and perform this algorithm until the yellow piece is on top, keep in mind this will look like it’s messing up the cube, but in fact it will all fix itself in the end.  Then flip only the top until a corner piece doesn’t have yellow on top and do the algorithm again and repeat. Once the last one has been flipped yellow up, then the whole cube is solved. Just orient the top and bottom to there correct color.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

I then solved a scrambled cube a few times using this method and then deliberately watched the pieces’ position that was in questions to help me memorize the algorithms.  For instance for R’ D’ R D I watched the white piece move around each time I performed this algorithm until it reached its final destination. Then I solved a cube with as many algorithms I could remember up to that point and then looked up the one I had forgotten and repeated until I had all of them memorized.  Then once a day I solved the cube once for 3 days to verify I hadn’t forgotten it over night.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->
