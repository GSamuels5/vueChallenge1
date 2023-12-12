<template>
<div id="app">
<!-- Dropdown to select categories -->
<select v-model="selectedCategory">
    <option value="">All Categories</option>
    <!-- loop through unique catergories -->
    <option v-for="category in uniqueCategories" :key="category" :value="category">{{ category }}</option>
</select>
<!-- input field for searching products by name -->
<input type="text" v-model="search" placeholder="Search by name"/>
<!-- Display products based on filters -->
<div v-if="filteredProducts.length > 0">
    <!-- loop through filtered products and display their details -->
<div v-for="product in filteredProducts" :key="product.id">
<img :src="product.image" alt="Product"/>
<p>{{ product.make }}</p>
<p>{{ product.type }}</p>
<p>R{{ product.price }}</p>
<p>{{ product.year }}</p>
</div>
</div>
<div v-else >
    <!-- Show message when no products match the sea -->
    <p v-if="search !== ''">Product not found.</p>
    <!-- Display all products when no search or filter is applied -->
    <div v-else>
        
        <div v-for="product in products" :key="product.id">
            <img :src="product.image" alt="Product" />
        <p>{{ product.make }}</p>
        <p>{{ product.type }}</p>
        <p>R{{ product.price }}</p>
        <p>{{ product.year }}</p>
        </div>
    </div>
</div>
</div>
  
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
        products: [{
                          'id': 1,
                                                'make': 'crown',
                                                'type': 'Antique',
                                                'price': 4396.83,
                                                'year': 1920,
                                                'image': 'https://i.postimg.cc/c1h1LxQ0/Antique-Crown-Watch-Co-pocket-as170a11992b.jpg'
                                
                                            },
                                            {
                                                'id': 2,
                                                'make': 'Seiko prestage',
                                                'type': 'Mens',
                                                'price': 20592,
                                                'year': 1950,
                                                'image': 'https://i.postimg.cc/9f1ngM9x/image.jpg'
                                            },
                                            {
                                                'id': 3,
                                                'make': 'Rolex',
                                                'type': 'Mens',
                                                'price': 15000,
                                                'year': 1963,
                                                'image': 'https://i.postimg.cc/3xZk65xS/Microsoft-Teams-image-10-1000x.jpg'
                                            },
                                            {
                                                'id': 4,
                                                'make': 'kiroh',
                                                'type': 'Womens',
                                                'price': 4500,
                                                'year': 2003,
                                                'image': 'https://i.postimg.cc/htmkPcds/rtz5g-512.webp'
                                            },
                                            {
                                                'id': 5,
                                                'make': 'kiroh',
                                                'type': 'Womens',
                                                'price': 3500,
                                                'year': 2001,
                                                'image': 'https://i.postimg.cc/N0HmzCZ5/71ng-D-Rf8-LL-SX679.jpg'
                                            },
                                        ],
                                       //Selected category from dropdown
                                        selectedCategory: "",
                                        //search input for filtering products by name
                                        search: '',
    };
  },
          computed: {
            //calculate unique categories from products
              uniqueCategories(){
                const categories = new Set();
                this.products.forEach(product => {
                    categories.add(product.type);
           
                });
                           return Array.from(categories);
                           },
                           //filter products based on selected category and search input
                           filteredProducts(){

                               let filtered = this.products;
    
                               if(this.selectedCategory !== ''){

                                   filtered = filtered.filter(product=> product.type === this.selectedCategory);
                               }

                               if (this.search !== ""){
                                  const searchTerm = this.search.toLowerCase()
                                  filtered = filtered.filter(product=> product.make.toLowerCase().includes(searchTerm));
                          }
                        
                          return filtered;
                      }
                          
           
          
          },};
                
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
img{
    height: 400px;
    width: 500px;
}
</style>
