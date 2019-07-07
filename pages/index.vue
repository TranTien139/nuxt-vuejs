<template>
  <div>
    <div v-if="loading==true">
      Loading ...
    </div>
    <div class="wrapper">
      <div class="row">
          <div v-for="joke in jokes" :key="joke.id">
          <div class="col-md-4 cards">
             <img src="https://placeimg.com/300/300/nature" class="img-responsive" alt="Random images placeholder"> 
            <div>
              <h3>{{ joke.id }}</h3>
              <p>{{ joke.joke }}</p>
              <p>{{ joke.category }}</p>
            </div>
          </div>
        </div>
        </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      jokes: [],
      loading: false
    }
  }, 
  created(){
      this.loading = true;
      axios.get("http://api.icndb.com/jokes/random/10")
      .then((response)  =>  {
        this.loading = false;
        this.jokes = response.data.value;
      }, (error)  =>  {
        this.loading = false;
      })
  },
}
</script>