<template>
  <v-card class="pa-4">
		 <v-text-field
      label="Search"
			v-model="keyword"
    ></v-text-field>
		<v-table>
			<template v-slot:default>
				<thead>
					<tr class="text-left">
						<th>
							Video
						</th>
						<th>
							Marker
						</th>
						<th>
							Description
						</th>
						<th>
							Time
						</th>
					</tr>
				</thead>
				<tbody>
					<tr
						v-for="item in data"
						:key="item.title + item.time + item.videoTitle"
						class="text-left"
					>
						<td>{{ item.videoTitle }}</td>
						<td>{{ item.title }}</td>
						<td>{{ item.description }}</td>
						<td>{{ item.time }}</td>
					</tr>
				</tbody>
			</template>
		</v-table>
	</v-card>

</template>

<script>
import { ref, computed } from 'vue'
import Fuse from 'fuse.js'
import { videos } from '../data/videos'
export default {
  name: 'VideoPlayer',
	setup(props) {
		const keyword = ref('')
		const options = {
			findAllMatches: true,
			minMatchCharLength: 3,
			keys: [
				'videoTitle',
				'title',
				'description'
			]
		}
		const flattenVideos = []

		videos.forEach(video => {
			const enrichMarkers = video.markers.map(marker => {
				return {
					...marker,
					videoTitle: video.title,
					url: video.url
				}
			})
			flattenVideos.push(...enrichMarkers)
		})

		const fuseVideos = new Fuse(flattenVideos, options)

		const data = computed(() => {
			return keyword.value ? fuseVideos.search(keyword.value).map(elm => elm.item) : flattenVideos
		})
		return {
			keyword,
			data
		}
	}
}
</script>
