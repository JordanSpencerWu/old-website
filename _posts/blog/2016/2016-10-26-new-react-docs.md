---
categories: [blog]
date: 2016-10-26 10:00:00
layout: post
libraries: [react, immutable]
title: "New React Docs"
---

React recently improved their website by creating new guides written from scratch using ES6 and CodePen snippets. These improvements will help you understand how to use the React libraries. I went through the documents and tutorial a year ago, everything was written in ES5 and there wasn't as much information. Looking at the new documents, I can say they greatly improved with many examples and detailed walkthroughs. In this blog I will recreate their interactive tic-tac-toe game tutorial.

You can find the tutorial <a href="https://facebook.github.io/react/tutorial/tutorial.html" target="_blank">here</a>.

##### Tic-Tac-Toe Game

<div id="root"></div>

The react team did a great job in making this tutorial! I remember learning React.js a year ago and it took me awhile to learn about lifting states up. We lift states up so only one component stores the states, so there is only one source of truth. This will make it easier to understand how everything works and how we pass props into dumb components. The dumb components are __stateless functional components__! A lot has changed over a year, the most significant changed is ES6 has made using React a lot easier and more readable!

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
        return <Square value={props.squares[row][col].value} onClick={() => props.onClick(row,col)}/>;
      }

      function renderSquares (row, col) {
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
      );
    }

    class Game extends React.Component {
      constructor() {
        super();
        this.state = {
          history: [{
            squares: this.createSquares(3,3),
            movedLocation: null,
            player: null,
            isGameOver: false
          }],
          xIsNext: true,
          stepNumber: 0,
          isAscend: true
        }
      }

      handleClick(row,col) {
        let history = window.Immutable.fromJS(this.state.history).toJS().slice(0, this.state.stepNumber + 1);
        let current = history[history.length - 1];
        let isGameOver = current.isGameOver;
        const squares = window.Immutable.fromJS(current.squares).toJS();

        if (squares[row][col].value || isGameOver) {
          return;
        }

        squares[row][col].value = this.state.xIsNext ? 'X' : 'O';
        const winningSquares = calculateWinner(squares);
        let location = `(${row},${col})`;

        if (winningSquares) {
          for (let i = 0; i < winningSquares.length; i++) {
            squares[winningSquares[i][0]][winningSquares[i][1]].winner = true;
          }
          isGameOver = true;
        }
        this.setState({
          history: history.concat([{
            squares: squares,
            movedLocation: location,
            player: this.state.xIsNext ? 'X' : 'O',
            isGameOver: isGameOver
          }]),
          xIsNext: !this.state.xIsNext,
          stepNumber: history.length
        });
      }

      jumpTo(event,step) {
        event.preventDefault();
        this.setState({
          stepNumber: step,
          xIsNext: (step % 2) ? false : true,
        });
      }

      createSquares(numbersOfRows, numbersOfColumns) {
        let array = new Array(numbersOfRows);

        for (let i = 0; i < numbersOfRows; i++) {
          array[i] = new Array(numbersOfColumns);
          for (let j = 0; j < numbersOfColumns; j++) {
            array[i][j] = {
                column: j,
                  row: i,
                  value: null,
                  winner: false
              };
          }
        }

        return array;
      };

      handleToggle() {
        this.setState({
          isAscend: !this.state.isAscend
        });
      }

      render() {
        const history = this.state.history;
        const current = history[this.state.stepNumber];
        const winningSquares = calculateWinner(current.squares);
        const winner = this.state.xIsNext ? 'O' : 'X';

        let status;
        if (winningSquares) {
          status = 'Winner: ' + winner;
        } else {
          status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
        }

        const moves = history.map((step, move) => {
          const text = move ? `Player ${step.player} moved to ${step.movedLocation}` : 'Game start';
          let link = null;
          
          if (move === this.state.stepNumber) {
            link = <p>{text}</p>;
          } else {
            link = <a href="#" onClick={(event) => this.jumpTo(event,move)}>{text}</a>
          }
          return (
            <li key={move}>
              {link}
            </li>
          );
        }, this);

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
              <button className="btn" onClick={() => this.handleToggle()}>
                { this.state.isAscend ? 'ASCEND' : 'DESCEND' }
              </button>
              <p>{status}</p>
              <ol>{ this.state.isAscend ? moves : moves.reverse() }</ol>
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
        return squares[row][col].value;
      }

      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (valueAt(a[0],a[1]) && valueAt(a[0],a[1]) === valueAt(b[0],b[1]) && valueAt(a[0],a[1]) === valueAt(c[0],c[1])) {
          return lines[i];
        }
      }
      return null;
    };
  });
</script>