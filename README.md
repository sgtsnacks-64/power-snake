<h1># power-snake</h1>

<i>Snake in a Canvas App - Unmanaged Solution provided</i>

![image](https://user-images.githubusercontent.com/96265020/163811054-5838365b-4cd4-40c0-bd9e-0c00777e094a.png)

Before we go any further:
1. Yes, my cat is the main protagonist.
2. No, I cannot change this now.

<h2>How it works:</h2>

<h3>Playboard - Made up of three collections</h3>

  1. Playfield Collection (0 - 99 currently)
  2. Player collection - Each row contains position and index (1, 2, 3 etc)
  3. Fruit collection - Adds fruit to the screen.

Main Gallery (galGameGrid) contains the Playfield collection and fills based on the following formula:

<code>galGameGrid.TemplateFill = If(
    ThisItem.Value in Player.Pos,
    Color.Black,
    If(
        ThisItem.Value in Fruit.Value,
        Color.Red,
        Color.White))</code>

<h3>Moving the player</h3>

Movement is controlled in the OnTimerStart event of tmrGameUpdate:

Player collection is reversed using Sort() function, then each element takes the previous element's .NextMove property, apart from Index1 which takes varMovement variable value. Moves are stacked in colMovement and each turn takes the first element from this collection and sets to varMovement, which is ingested by Player Index 1.

<h3>Out of Bounds/Playfield</h3>

Playfield is 10x10 and Zero-Indexed. So when the player is either on:

0, 10, 20, 30, 40, 50, 60, 70, 80, 90

We can do the following formula:

<code>If(Mod(Index(Player,1).Pos,WrapCount) = 0 && varMovement = -1</code> - This determines if the player is going to move out of the left field. If we divide the position by 10 and get 0, we know we're on the far left of the screen.

Likewise:

<code>If(Mod(Index(Player,1).Pos,WrapCount) = 9 && varMovement = 1</code> - Would prove we're on the right, about to go out of bounds.

To check Top and Bottom, we ensure the next move won't take the player's 1st block either:

+ < 0
+ > 99



