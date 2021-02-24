<template>
	<div class="gameContainer">
			<template v-for="(row, index) in numsSequence">
				<div 
						v-for="el in row" 
						:key="el" 
						v-bind:class="[el.isEmpty ? 'empty' : 'num']">
					<p>{{show(el.value,index)}}</p>
				</div>
			</template>
	</div>
</template>

<script>



export default {
	name:'Game',
	data(){
		return{
			numsSequence: [
				[{value:1, isEmpty:false}, {value:2, isEmpty:false}, {value:3, isEmpty:false}],
				[{value:4, isEmpty:false}, {value:5, isEmpty:false}, {value:6, isEmpty:false}],
				[{value:7, isEmpty:false}, {value:8, isEmpty:false}, {value:'', isEmpty:true}]]
		}
	},
	methods:{
		show(num){
			return num
		}
	}
}
</script>

<style>

@import './Game.css'

</style>