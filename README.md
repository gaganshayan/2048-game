# 2048-game
New Repsitory for the 2048 game, Monday, July 27, 2020

# RULES OF THE GAME 2048
2048 is a game played on a 4x4 grid, with numbered tiles that slide in the direction of the player's choice. As the the tiles slide, they are added to tiles of similar denominations untill the tile numbered 2048 is reached! Everytime a tile is moved, another tile with the value of 2 will randomly appear in an open space. Once added, the tile opposite of the direction the player moved will dissapear and the tile in the direction of the players choice will be changed for one double the value of the two tiles added together.

# How to play

Use the arrow keys on your keyboard to move the tiles up, down, left and right to add the tiles together to make 2048. Goodluck!

# Technology Used

- HTML
- CSS
- JavaScript
- VSCode

# Link to Game

[This is the link to my game](https://gaganshayan.github.io/2048-game/)

# Code Breakdown

I used a function with a nested forloop to create the playing board and generate two 2's on the board to start

```
    function createBoard() {
      for (let i=0; i < width*width; i++) {
        square = document.createElement('div')
        square.innerHTML = 0
        gridDisplay.appendChild(square)
        squares.push(square)
      }
      generate()
      generate()
    }
    createBoard()
```

In order to randomly assign an empty square with a new tile in the denomination of 2, only if there is a 0 ther first. I used a math.random function and have it check to see if the game is over or not.

```
 function generate() {
      randomNumber = Math.floor(Math.random() * squares.length)
      if (squares[randomNumber].innerHTML == 0) {
        squares[randomNumber].innerHTML = 2
        checkForGameOver()
      } else generate()
    }
```

In order to allow the cells to interact with eachother in the game. Here I used forloops to define each row and have them all shift in each direction (up, down, left, right). I used the js method 'parseInt' to convert the strings into integers in the innerHTML to be more recognizable.

```
function moveRight() {
      for (let i=0; i < 16; i++) {
        if (i % 4 === 0) {
          let totalOne = squares[i].innerHTML
          let totalTwo = squares[i+1].innerHTML
          let totalThree = squares[i+2].innerHTML
          let totalFour = squares[i+3].innerHTML
          let row = [parseInt(totalOne), parseInt(totalTwo), parseInt(totalThree), parseInt(totalFour)]
  
          let filteredRow = row.filter(num => num)
          let missing = 4 - filteredRow.length
          let zeros = Array(missing).fill(0)
          let newRow = zeros.concat(filteredRow)
  
          squares[i].innerHTML = newRow[0]
          squares[i +1].innerHTML = newRow[1]
          squares[i +2].innerHTML = newRow[2]
          squares[i +3].innerHTML = newRow[3]
        }
      }
    }
```

I used a function with nested for loops to control the combine function which adds the innerHTML values of each squares and their integer values. 

```
function combineColumn() {
      for (let i =0; i < 12; i++) {
        if (squares[i].innerHTML === squares[i +width].innerHTML) {
          let combinedTotal = parseInt(squares[i].innerHTML) + parseInt(squares[i +width].innerHTML)
          squares[i].innerHTML = combinedTotal
          squares[i +width].innerHTML = 0
          score += combinedTotal
          scoreDisplay.innerHTML = score
        }
      }
      checkForWin()
    }
```

I used a function to assign keycodes to the keys on the keyboard to operate the game.

```
//assign functions to keyCodes
    function control(e) {
      if(e.keyCode === 37) {
        keyLeft()
      } else if (e.keyCode === 38) {
        keyUp()
      } else if (e.keyCode === 39) {
        keyRight()
      } else if (e.keyCode === 40) {
        keyDown()
      }
    }
    document.addEventListener('keyup', control)
```

I used a function to check for the win if the innerHTML of the tile reaches 2048. Once you win, the message 'you win' will be displayed!

```
//check for the winning tile - 2048
    function checkForWin() {
      for (let i=0; i < squares.length; i++) {
        if (squares[i].innerHTML == 2048) {
          resultDisplay.innerHTML = 'You WIN'
          document.removeEventListener('keyup', control)
          setTimeout(() => clear(), 3000)
        }
      }
    }
```

The game is designed to end when there are no more zeros on the grid, the zeros are present on the page, but their fonts are matched in the CSS to hide in plain sight! Once you lose, the message 'you lose' is displayed!

```
    function checkForGameOver() {
      let zeros = 0
      for (let i=0; i < squares.length; i++) {
        if (squares[i].innerHTML == 0) {
          zeros++
        }
      }
      if (zeros === 0) {
        resultDisplay.innerHTML = 'You LOSE'
        document.removeEventListener('keyup', control)
        setTimeout(() => clear(), 3000)
      }
    }
```

Each number set has it's own color and each number is a factor of 2.
```
    function addColors() {
      for (let i=0; i < squares.length; i++) {
        if (squares[i].innerHTML == 0) squares[i].style.backgroundColor = 'black';
        else if (squares[i].innerHTML == 2) squares[i].style.backgroundColor = 'whitesmoke';
        else if (squares[i].innerHTML  == 4) squares[i].style.backgroundColor = 'gray';
        else if (squares[i].innerHTML  == 8) squares[i].style.backgroundColor = 'orange'; 
        else if (squares[i].innerHTML  == 16) squares[i].style.backgroundColor = 'salmon';
        else if (squares[i].innerHTML  == 32) squares[i].style.backgroundColor = 'bisque'; 
        else if (squares[i].innerHTML == 64) squares[i].style.backgroundColor = 'gold'; 
        else if (squares[i].innerHTML == 128) squares[i].style.backgroundColor = 'yellow'; 
        else if (squares[i].innerHTML == 256) squares[i].style.backgroundColor = 'darkolivegreen'; 
        else if (squares[i].innerHTML == 512) squares[i].style.backgroundColor = 'sandybrown'; 
        else if (squares[i].innerHTML == 1024) squares[i].style.backgroundColor = 'goldenrod'; 
        else if (squares[i].innerHTML == 2048) squares[i].style.backgroundColor = 'orangered'; 
      }
  }
  addColors()
  
  var myTimer = setInterval(addColors, 50)
  
  })
```
# Citation

I took guidance from this [YouTube tutorial](https://www.youtube.com/watch?v=aDn2g8XfSMc) and made the following modifications:
