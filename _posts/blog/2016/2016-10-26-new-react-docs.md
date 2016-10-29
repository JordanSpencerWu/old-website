---
categories: [blog]
date: 2016-10-26 10:00:00
layout: post
libraries: [react]
title: "New React Docs"
---

React recently improved their website by creating new guides written from scratch using ES6 and CodePen snippets. These improvements will help you understand how to use the React libraries. I went through the documents and tutorial a year ago, everything was written in ES5 and there wasn't as much information. Looking at the new documents, I can say they greatly improved with many examples and detailed walkthroughs. In this blog I will recreate their interactive tic-tac-toe game tutorial.

You can find the tutorial <a href="https://facebook.github.io/react/tutorial/tutorial.html" target="_blank">here</a>.

##### Tic-Tac-Toe Game

<div id="root"></div>

The react team did a great job in making this tutorial! I remember learning React.js a year ago and it took me awhile to learn about lifting states up. We lift states up so only one component stores the states, so there is only one source of truth. This will make it easier to understand how everything works and how we pass props into dumb components. The dumb components are __stateless functional components__! A lot has changed over a year, the most significant changed is ES6 has made using React a lot easier and more readable!

##### BONUS!!

> 1. Display the move locations in the format "(1,3)" instead of "6".

The current board props is a single dimensional array that represents the boxes on the tic tac toe board. In the game of tic tac toe there are only nine boxes, so we can represent all the boxs in a array with nine elements. This means that the first row has the index of [0..2], second row has the index of [3..5], and third row has the index of [7..8]. In the tutorial we are able to use this array to represent the state of the boxes on the board.

Instead of using this representation of the state of the board, we can use a multidimensional array. A multidimensional array will increase readability! Lets figure out how to represent this board as a multidimensional array!

{% highlight javastript %}
  let boardState = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
  ];
{% endhighlight %}

A multidimensional array in JavaScript is an Array object that stores Arrays! What I love about this data type is that they are similar to matrices in math. The first thing we need to do is change the state of the board to a multidimensional array. To do this I created a function that will create a multidimensional array of nulls.

{% highlight javastript %}
  multiDimensionalArrayOfNull(numbersOfRows, numbersOfColumns) {
    let array = new Array(numbersOfRows);

    for (let i = 0; i < numbersOfRows; i++) {
      array[i] = new Array(numbersOfColumns).fill(null);
    }

    return array;
  }
{% endhighlight %}

I decided to add this inside the `Game` class, because it's only used inside this class. Now that we have this function, we can use it to initialize our state inside the constructor.

{% highlight javastript %}
  constructor() {
    super();
    this.state = {
      history: [{
        squares: this.multiDimensionalArrayOfNull(3,3)
      }],
      xIsNext: true,
      stepNumber: 0
    }
  }
{% endhighlight %}

We changed it from a single dimensional array to a multidimensional array, but we are not done yet. Since we changed our representation of the board states, we need to change how we check for winners. Lets refactor our `calculateWinner` function so that it takes a multidimensional array as a parameter.

{% highlight javastript %}
  function calculateWinner(squares) {
    const lines = [
      [[0,0], [0,1], [0,2]],
      [[1,0], [1,1], [1,2]],
      [[2,0], [2,1], [2,2]],
      [[0,0], [1,0], [2,0]],
      [[0,1], [1,1], [2,1]],
      [[0,2], [1,2], [2,2]],
      [[0,0], [1,1], [2,2]],
      [[0,2], [1,1], [2,0]],
    ];

    function valueAt(row, col) {
      return squares[row][col];
    }

    for (let i = 0; i < lines.length; i++) {
      const [a, b, c] = lines[i];
      if (valueAt(a[0],a[1]) && valueAt(a[0],a[1]) === valueAt(b[0],b[1]) && valueAt(a[0],a[1]) === valueAt(c[0],c[1])) {
        return valueAt(a[0],a[1]);
      }
    }
    return null;
  };
{% endhighlight %}

Now `calculateWinner` function works for multidimensional array, note this function is used only for tic tac toe. In tic tac toe there's only eight unique conditions we have to check to see if there's a winner. We have to check for horizontal, vertical, and diagonal conditions.

The last thing we need to do is refactor our callback function for the `onClick` event. To know which box was clicked, we need the following parameters `row` and `column`. We can easily do this by changing the `renderSquare` function inside our `Board` stateless functional component.

