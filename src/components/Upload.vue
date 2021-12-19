<template>
  <div class="upload">
    <div class="container">
      <div class="large-12 medium-12 small-12 cell">
        <div
          style="text-align: justify"
          class="row"
          v-for="(r, key) in resp"
          :key="key"
        >
          <span>{{ r }}</span>
        </div>
      </div>
      <div class="large-12 medium-12 small-12 cell">
        <label
          >Arquivo
          <input type="file" @change="handleFileUpload($event)" />
        </label>
        <button v-on:click="submitFile()">Enviar</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Upload",
  props: {},
  data() {
    return {
      file: "",
      resp: [],
    };
  },

  methods: {
    submitFile() {
      var t = this;
      let formData = new FormData();

      formData.append("file", this.file);

      axios
        .post("http://localhost:4567/upload_task", formData, {
          headers: {
            "Content-Type": "multipart/form-data",
          },
        })
        .then(function (resp) {
          console.log(resp);
          t.resp = resp.data;
        })
        .catch(function () {
          console.log("FAILURE!!");
        });
    },

    handleFileUpload(event) {
      this.file = event.target.files[0];
    },
  },
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
