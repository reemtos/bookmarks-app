<template>
    <div class="container">
        <header class="section section__header">
            <div class="intro-section">
                <div class="logo-holder">
                    <i class="far fa-bookmark icon"></i>
                </div>
                <div class="introduction">
                    <h1 class="intro-phrase">Tosin’s Bookmarks</h1>
                    <!-- <p class="intro-paraphrase">A collection of my favourite and valuable design and development resources as used frequently in my projects.</p> -->
                    <p class="intro-paraphrase">A collection of my favourite design and development resources; because my browser’s bookmarks bar became a mess.</p>
                </div>
            </div>
            <div class="illustration-section">
                <img src="../assets/images/checklist.png" alt="" class="illustration" />
            </div>
        </header>
        <section class="section section__search">
            <div class="search-box">
                <input type="text" v-model="searchQuery" v-on:keyup="filterResources" class="search-field" placeholder="Search from 70 awesome resources.." name="keyword">
                <i class="fas fa-search search-icon"></i>
            </div>
        </section>
        <section class="section section__listing">
            <div class="category" v-for="(category, index) in filteredResourceList" v-bind:key="index">
                <h3 class="category__title">{{category.categoryName}}</h3>
                <div class="category__list">
                    <a v-bind:href="link.url" target="_blank" v-for="(link, index2) in category.links" v-bind:key="index2" class="category__list--link">
                        <div class="category__list--item">
                            <div class="info">
                                <h5 class="title">{{link.title}}</h5>
                                <h6 class="link">{{link.url}}</h6>
                            </div>
                            <div class="icon">
                                <i class="fas fa-external-link-alt icon"></i>
                            </div>
                        </div>
                    </a>
                </div>
            </div>
        </section>
        <footer class="section section__footer">
            <p class="info">Created by <a href="#" class="link" target="_blank">Tosin Orimogunje</a>.</p>
            <p class="info">Illustration from <a href="#" class="link" target="_blank">Undraw</a>.</p>
        </footer>
    </div>
</template>

<script>
import Resources from '../data/data.resources'
export default {
  name: 'Home',
  data () {
    return {
      MyResources: [...Resources],
      searchQuery: ''
    }
  },
  computed: {
    filteredResourceList () {
      if (!this.searchQuery) {
        return this.MyResources
      }
      var searchResult = []
      var lowerCaseQuery = this.searchQuery.toLowerCase()
      this.MyResources.forEach((resource) => {
        var matchTitle = resource.links.some(link => link.title.toLowerCase().includes(lowerCaseQuery))
        if (matchTitle) {
          var filteredResource = {}
          filteredResource.categoryName = resource.categoryName
          filteredResource.links = resource.links.filter(link => link.title.toLowerCase().includes(lowerCaseQuery))
          searchResult.push({...filteredResource})
        }
      })
      return searchResult
    }
  },
  methods: {
    filterResources () {}
  }
}
</script>