{% highlight javastript %}
  function renderSquare(row,col) {
    return <Square value={props.squares[row][col]} onClick={() => props.onClick(row,col)}/>;
  }
{% endhighlight %}

This allows us to click on a box which is represented by a `Square` stateless functional component. This component will delegate the onClick handler to it's parent React component by passing in two arguments `row` and `column`. This allows the `Game` stateful component to handle the changes to the states and has access to information on which box was clicked on.

Refactor the code so that everything works, makes sure that every instance of `squares` is represented by a multidimensional array instead of a single dimensional array inside the `Game` class.

<script type="text/babel">
  $( document ).ready(function() {
    function Square(props) {
      return (
        <button className="square" onClick={() => props.onClick()}>
          {props.value}
        </button>
      );
    }

    function Board(props) {
      function renderSquare(row,col) {
        return <Square value={props.squares[row][col]} onClick={() => props.onClick(row,col)}/>;
      }

      return (
        <div>
          <div className="board-row">
            {renderSquare(0,0)}
            {renderSquare(0,1)}
            {renderSquare(0,2)}
          </div>
          <div className="board-row">
            {renderSquare(1,0)}
            {renderSquare(1,1)}
            {renderSquare(1,2)}
          </div>
          <div className="board-row">
            {renderSquare(2,0)}
            {renderSquare(2,1)}
            {renderSquare(2,2)}
          </div>
        </div>
      );
    }

    class Game extends React.Component {
      constructor() {
        super();
        this.state = {
          history: [{
            squares: this.multiDimensionalArrayOfNull(3,3)
          }],
          xIsNext: true,
          stepNumber: 0
        }
      }

      handleClick(row,col) {
        var history = this.state.history.slice(0, this.state.stepNumber + 1);
        var current = history[history.length - 1];
        const squares = current.squares.slice();
        if (calculateWinner(squares) || squares[row][col]) {
          return;
        }
        squares[row][col] = this.state.xIsNext ? 'X' : 'O';
        this.setState({
          history: history.concat([{
            squares: squares
          }]),
          xIsNext: !this.state.xIsNext,
          stepNumber: history.length
        });
      }

      jumpTo(event,step) {
        event.preventDefault();
        this.setState({
          stepNumber: step,
          xIsNext: (step % 2) ? false : true
        });
      }

      multiDimensionalArrayOfNull(numbersOfRows, numbersOfColumns) {
        let array = new Array(numbersOfRows);

        for (let i = 0; i < numbersOfRows; i++) {
          array[i] = new Array(numbersOfColumns).fill(null);
        }

        return array;
      }

      render() {
        const history = this.state.history;
        const current = history[this.state.stepNumber];
        const winner = calculateWinner(current.squares);

        let status;
        if (winner) {
          status = 'Winner: ' + winner;
        } else {
          status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
        }

        const moves = history.map((step, move) => {
          const desc = move ? 'Move #' + move : 'Game start';
          return (
            <li key={move}>
              <a href="#" onClick={(event) => this.jumpTo(event,move)}>{desc}</a>
            </li>
          );
        });

        return (
          <div>
            <div className="game">
              <div className="game-board">
                <Board 
                  squares={current.squares}
                  onClick={(row,col) => this.handleClick(row,col)}
                />
              </div>
            </div>
            <div className="game-info">
              <p>{status}</p>
              <ol>{moves}</ol>
            </div>
          </div>
        );
      }
    }

    ReactDOM.render(
      <Game />,
      document.getElementById('root')
    );
    
    function calculateWinner(squares) {
      const lines = [
        [[0,0], [0,1], [0,2]],
        [[1,0], [1,1], [1,2]],
        [[2,0], [2,1], [2,2]],
        [[0,0], [1,0], [2,0]],
        [[0,1], [1,1], [2,1]],
        [[0,2], [1,2], [2,2]],
        [[0,0], [1,1], [2,2]],
        [[0,2], [1,1], [2,0]],
      ];

      function valueAt(row, col) {
        return squares[row][col];
      }

      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (valueAt(a[0],a[1]) && valueAt(a[0],a[1]) === valueAt(b[0],b[1]) && valueAt(a[0],a[1]) === valueAt(c[0],c[1])) {
          return valueAt(a[0],a[1]);
        }
      }
      return null;
    };
  });
</script>