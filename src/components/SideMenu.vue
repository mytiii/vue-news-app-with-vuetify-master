<template>
<!--用drawer控制开关-->
  <v-navigation-drawer v-model="drawer" fixed app clipped class="drawer-style"   id="style-1">


    <!--侧边List-->
    <v-list dense class="pt-3  white--text" >

      <v-list-tile
        v-for="source in sources"
        :key="source.id"
        @click="selectSource(source.id)"><!--选定-->
      

        <v-list-tile-action>
          <v-avatar size="32px">
                <img
                  class="img-circle elevation-7 mb-1"
                  :src="getImgUrl(source.id)" />
          </v-avatar>

        </v-list-tile-action>

        <v-list-tile-content>
          <v-list-tile-title>{{ source.name }}</v-list-tile-title>
        </v-list-tile-content>
      </v-list-tile>
    </v-list>

  </v-navigation-drawer>

</template>


<script>

import axios from 'axios'


export default {

   props: {
      api_key: String,
      drawer: Boolean
    },

  data: () => ({
    sources: [],
    errors: []
  }),

  /*生命周期*/
  /*将从api接口get到的sources，*/
  created () {
    axios.get('https://newsapi.org/v2/sources?language=en&apiKey='+this.api_key)
      .then(response => {
        //this.articles = response.data.articles
        this.sources = response.data.sources
        console.log('data:')
        console.log(response.data.sources) // 改变response.data.sources，展示在页面上
      })/*catch下错误*/
      .catch(e => {
        this.errors.push(e)
      })
  },

  /**/
  methods: {
    /*获取图片路径*/
      getImgUrl(pic) {
         return require('../assets/images/'+pic+'.png')
      },
    /*触发器*/
    //实际上就是将source。id完成改变
      selectSource(source){
        this.$emit('selectsource',source)
      }
  }

}
</script>

<!--样式-->
<style scoped>

  #style-1::-webkit-scrollbar {
    width: 6px;
    background-color: #F5F5F5;
  }

  #style-1::-webkit-scrollbar-thumb {
    background-color: #F90;
    background-image: -webkit-linear-gradient(90deg, rgba(255, 255, 255, .2) 25%,
                        transparent 25%,
                        transparent 50%,
                        rgba(255, 255, 255, .2) 50%,
                        rgba(255, 255, 255, .2) 75%,
                        transparent 75%,
                        transparent)
  }

  #style-1::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
    background-color: #F5F5F5;
  }


  .drawer-style {
    background-color: #2196F3 !important;
    border-color: #2196F3 !important;
  }


</style>


