<template>
  <main role="main">
    <!-- <section class="jumbotron text-center">
      <div class="container">
        <h1 class="jumbotron-heading">My Album</h1>
        <p class="lead text-muted">{{message}}</p>
      </div>
    </section>-->
    <CategoryBar />
    <div class="bg-light py-5">
      <div class="container">
        <div class="row" ref="AlbumFrame">{{ LoadingData }}</div>
      </div>
    </div>
  </main>
</template>
<style >
.card-img-top {
  width: 100%;
  border-top-left-radius: calc(0.25rem - 1px);
  border-top-right-radius: calc(0.25rem - 1px);
}
</style>
<script>
import axios from "axios";
var imgData = [];
export default {
  // data() {
  //   return {
  //     message: "Welcome to the world of atractive magic",
  //   };
  // },
  async fetch() {
    let config = {
      method: "GET",
      url: "https://localhost:5001/api/album/",
      headers: {
        "Access-Control-Request-Headers": "*",
      },
    };
    await axios.request(config).then((res) => {
      var prefix = "https://localhost:5001/";
      for (let i = 0; i < res.data.length; i++) {
        res.data[i] = prefix + res.data[i];
      }
      imgData = res.data;
    });
  },
  computed: {
    LoadingData: function () {
      setTimeout(() => {
        var _albumFrame = this.$refs.AlbumFrame;
        if (_albumFrame != null) {
          console.log("Detected Element");
          var data = ["", "", "", "", "", ""];

          imgData.forEach((element) => {
            ///Div col: _albumFrame
            var col = document.createElement("div");
            col.className = "col-md-4";
            _albumFrame.appendChild(col);

            /// Div card: col
            var card = document.createElement("div");
            card.className = "card mb-4 box-shadow";
            col.appendChild(card);

            /// img: card
            var img = document.createElement("img");
            img.className = "card-img-top";
            img.src = element;
            img.style.maxWidth = "100%";
            img.style.maxHeight = "100%";
            card.appendChild(img);

            /// Div cardBody: card
            var cardBody = document.createElement("div");
            cardBody.className = "card-body";
            var paragraph = document.createElement("p");
            paragraph.className = "card-text";
            paragraph.innerText = "unsplash";
            cardBody.appendChild(paragraph);
            card.appendChild(cardBody);
          });
        } else {
          console.log("Fail Detected Element");
        }
      }, 1000);
    },
  },
};
</script>