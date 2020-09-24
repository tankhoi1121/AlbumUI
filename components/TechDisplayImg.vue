<template>
  <main role="main">
    <CategoryBar />
    <div class="bg-light py-5">
      <div class="container">
        <div class="row" ref="LandscapeFrame">{{ LoadingData }}</div>
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
      url: "https://localhost:5001/api/album/tech",
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
    // console.log(imgData);
    return imgData;
  },
  computed: {
    LoadingData: function () {
      setTimeout(() => {
        var _albumFrame = this.$refs.LandscapeFrame;
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
            paragraph.innerText = "Khoi Nguyen Tan";
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