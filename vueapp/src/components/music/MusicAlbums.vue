<template>
    <div class="albums">
        <a-player autoplay :isShow="isShow" :music="song" :list="list" :showLrc="true"></a-player>
    </div>
</template>

<script>
import Axios from "axios";
import VueAplayer from "vue-aplayer";

export default {
  data() {
    return {
      song: {
        title: "我要你",
        author: "老狼",
        src: "http://up.mcyt.net/md5/53/OTkwNzUxMQ_Qq4329912.mp3",
        musicImgSrc:
          "http://omratag7g.bkt.clouddn.com/%E6%88%91%E8%A6%81%E4%BD%A0.jpg",
        lrc: "lrc/我要你.lrc"
      },
      // song:{},
      list: [],
      isShow: false
    };
  },
  components: {
    "a-player": VueAplayer
  },
  mounted() {
    Axios.get("/static/data/musicdata.json")
      .then(res => {
        let list = res.data.musicData;
        this.song = list[1];
        list.forEach(element => {
          this.list.push({
            title: element.title,
            artist: element.author,
            src: element.src,
            pic: element.musicImgSrc,
            lrc: "/static/" + element.lrc
          });
        });
        this.isShow = true;
      })
      .catch();
  }
};
</script>

<style scoped>
.albums {
  margin: 1rem 0;
}
</style>
