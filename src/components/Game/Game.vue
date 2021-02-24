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
			<button v-if="isWin" class="isWinBtn" v-on:click="shuffle">Shuffle</button>
	</div>
</template>

<script>



export default {
	name:'Game',
	data(){
		return{
			isWin: false,
			isFirstMove: true,
			numsSequence: [
				[{value:3, isEmpty:false}, {value:6, isEmpty:false}, {value:1, isEmpty:false}],
				[{value:8, isEmpty:false}, {value:7, isEmpty:false}, {value:2, isEmpty:false}],
				[{value:5, isEmpty:false}, {value:4, isEmpty:false}, {value:'', isEmpty:true}]]
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

			if(!this.isFirstMove) this.isWinHandler()

			this.isFirstMove = !this.isFirstMove
		},

		isWinHandler(){
			const arrayOfCurrentSequence = []

			this.numsSequence.map(row => row.map(num => arrayOfCurrentSequence.push(num.value)))

			const rightSequence = new Array(arrayOfCurrentSequence.filter(val => val != '').sort((a, b) => a - b))

			if(arrayOfCurrentSequence.filter(val => val != '').join() == rightSequence.join()){
				this.isWin = true
			}
		},

		shuffle(){
			let arr = [1, 2, 3, 4, 5, 6, 7, 8],
					shuffledSequence = []
			
			for(let i = 0; i < arr.length + 1; i++){
				const randomIndex = Math.floor(Math.random() * arr.length)

				shuffledSequence.push(arr[randomIndex])

				arr.splice(randomIndex, 1)

				i = 0
			}

		let iter = 0

		this.numsSequence.map((row) => row.map((num) => {
			if(num.value != ''){
				num.value = shuffledSequence[iter]
				num.isEmpty = false
				iter++
			}
		}))

		this.isWin = false
		}
	}
}
</script>

<style>

@import './Game.css'

</style>