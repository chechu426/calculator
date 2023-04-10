<template>
  <div>
    <div class="item.container" v-for="user in users" :key="user.id">
      <div>
        <img @click="deleteImage(user.id)" :src=user.thumbnailUrl>
        <h1><a> {{ user.title }} </a></h1>
        <br>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'ListMain',
    data() {
      return {
        users: [],
        cols: 2
      }
    },
    computed: {
      /* columns () {
        let columns = []
        let mid = Math.ceil(this.items.length / this.cols)
        for (let col = 0; col < this.cols; col++) {
          columns.push(this.items.slice(col * mid, col * mid + mid))
        }
        return columns
      } */
    },
    created() {
      // load the users at the beginning
      this.loadJson()
    },
    methods: {
      async loadJson() {
        await fetch('https://jsonplaceholder.typicode.com/photos').then(response => response.json()).then(json => {
          // users is the result of the json needed
          this.users = json
        },(error) => {
          console.log(error);
        })
        this.setName()
      },
      setName () {
        // use just TWO word of the title (to be Name and Surname title)
        for(let i = 0; i < this.users.length; i++) {
          this.users[i].title = this.users[i].title.split(' ').slice(0, 2).join(' ')
        }
      },
      deleteImage (id) {
        // NOT WORKING - this.user is a proxy when it comes from external json and there is no way
        // to manage the items in it (i cannot change proxy to a common array, no information enough founded)
        for(let i = 0; i < this.users.length; i++) {
          if (this.users[i].id === id) {
            this.users.splice[i, 1]
            console.log(this.users)
          }
        }
      }
      // ADDITIONAL COMMENTS:
      // i had no time enough to implement correctly this functions:
      // - responsive and columns - just one column in the center
      // - deleting images - explained at the begginning of the method deleteImage()
      // - autoload - all the images and names are loaded at the beginning

      // i hope you may like the things i have time to do, but i know thats not a complete project
      // thanks for your time
    }
  }
</script>
    
<style>
  .container {
    display: flex;
    border: 1px solid;
  }
  .col {
    margin: 10px;
    border: 1px solid;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
  }
  .item-container {
    border: 1px solid;
    padding: 5px;
    margin: 5px;
  }
  .user {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px;
    grid-auto-rows: minmax(100px, auto);
  }
  img {
    border-radius: 90px;
    border: 2px solid #ffffff;
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
  h1 {
    color: rgb(255, 255, 255);
    font-family: Arial;
    font-size: 12px;
    text-align: center;
    text-transform: uppercase;
  }
</style>
    