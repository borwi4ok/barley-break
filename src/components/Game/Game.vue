<template>
	<div class="gameContainer">
		<p v-if="isWin" class="isWinText">
			Congratulations! You resolve this brainteaser
		</p>

			<template v-for="row in numsSequence">
				<div 
						v-for="el in row" 
						:key="el + Math.random()" 
						v-bind:class="[el.isEmpty ? 'empty' : 'num']"
						v-on:click="changePosition">
					<p>{{el.value}}</p>
				</div>
			</template>

			<button v-if="isWin" class="isWinBtn">Shuffle</button>
	</div>
</template>

<script>



export default {
	name:'Game',
	data(){
		return{
			isWin: true,
			numsSequence: [
				[{value:3, isEmpty:false}, {value:2, isEmpty:false}, {value:1, isEmpty:false}],
				[{value:7, isEmpty:false}, {value:4, isEmpty:false}, {value:8, isEmpty:false}],
				[{value:5, isEmpty:false}, {value:6, isEmpty:false}, {value:'', isEmpty:true}]]
		}
	},
	methods:{
		changePosition(event){
			let xClicked, yClicked, 
					xEmpty, yEmpty

			this.numsSequence.map((row, index) => {
				//find x and y of clicked num
				if(row.findIndex(num => num.value == +event.target.outerText) != -1){
					xClicked = index
					yClicked = row.findIndex(num => num.value == +event.target.outerText)
					console.log(xClicked, yClicked)
				}

				//find x and y of empty elem
				if(row.findIndex(num => num.value == '') != -1){
					xEmpty = index
					yEmpty = row.findIndex(num => num.value == '')
					console.log(xEmpty, yEmpty)
				}
			})

			// if clicked num in available row and col
			if(Math.abs(xEmpty - xClicked) < 2 && Math.abs(yEmpty - yClicked) < 2){

				//and it shouldn't be in diagonal cell
				if(Math.abs(xEmpty - xClicked) + Math.abs(yEmpty - yClicked) != 2){
				const clickedCell = this.numsSequence[xClicked][yClicked]
				const emptyCell = this.numsSequence[xEmpty][yEmpty]

				//change empty and clicked cells
				emptyCell.value = clickedCell.value
				emptyCell.isEmpty = false
				
				clickedCell.value = ''
				clickedCell.isEmpty = true
				}

			}
		}
	}
}
</script>

<style>

@import './Game.css'

</style>