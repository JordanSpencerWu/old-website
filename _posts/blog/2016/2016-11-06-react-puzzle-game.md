---
categories: [blog]
date: 2016-11-06 10:00:00
layout: post
libraries: [react, immutable]
title: "React Puzzle Game"
---

The react Tic-Tac-Toe board game reminded me of a puzzle game that I helped build a few years ago. It was when I enrolled in CS1410 an Introduction to Object Oriented Programming at Salt Lake Community College in summer of 2014. This course is where I learned the programming language Java and the IDE Eclipse. For the final project, I worked in a team of three building a puzzle game in Java. In this blog I will recreate this game in React.

##### Here Are The Rules

1. Whenever you click on a tiles, the four adjacent tiles change color. (Diagonal titles are not considered adjacent)

2. Colors change in this order: BLUE -> BLUE_PURPLE -> BLUE_GREEN -> back to BLUE.

3. When all the tiles are the same color, you win!

4. Try to use as few clicks as possible for the best score.

The original source code for this game can be found <a href="https://github.com/JordanSpencerWu/PuzzleGame" target="_blank">here</a>.

##### Puzzle Game

<div id="root"></div>

##### Code

{% highlight javascript %}
  class Game extends React.Component {
    constructor() {
      super();
      this.state = {
        clickCount: 0,
        isGameOver: false,
        squares: this.newSquareStates(3,3),
        status: 'Currently Playing'
      }
    }

    newSquareStates(numbersOfRows, numbersOfColumns) {
      let squares = new Array(numbersOfRows);
      let color = this.randomColor(COLORS);

      for (let i = 0; i < numbersOfRows; i++) {
        squares[i] = new Array(numbersOfColumns);
        for (let j = 0; j < numbersOfColumns; j++) {
          squares[i][j] = {
              column: j,
                row: i,
                color: color
            };
        }
      }

      for (let i = 0; i < this.randomNumberBetweenTenAndTwenty(); i++) {
        let row = Math.floor(Math.random() * 3);
        let col = Math.floor(Math.random() * 3);
        squares = this.clickSquare(row,col,squares);
      }

      return squares;
    }

    randomColor(colors) {
      let keys = Object.keys(colors);
      let randomIndex = Math.floor(Math.random() * keys.length);
      return colors[keys[randomIndex]];
    }

    randomNumberBetweenTenAndTwenty() {
      return Math.floor(Math.random() * 11) + 10;
    }

    clickSquare(row,col,squares) {
      if (row + 1 < 3) {
        squares[row + 1][col].color = this.nextColor(squares[row + 1][col].color);
      }
      if (row - 1 > -1) {
        squares[row - 1][col].color = this.nextColor(squares[row - 1][col].color);
      }
      if (col + 1 < 3) {
        squares[row][col + 1].color = this.nextColor(squares[row][col + 1].color);
      }
      if (col - 1 > -1) {
        squares[row][col - 1].color = this.nextColor(squares[row][col - 1].color);
      }
      return squares;
    }

    nextColor(currentColor) {
      let nextColor;
      
      switch (currentColor) {
        case COLORS.BLUE_GREEN:
          nextColor = COLORS.BLUE;
          break;
        case COLORS.BLUE:
          nextColor = COLORS.BLUE_PURPLE;
          break;
        default:
          nextColor = COLORS.BLUE_GREEN;
      }

      return nextColor;
    }

    handleClick(row,col) {
      let isGameOver = this.state.isGameOver;
      if (isGameOver) return;

      let squares = window.Immutable.fromJS(this.state.squares).toJS().slice();
      squares = this.clickSquare(row,col,squares);
      let status = this.state.status;

      if (this.checkWinner(squares,squares[row][col].color)) {
        status = 'Congratulations You Won';
        isGameOver = true;
      }

      this.setState({
        squares: squares,
        status: status,
        clickCount: ++this.state.clickCount,
        isGameOver: isGameOver
      });
    }

    checkWinner(squares,color) {
      for (let row = 0; row < squares.length; row++) {
        for (let col = 0; col < squares.length; col++) {
          if (squares[row][col].color !== color)
            return false;
        }
      }
      return true;
    }

    handleNewGame() {
      this.setState({
        clickCount: 0,
        isGameOver: false,
        squares: this.newSquareStates(3,3),
        status: 'Currently Playing'
      });
    }

    render() {
      return (
        <div>
          <div className="game">
            <div className="game-board">
              <Board
                squares={this.state.squares}
                onClick={(row,col) => this.handleClick(row,col)}
              />
            </div>
          </div>
          <div className="game-info">
            <p>{this.state.status}</p>
            <p>{`Clicks: ${this.state.clickCount}`}</p>
            <button className="btn" onClick={() => this.handleNewGame()}>
              { 'New Game' }
            </button>
          </div>
        </div>
      );
    }
  }

  function Board(props) {
    function renderSquare(row,col) {
      return <Square color={props.squares[row][col].color} onClick={() => props.onClick(row,col)} />;
    }

    function renderSquares(row, col) {
      let render = [];
      for (let i = 0; i < row; i++) {
        let cells = [];
        for (let j = 0; j < col; j++) {
          cells.push(renderSquare(i,j));
        }
        render.push(<div key={i} className="board-row">{ cells }</div>);
      }
      return render;
    }

    return (
      <div>
        {renderSquares(3,3)}
      </div>
    )
  }

  function Square(props) {
    let style = {
      backgroundColor: props.color,
      borderColor: '#FFFFFF'
    }

    return (
      <button className="square" style={style} onClick={() => props.onClick()}>
      </button>
    );        
  }

  const COLORS = {
    BLUE_GREEN: '#21B6A8',
    BLUE: '#0000FF',
    BLUE_PURPLE: '#551A8B'
  };

  ReactDOM.render(
    <Game />,
    document.getElementById('root')
  );
{% endhighlight %}

