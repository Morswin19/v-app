<template>
  <div class="outerWrapper">
      <div class="innerWrapper">
          <div class="photo">
              <img :src="photo" alt="">
          </div>
          <div class="description">
              <div class="descriptionData">
                <h2 class="title">autor: <span>{{ author }}</span></h2>
                <p>tags: <span>{{ tags }}</span></p>
                <p>pixabay views: <span>{{ views }}</span></p>
                <p>pixabay downloads: <span>{{ downloads }}</span></p>
                <p>pixabay likes: <span>{{ likes }}</span></p>
              </div>
              <div class="links">
                <div><a :href="hqLink" target="_blank">click to see in HQ</a></div>
                <div><a :href="pixaLink" target="_blank">click to see in Pixabay</a></div>
              </div>
          </div>
      </div>
      <div class="close" @click="$emit('closeModal')" />
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      author: null,
      tags: null,
      views: null,
      downloads: null,
      likes: null,
      hqLink: null,
      pixaLink: null,
    };
  },
  mounted() {
    this.photo = this.item.webformatURL;
    this.author = this.item.user;
    this.tags = this.item.tags;
    this.views = this.item.views;
    this.downloads = this.item.downloads;
    this.likes = this.item.likes;
    this.hqLink = this.item.largeImageURL;
    this.pixaLink = this.item.pageURL;
  },
};
</script>

<style lang="sass" scoped>
  .outerWrapper
      width: 100vw
      height: 100%
      position: fixed
      top: 0
      left: 0
      background-color: #fff
      z-index: 10
      .innerWrapper
          display: flex
          justify-content: center
          align-items: center
          height: 100%
          padding: 25px
          flex-direction: column
          .photo
              max-width: 100%
              height: auto
              img
                  max-width: 100%
                  max-height: 350px
                  height: auto
          .description
              .descriptionData
                  margin-bottom: 20px
                  h2
                      font-weight: 400
                      font-size: 20px
                      margin: 10px
                      span
                          margin-left: 20px
                          font-weight: 800
                          font-size: 24px
                  p
                      font-size: 11px
                      margin: 5px
                      span
                          font-size: 14px
                          margin-left: 20px
              .links
                  display: flex
                  flex-wrap: wrap
                  flex-direction: column
                  margin-bottom: 20px
                  div
                      background-color: black
                      padding: 10px
                      margin-right: 10px
                      margin-bottom: 10px
                      text-align: center
                      a
                          color: white
                          cursor: pointer
                          text-decoration: none
                          margin-right: 10px
      .close
          position: absolute
          padding: 30px
          width: 20px
          height: 20px
          cursor: pointer
          top: 0px
          right: 0px
          &::before,
          &::after
              position: absolute
              top: 30px
              right: 20px
              content: ''
              width: 15px
              height: 2px
              background: black
              display: block
          &::before
              transform: rotate(45deg)
          &::after
              transform: rotate(-45deg)
  @media(min-width: 768px)
    .outerWrapper
      height: 100%
      .innerWrapper
          .photo
              img
                  max-height: 650px

  @media(min-width: 1024px)
    .outerWrapper
      max-width: 70%
      height: 70%
      right: 0
      bottom: 0
      margin: auto
      box-shadow: 15vw 0vh 200px 100px rgba(0,0,0,0.5), -15vw 0vh 200px 100px rgba(0,0,0,0.5),
      .innerWrapper
          height: 100%
          padding: 0px
          flex-direction: row
          .photo
              margin-right: 25px
              max-width: 100%
              height: auto
              img
                  max-width: 100%
                  max-height: 60vh
          .description
              margin-left: 25px
              .descriptionData
                  margin-bottom: 50px
                  h2
                      font-weight: 400
                      font-size: 20px
                      span
                          margin-left: 20px
                          font-weight: 800
                          font-size: 24px
                  p
                      font-size: 12px
                      margin: 15px
                      span
                          font-size: 16px
                          margin-left: 20px
              .links
                  display: flex
                  flex-wrap: wrap
                  div
                      background-color: black
                      padding: 15px
                      margin-right: 10px
                      margin-bottom: 10px
                      a
                          color: white
                          cursor: pointer
                          text-decoration: none
                          margin-right: 10px
</style>
