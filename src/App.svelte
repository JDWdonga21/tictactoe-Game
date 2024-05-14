<script lang="ts">
	let board: string[][] = [
	  ['', '', ''],
	  ['', '', ''],
	  ['', '', ''],
	];
	let currentPlayer = 'X';
	let message = 'Player X\'s turn';
  
	function handleClick(row: number, col: number) {
	  if (board[row][col] === '') {
		board[row][col] = currentPlayer;
  
		if (checkWin()) {
		  message = `${currentPlayer} wins!`;
		} else if (checkDraw()) {
		  message = 'It\'s a draw!';
		} else {
		  currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
		  message = `Player ${currentPlayer}'s turn`;
		}
	  }
	}
  
	function checkWin() {
	  // Check rows
	  for (let row of board) {
		if (row.every((cell) => cell === currentPlayer)) {
		  return true;
		}
	  }
  
	  // Check columns
	  for (let col = 0; col < 3; col++) {
		if (board.every((row) => row[col] === currentPlayer)) {
		  return true;
		}
	  }
  
	  // Check diagonals
	  if (
		board[0][0] === currentPlayer &&
		board[1][1] === currentPlayer &&
		board[2][2] === currentPlayer
	  ) {
		return true;
	  }
  
	  if (
		board[0][2] === currentPlayer &&
		board[1][1] === currentPlayer &&
		board[2][0] === currentPlayer
	  ) {
		return true;
	  }
  
	  return false;
	}
  
	function checkDraw() {
	  return board.every((row) => row.every((cell) => cell !== ''));
	}
</script>

<div class="main">
	<h1>{message}</h1>
	<div class="board">
		{#each board as row, i}
		  <div class="boardrow">
			{#each row as cell, j}
				<div class="btns">
					<button class="cell" on:click={() => handleClick(i, j)}>
						{cell}
					</button>
				</div>
			{/each}
		  </div>
		{/each}
	</div>
</div>

<style>
	.main {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	h1 {
		margin-bottom: 20px;
	}

	.board {
		display: flex;
		flex-direction: column;
	}
	.boardrow {
		display: flex;
	}
	.btns {
		
	}
	.cell {
		border: 2px solid black;
		text-align: center;
		font-size: 24px;
		width: 100px;
		height: 100px;
		background-color: #f0f0f0;
		cursor: pointer;
		transition: background-color 0.3s;
	}
	.cell:hover {
		background-color: #ddd;
	}
	.cell:disabled {
		background-color: #bbb;
		cursor: not-allowed;
	}
</style>