---
ID: 134
post_title: Connect 4 Solver
author: jarndt
post_excerpt: ""
layout: post
permalink: >
  https://52projects52weeks.com/2019/01/18/connect-4-solver/
published: true
post_date: 2019-01-18 06:03:49
---
<!-- wp:html -->

<div id="header">
</div>

<div id="connect4">
</div>

<button id="reset" onclick="reset()">reset</button> 
###  {#winner}

<!-- /wp:html -->

<!-- wp:paragraph -->

Above is the connect 4 two player game. It does not have AI incorporated, but the java source code attached does.

<!-- /wp:paragraph -->

<!-- wp:heading -->

## Connect 4 Info

<!-- /wp:heading -->

<!-- wp:paragraph -->

Connect 4 is a solved game and has typically 6x7 rows and columns. Connect 4 is solved meaning that if you play perfectly and go first, you’ll win every time. In connect 4, since you can see every move both you and your opponent can make, it has perfect information. These games can be solved with the typical min max algorithm.   


<!-- /wp:paragraph -->

<!-- wp:heading -->

## Minimax

<!-- /wp:heading -->

<!-- wp:paragraph -->

The min max algorithm works to maximize its move while minimizing its opponent’s move. It will run through every move and every move for that move and so forth. These moves alternate maximizing and minimizing until that particular game is complete. Then it will follow the tree up and find which one is the best, where the best is the one that wins in the fewest moves.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The speed and efficiency of the solver is directly determined by how good the heuristic function is.  The heuristic function simply tells the program how close it is to winning. It needs to be based on the set of 4 spaces that a color could potentially be in.  For instance a high heuristic would be one where 3 of the same color are in a row, with a space at any point in the fourth spot. So, xx x or xxx or x xx ect all would work for a horizontally high heuristic.  However if a y replaced one of those x’s or a y was put in the blank spot then the heuristic value would drop dramatically.  


<!-- /wp:paragraph -->

<!-- wp:heading -->

## Interesting Notes

<!-- /wp:heading -->

<!-- wp:paragraph -->

A depth difference of 2 can cause a second to go to be able to win.  For instance if the first player has a depth of 5 and the second player has a depth of 7 then the second player can win.  Whereas if first has a depth of 6 or 7 or higher then first always wins. This means if you just look 2 more moves into the future than your opponent, then you can win even if you don’t have optimal initial conditions.    


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

It is believed that chess grandmasters typically think 10-15 moves ahead, so with that depth considered, to beat even the best humans at this game, I’d have to set my depth to 17 at least.  However with a depth of 17, the computer would hang while thinking for tens of minutes maybe longer even with more advanced algorithms than minimax like principle variation search.  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

This leads me to the questions, is there a depth where no matter how deeper you look, first place will always win?  The answer is yes, but I don’t know if it’s yes, but only if you have a depth as far as the deepest tree or not.

<!-- /wp:paragraph -->

<!-- wp:heading -->

## Future

<!-- /wp:heading -->

<!-- wp:paragraph -->

There are other algorithms better than minmax, like the alpha beta pruning extension, but for now, minmax is good enough. In the future i'd like to port my code to javascript to be played on the web, as well as have the ability to change ai depth level so you can test different depths yourself. As well as test yourself against different ai depth levels.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

I could see this ai helpful for games at places like Boondocks where you go against an ai who will dish out tickets the more games you win. Simply plug in the opponent's moves and get the ai's output moves and if the depth is high enough, you'll win every time if you go first.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[Github link to code][1]

<!-- /wp:paragraph -->

 [1]: https://github.com/unsupo/connectN