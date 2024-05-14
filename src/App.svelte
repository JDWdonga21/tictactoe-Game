<script lang="ts">
	let board: string[][] = [
	  ['', '', ''],
	  ['', '', ''],
	  ['', '', ''],
	];
	let currentPlayer = 'X';
  
	function handleClick(row: number, col: number) {
	  if (board[row][col] === '') {
		board[row][col] = currentPlayer;
  
		if (checkWin()) {
		  alert(`${currentPlayer} wins!`);
		} else if (checkDraw()) {
		  alert('It\'s a draw!');
		} else {
		  currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
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
		
	}

	.board {
		display: flex;
		flex-direction: column;
		/* grid-template-columns: repeat(3, 1fr); */
		/* gap: 10px; */
	}
	.boardrow {
		margin: 0;
		display: flex;
		flex-direction: row;
		width: 300px;
	}
	.btns {
		margin: 10px;
		width: 30px;
		height: 30px;
	}
	.cell {
	  border: 1px solid black;
	  text-align: center;
	  font-size: 24px;
	}
</style>