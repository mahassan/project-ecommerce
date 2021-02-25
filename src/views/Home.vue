<template>
    <div class="container">
      <div class="row">
        <div class="col-3">
          <input type="text"v-model="searchItems" name="" id="">
          <ul v-if="items.length > 0">
            <li v-for="item in filteredPosts" :key="item.id">
              <img :src="item.image" alt="item.title">
              {{item.title}}
            </li>
          </ul>
        </div>
      </div>
    </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {

  },
 data(){
   return{
     items :  [],
     search : "",
     searchItems : ""
   }
 },
 methods: {
  searchItem(items){
    // we need to look search for items that matches search item
    this.items[0].filter((item) => {
      if(item.title.includes(this.search)){
        this.searchItems.push(item)
      }
    })
  }
 },
computed: {
    filteredPosts(){
    return this.items[0].filter((item) => {
      return item.title.match(this.searchItems)
    })
    }
 },
  created(){
      fetch('https://fakestoreapi.com/products/')
      .then((res)=>{
       return res.json()
      })
      .then((res)=>{
        this.items.push(res)
      })
  }
}
</script>
