<template>
  <div class="hello">
    <h1>{{ msg }} {{v}}</h1>
    <h3>Download</h3>
    <a href="https://dl.moro.mama.sh/download">
      <img alt="Download" height="80" src="../assets/dl.png" />
    </a>
      <h3>Release noter til version {{ v }}:</h3>
    <p>
      {{ message }}
    </p>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="#">About</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      v: "",
      message: ""
    };
  },
  props: {
    msg: String,
  },
  methods: {
    getLatest: function () {
      fetch("https://dl.moro.mama.sh/version", {
        method: "GET",
        headers: { Accept: "application/json" },
      })
        .then((r) => r.json())
        .then(
          function (x) {
            this.v = x.Version
            this.message = x.Message
          }.bind(this)
        )
    },
  },
  beforeMount(){
    this.getLatest()
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
  color: #42b983;
}
</style>
