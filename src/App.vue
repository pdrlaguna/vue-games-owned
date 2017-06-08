<template>
<div id="app" class="container">
    <div class="panel-body">
        <table class="table table-striped">
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Publisher</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="game in games">
                    <td>{{game.name}}</td>
                    <td>{{game.publisher}}</td><td><span class="glyphicon glyphicon-trash" aria-hidden="true" v-on:click="removeGame(game)"></span></td>
                </tr>
            </tbody>
        </table>
    </div>
    <div class="panel panel-default">
    <div class="panel-heading">
        <h3 class="panel-title">Add New Games</h3>
    </div>
    <div class="panel-body">
        <form id="form" class="form-inline" v-on:submit.prevent="addGame">
            <div class="form-group">
                <label for="gameName">Name:</label>
                <input type="text" id="gameName" class="form-control" v-model="newGame.name">
            </div>
            <div class="form-group">
                <label for="gamePublisher">publisher:</label>
                <input type="text" id="gamePublisher" class="form-control" v-model="newGame.publisher">
            </div>
            <input type="submit" class="btn btn-primary" value="Add game">
        </form>
    </div>
</div>
</div>

</template>

<script>
import Firebase from 'firebase'

let config = {
    apiKey: "AIzaSyBh0X6x0YDzDgWUvxLMoAG3e3LRmTXs_Ok",
    authDomain: "vue-games-owned.firebaseapp.com",
    databaseURL: "https://vue-games-owned.firebaseio.com",
    projectId: "vue-games-owned",
    storageBucket: "vue-games-owned.appspot.com",
    messagingSenderId: "1033017753125"
  };
  
let app = Firebase.initializeApp(config)
let db = app.database()

let gamesRef = db.ref('games')

export default {
	name: 'app',
	firebase: {
    	games: gamesRef
  	},
  	data () {
	    return {
	      	newGame: {
	          	name: '',
	          	publisher: ''
	      	}
	    }
	},
	methods: {
	      addGame: function () {
	        gamesRef.push(this.newGame);
	        this.newgame.name = '';
	        this.newgame.publisher = ''
	      },
			removeGame: function(game) {
    			gamesRef.child(game['.key']).remove()
			}
	    },

}
</script>

<style>
#app {
	color: #BEBEBE;
}
</style>