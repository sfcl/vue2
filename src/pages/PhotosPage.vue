<template>
    <v-container>
        <PhotoForm v-if="photos.length < 11" @addPhoto="addPhoto"/>
        <div v-else>Вы не можете добавить фотографии</div>
        <v-row>
            <Photo
                v-for="(photo, index) in $store.getters.getAllPhotos"
                :photo="photo"
                :key="index"
            />
        </v-row>
        <PhotoDialog/>
    </v-container>
</template>

<script>
  import Photo from "@/components/Photo/Photo";
  import PhotoForm from "@/components/Photo/PhotoForm";
  import PhotoDialog from "@/components/Photo/PhotoDialog";
  import {mapActions} from 'vuex'

  export default {
    components: {
      Photo, PhotoForm, PhotoDialog,
    },
    name: "PhotosPage",
    data: () => ({
      photos: [],
      // currentPhoto: {},
      // dialogVisible: false,
    }),
    mounted() {
        //this.fetchTodo()
      this.fetchPhotos()
    },
    methods: {
      ...mapActions(['fetchPhotos']),
      // fetchTodo() {
      //   this.axios.get('https://jsonplaceholder.typicode.com/photos?_limit=10')
      //       .then(response => this.photos = response.data);
      // },
      addPhoto(photo) {
        this.photos.push(photo);
      },
      openPhoto(photo) {
        this.currentPhoto = photo
        this.dialogVisible = true
      },
    }
  }
</script>

<style scoped>

</style>