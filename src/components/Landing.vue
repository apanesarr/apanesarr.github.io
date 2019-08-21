<template>
<body>
<div class="container">
    <div class="row">
        <div class="column">
            <div class="row">
                <h5>Amandeep <b>Panesar</b></h5>
                
            </div>
            <h6>Software Engineer</h6>
        </div>
    </div>
    <hr>
    <div class="row" style="margin-top: 1rem">
        <b>About Me</b>
    </div>
    <div class="row">
        <p class="article" style="margin-top: 0.1rem; margin-bottom: 1rem">
            Hi, my name is <b>Amandeep</b> and I'm a developer.  I’m interested in machine learning, full stack, and complex problems in general. Currently, I have experience in a variety of languages which you can view by clicking on my resume. I just graduated from McMaster University and on my spare time I love playing basketball, and tinkering with electronics. 
        </p>
    </div>
    <div class="row">
        <p class="col gap-1 xl-row xl-gap-2 article top" style="margin-bottom: 1rem">
            <span><a href="https://github.com/apanesarr">
            <i class="fa fa-github fa-1x"> </i>
                GitHub
            </a></span>
            <span class="xl-only">•</span>
            <span><a href="https://drive.google.com/open?id=1pWDM7Tpu-zXv9FxOERegrIGfdrlaHY3X">
                <i class="fa fa-download fa-1x"> </i>
                Resume
            </a></span>
            <span class="xl-only">•</span>
            <span><a href="https://www.linkedin.com/in/amandeep-s-panesar/">
            <i class="fa fa-linkedin fa-1x"> </i>
                LinkedIn
            </a></span>
            <span class="xl-only">•</span>
            <span><a href="mailto:panesas2@mcmaster.com">
                <i class="fa fa-envelope fa-1x"> </i>
                panesas2@mcmaster.ca</a></span>
        </p>
    </div>
    <hr>
    <div class="row" style="margin-top: 1rem">
        <b>Education</b>

    </div>
    <p class="article" style="margin-top: 0.1rem; margin-bottom: 1rem">
        Just graduated from McMaster University from the <b>Software Engineering (Co-op)</b> program. Although school is formally done I still love to learn and currenly am reading Clean Code by Robert C. Martin.
    </p>
    <hr>
    <div class="row" style="margin-top: 1rem; margin-bottom: 1rem">
        <b>Projects On Github</b>
        
    </div>
    
    <div v-if="loading">Loading...</div>
    <div v-else v-for="item in this.projects" v-bind:key="item.id">
      <p class="article">
      <a :href="'' + item.url + ''"><b>{{item.name}}</b></a>
      <code>{{item.language}}</code>
      <br>
      <span v-if ="item.description">
      {{item.description}}
      </span>
      </p>
    </div>
    <hr style="margin-top: 1rem; margin-bottom: 1rem">
    <div id="root"></div>

</div>
</body>
</template>

<script>
export default {
  name: 'Landing',
  data () {
    return {
      projects: [],
      loading: true
    }
  },

  mounted() {
       this.getgit()
  },
    methods: {
    getgit(){
      this.axios.get('https://api.github.com/users/apanesarr/repos').then((response) => {
        this.projects = response.data.map(proj => {
          return {
            name: proj.name,
            url: proj.html_url,
            language: proj.language,
            description: proj.description,
            update: Date.parse(proj.updated_at)
          }
        })
        this.projects.sort(function(a,b){
          return b.update-a.update
        })
      }).finally(() => this.loading = false)
    }
  },

}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Raleway&display=swap');
  @import '../assets/css/normalize.css';
  @import '../assets/css/skeleton.css';
  @import '../assets/css/devicon.css';
  @import '../assets/css/all.css';
  @import '../assets/lib/fontawesome/css/font-awesome.min.css';
  
</style>
