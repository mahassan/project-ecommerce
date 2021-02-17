<template>
    <div class="container">
      <div class="row">
        <div class="col-3">
          <input type="text" v-model="search" name="" id="">
          <button @click="searchItem(items)">Search</button>
          <ul v-if="items.length > 0">
            <li v-for="item in items[0]" :key="item.id">
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
     name : "Ammar",
     items :  [],
     search : "",
     searchItems : []
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
  async mounted(){
    try {
      const endpoint = await fetch('https://fakestoreapi.com/products/');
      const result = await endpoint.json();
      this.items.push(result)
    } catch (error) {
      console.log(error)
    }
  }
}
</script>
