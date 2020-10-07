<template>
  <form method="POST" ref="formImgUpload">
    <div class="form-group d-flex mh-30px">
      <div class="col-md-4"></div>
      <div class="col-md-4">
        <div class="border border-primary w-100 mr-3" ref="showFileName">
          <label for="fileAccess">
            <fa :icon="['fas', 'paperclip']" />
          </label>
        </div>
        <input
          type="file"
          class="invisible"
          ref="fileAccess"
          id="fileAccess"
          name="file"
          @change="ShowFileName()"
        />
      </div>
      <div class="col-md-4"></div>
    </div>
    <div class="form-group d-flex mh-30px">
      <div class="col-md-4"></div>
      <div class="col-md-4">
        <input type="text" name="subDir" id="subDirectory" />
        <p v-if="mimeType" class="text-danger">{{ alert }}</p>
      </div>
      <div class="col-md-4"></div>
    </div>
    <div class="form-group d-flex mh-30px">
      <div class="col-md-4"></div>
      <div class="col-md-4">
        <span class="icon-cloud-position" v-if="loading">
          <fa
            :icon="['fas', 'cloud-upload-alt']"
            class="fa"
            @click="Upload()"
          />
        </span>
      </div>
      <div class="col-md-4"></div>
    </div>
  </form>
</template>
<style>
.mh-30px {
  min-height: 30px;
}
.icon-cloud-position {
  position: relative;
  left: 50%;
}

.fa {
  transform: scale(2, 2);
}
</style>

<script>
export default {
  data() {
    return {
      loading: true,
      mimeType: false,
      alert: "",
    };
  },
  methods: {
    Upload() {
      var form = this.$refs.formImgUpload;
      var fileContainer = this.$refs.fileAccess;
      var mimeTypeThrough = this.CheckMIMEType(
        form["fileAccess"].files.item(0).type
      );
      let formData = new FormData();
      formData.append("file", form["fileAccess"].files.item(0));
      formData.append("subDir", form["subDir"].value);
      let config = {
        header: {
          "content-type": "image/jpeg",
        },
      };
      var res = null;
      if (mimeTypeThrough) {
        do {
          res = this.$axios.$post("/api/album/upload", formData, config);
          console.log(res);
        } while (res == null);
        if (res != null) {
          setTimeout(() => {
            location.reload();
          }, 3000);
        }
      } else {
        this.mimeType = true;
        this.alert = "Format Not Allow";
      }
    },
    ShowFileName() {
      var form = this.$refs.formImgUpload;
      var showFileName = this.$refs.showFileName;
      showFileName.innerHTML = form["fileAccess"].files.item(0).name;
    },
    start() {
      this.loading = true;
    },
    end() {
      this.loading = false;
    },
    CheckMIMEType(mimetype) {
      if (mimetype === "image/jpeg") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>