<template>
<!--新闻内容部分-->
    <v-layout row wrap align-center>

          <v-flex xs8  offset-md2>
            <div v-for="article in articles" :key="article.title">

              <v-card class="my-3" hover data-aos="zoom-in" data-aos-easing="ease" v-bind:href="article.url">

                <!--img-->
                <v-img
                  height="350px"
                  v-bind:src="article.urlToImage"
                ></v-img>

                  <v-container fill-height fluid>
                    <v-layout>
                      <v-flex xs12 align-end d-flex>
                        <span class="headline">{{ article.title }}</span>
                      </v-flex>
                    </v-layout>
                  </v-container>
                <!--新闻简介-->
                <v-card-text>
                  {{ article.description }}
                </v-card-text>
                <v-card-actions>
                  <!--新闻名-->
                <v-chip small color="secondary" class="white--text">
                  {{article.source.name}}
                </v-chip>
                <!--自动填充-->
                <v-spacer></v-spacer>

                <!--按钮-->
                <v-btn icon class="red--text">
                  <v-icon small>fa-reddit</v-icon>
                </v-btn>
                <v-btn icon class="light-blue--text">
                  <v-icon small>fa-twitter</v-icon>
                </v-btn>
                <v-btn icon class="blue--text text--darken-4">
                  <v-icon small>fa-facebook</v-icon>
                </v-btn>

                <v-btn icon class="red--text">
                  <v-icon small>fa-google-plus</v-icon>
                </v-btn>

                <v-btn icon class="blue--text text--darken-4">
                  <v-icon small>fa-linkedin</v-icon>
                </v-btn>


                <v-spacer></v-spacer>

                <v-btn small replace color="info" v-bind:href="article.url" target="_blank" >Read More</v-btn>
              </v-card-actions>
            </v-card>
            </div>
          </v-flex>

  </v-layout>

</template>


<!--作为部件导出，指明需要articles，api给的是array类型-->
<script>

export default {

  props: {
      articles: Array
  }

}

</script>
