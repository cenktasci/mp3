<template>
  <v-container class="pt-0 mb-8 pb-sm-12">
    <v-row class="text-center">
      <v-col cols="12">

        <!-- Loading progress bar -->
        <loading v-if='!newAlbums'/>

        <!-- Albums -->
        <div v-if="newAlbums" class="headline mx-auto mb-2">New Albums</div>
        <v-row no-gutters v-if="newAlbums">
          <v-col
            v-for="album in newAlbums.albums"
            :key="album.id"
            class="ma-0 py-0 px-0 px-sm-2"
            xs="12"
            sm="6"
            md="4"
            xl="3"
          >
            <AlbumItem
              :id="album.id"
              :ArtistPicUrl="album.artist.picUrl"
              :name="album.name"
              :artistName="album.artist.name"
              :picUrl="album.picUrl"
              :company="album.company"
              :subType="album.subType"
              :type="album.type"
              :size="album.size"
            />
          </v-col>
        </v-row>

      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import loading from '../components/Loading'
import AlbumItem from '../components/Common/AlbumItem'
import { mapGetters } from 'vuex'
// import { httpToHttps } from '../utils/helper'
import { mdiStar, mdiPlayCircleOutline } from '@mdi/js'
export default {
  name: 'PlayListDetails',
  components: {
    loading,
    AlbumItem
  },
  data () {
    return {
      // httpToHttps,
      mdiStar,
      mdiPlayCircleOutline,
      id: ''
    }
  },
  mounted () {
    this.$store.dispatch('album/fetchNewAlbums')
  },
  computed: {
    ...mapGetters({
      newAlbums: 'album/getNewAlbums'
    })
  },
  methods: {

  }
}
</script>
<style lang="scss" scoped>

</style>
