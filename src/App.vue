<template>
  <v-app>
    <v-main>
			<v-container>
				<v-row class="mb-7 text-center">
					<v-col cols="12">
							<h1> Video Maker Demo </h1>
					</v-col>
				</v-row>
    		<v-row class="text-center">
					<v-col md="12" lg="6">
						<VideoPlayer />
					</v-col>
					<v-col md="12" lg="6">
						<VideoList />
					</v-col>
				</v-row>
			</v-container>
    </v-main>
  </v-app>
</template>

<script>
import VideoPlayer from './components/VideoPlayer.vue'
import VideoList from './components/VideoList.vue'

export default {
  name: 'App',

  components: {
    VideoPlayer,
		VideoList
  },

  data: () => ({
    //
  }),
}
</script>
