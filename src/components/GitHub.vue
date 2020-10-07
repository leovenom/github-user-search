<template>
  <div class="hello">
    <img id="logo" src="../assets/logo.png"/>
    <h1>{{ msg }}</h1>
    <form v-on:submit.prevent="queryGitHub(query)">
      <input type="text" placeholder="Github username" v-model="query" />
    </form>
    <div class="results" v-if="results">
      <img v-bind:src="results.avatar_url"/>
      <div class="info">
        <h2>{{ results.name }}</h2>
        <div>{{ results.bio }}</div>
        <div>{{ results.location }}</div>
        <div v-if="results.followers" >Followers: {{ results.followers }}</div>
        <div v-if="results.following" >Following: {{ results.following }}</div>
        <a v-if="results.blog" v-bind:href="results.blog">Go to website</a>
        {{ results.message}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GitHub',
  data () {
    return {
      msg: 'GitHub Search',
      query: '',
      results: null
    }
  },
  methods: {
    queryGitHub(q) {
      let self = this;
      fetch('https://api.github.com/users/' + q)
        .then((j) => {
          return j.json();
        })
        .then((r) => {
          console.log(r);
          self.results = r;
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  font-family: 'Helvetica Neue', Helvetica Arial, Sans-serif;
}
.results {
  margin:30px 150px;
}
.results img {
  float:left;
  border-radius: 50%;
}
.results .info {
 padding-top: 8rem;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: rgba(10, 180, 180, 1);
  text-decoration: none;
}
input{
  margin: 15px 0;
  font-size: 16px;
  padding: 10px;
  width: 250px;
  border: 1px solid rgba(10, 180, 180, 1);
  border-top: none;
  border-left: none;
  border-right: none;
  background: rgba(20, 20, 20, .05);
  color: black;
  outline: none;
  border-radius: 25px;
  text-align: center;
}
@media (max-width: 600px) {
  .results img {
    float:center;
    margin:0px -130px 20px;
    width: 87vw;
  }
  .results .info  {
    display: grid;
    justify-content: center;
     margin:0px -130px 20px;
     padding-top: 0;
  }
}
#logo {
  margin-top:-14px;
  height: 100px;
}
</style>