<script type="text/babel">
  $( document ).ready(function(){
    class Game extends React.Component {
      constructor() {
        super();
        this.state = {
          clickCount: 0,
          isGameOver: false,
          squares: this.newSquareStates(3,3),
          status: 'Currently Playing'
        }
      }

      newSquareStates(numbersOfRows, numbersOfColumns) {
        let squares = new Array(numbersOfRows);
        let color = this.randomColor(COLORS);

        for (let i = 0; i < numbersOfRows; i++) {
          squares[i] = new Array(numbersOfColumns);
          for (let j = 0; j < numbersOfColumns; j++) {
            squares[i][j] = {
                column: j,
                  row: i,
                  color: color
              };
          }
        }

        for (let i = 0; i < this.randomNumberBetweenTenAndTwenty(); i++) {
          let row = Math.floor(Math.random() * 3);
          let col = Math.floor(Math.random() * 3);
          squares = this.clickSquare(row,col,squares);
        }

        return squares;
      }

      randomColor(colors) {
        let keys = Object.keys(colors);
        let randomIndex = Math.floor(Math.random() * keys.length);
        return colors[keys[randomIndex]];
      }

      randomNumberBetweenTenAndTwenty() {
        return Math.floor(Math.random() * 11) + 10;
      }

      clickSquare(row,col,squares) {
        if (row + 1 < 3) {
          squares[row + 1][col].color = this.nextColor(squares[row + 1][col].color);
        }
        if (row - 1 > -1) {
          squares[row - 1][col].color = this.nextColor(squares[row - 1][col].color);
        }
        if (col + 1 < 3) {
          squares[row][col + 1].color = this.nextColor(squares[row][col + 1].color);
        }
        if (col - 1 > -1) {
          squares[row][col - 1].color = this.nextColor(squares[row][col - 1].color);
        }
        return squares;
      }

      nextColor(currentColor) {
        let nextColor;
        
        switch (currentColor) {
          case COLORS.BLUE_GREEN:
            nextColor = COLORS.BLUE;
            break;
          case COLORS.BLUE:
            nextColor = COLORS.BLUE_PURPLE;
            break;
          default:
            nextColor = COLORS.BLUE_GREEN;
        }

        return nextColor;
      }

      handleClick(row,col) {
        let isGameOver = this.state.isGameOver;
        if (isGameOver) return;

        let squares = window.Immutable.fromJS(this.state.squares).toJS().slice();
        squares = this.clickSquare(row,col,squares);
        let status = this.state.status;

        if (this.checkWinner(squares,squares[row][col].color)) {
          status = 'Congratulations You Won';
          isGameOver = true;
        }

        this.setState({
          squares: squares,
          status: status,
          clickCount: ++this.state.clickCount,
          isGameOver: isGameOver
        });
      }

      checkWinner(squares,color) {
        for (let row = 0; row < squares.length; row++) {
          for (let col = 0; col < squares.length; col++) {
            if (squares[row][col].color !== color)
              return false;
          }
        }
        return true;
      }

      handleNewGame() {
        this.setState({
          clickCount: 0,
          isGameOver: false,
          squares: this.newSquareStates(3,3),
          status: 'Currently Playing'
        });
      }

      render() {
        return (
          <div>
            <div className="game">
              <div className="game-board">
                <Board
                  squares={this.state.squares}
                  onClick={(row,col) => this.handleClick(row,col)}
                />
              </div>
            </div>
            <div className="game-info">
              <p>{this.state.status}</p>
              <p>{`Clicks: ${this.state.clickCount}`}</p>
              <button className="btn" onClick={() => this.handleNewGame()}>
                { 'New Game' }
              </button>
            </div>
          </div>
        );
      }
    }

    function Board(props) {
      function renderSquare(row,col) {
        return <Square color={props.squares[row][col].color} onClick={() => props.onClick(row,col)} />;
      }

      function renderSquares(row, col) {
        let render = [];
        for (let i = 0; i < row; i++) {
          let cells = [];
          for (let j = 0; j < col; j++) {
            cells.push(renderSquare(i,j));
          }
          render.push(<div key={i} className="board-row">{ cells }</div>);
        }
        return render;
      }

      return (
        <div>
          {renderSquares(3,3)}
        </div>
      )
    }

    function Square(props) {
      let style = {
        backgroundColor: props.color,
        borderColor: '#FFFFFF'
      }

      return (
        <button className="square" style={style} onClick={() => props.onClick()}>
        </button>
      );        
    }

    const COLORS = {
      BLUE_GREEN: '#21B6A8',
      BLUE: '#0000FF',
      BLUE_PURPLE: '#551A8B'
    };

    ReactDOM.render(
      <Game />,
      document.getElementById('root')
    );
  });
</script>