# 1.8 million positions of racing king chess variant.

----------

### Racing kings is a [popular chess variant][2]. 

> Each player has a standard set of pieces without pawns. The opening setup is as below.

![starting position in RC][3]

> In this game, check is entirely forbidden: not only is it forbidden to move ones king into check, but it is also forbidden to check the opponents king.
> The purpose of the game is to be the first player that moves his king to the eight row. When white moves their king to the eight row, and black moves directly after that also their king to the last row, the game is a draw (this rule is to compensate for the advantage of white that they may move first.)
> Apart from the above, pieces move and capture precisely as in normal chess.

To learn a little bit more about a game and to experience the evaluation of the position, you can play a couple of games [here][5]. Do not forget to select Racing kings chess variant and to analyse the game at the end with the machine. Keep in mind that the evaluation score on lichess website is from -10 to 10 and slightly different than in my dataset.

----------

### What you get: 

2 csv files **train.csv** and **validate.csv** with 1.5 mln and ~0.35 mln positions. Both have an identical structure: [FEN][4] of the position and the score.

The score is real value in [-1, 1] range. The closer it is to 1/-1, the more probable is the win of a white/black player. Due to the symmetry I will explain the score only for a white player (for black is the same just with a negative sign.

 - 1 means that white already won (the game is already finished)
 - 0.98 white has a guaranteed(*) win in maximum 1 move
 - 0.96 ... 2 moves
 - 0.94 ... 3 moves
 - ....
 - 0.82 ... in 9 moves
 - 0.80 ... in 10 or more moves 
 - from 0.4 to 0.8 - white has big advantage. For a good player it is not hard to win in such situation
 - from 0.2 to 0.4 - white has some advantage. Might be hard to convert it to a win
 - from 0 to 0.2 - white has tiny advantage
 - 0 means that the position is either a draw or very close to a draw

(*) Guaranteed means that the machine has found a forced sequence of moves that allows white player to win no matter what moves the opponent will make. If the opponent makes the best moves - the game will finish in x moves, but it can finish faster if the black player makes a mistake.

----------

### Your goal is to use predict a score of the position knowin its FEN.

Use train.csv to build your model and evaluate the performance on the validate.csv dataset (without looking/using it). I used [MAE score][6] in my analysis.

### Construction of the dataset

Dataset was constructed by me. I created a bot that plays many games against itself. The bot takes 1 second to analyse the position and selects the move based on the score of position. It took almost a month to generate these positions.

  [1]: https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation
  [2]: https://en.lichess.org/variant/racingKings
  [3]: https://d27t3nufpewl0w.cloudfront.net/lichess/81ac368bd4749c16136f1923065e99a72b3f18a8_initial.png
  [4]: https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation
  [5]: https://en.lichess.org/
  [6]: https://en.wikipedia.org/wiki/Mean_absolute_error
