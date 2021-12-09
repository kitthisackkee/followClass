<template>
  <div>
      <v-container>
          <h3>ເພີ່ມເອກະສານ</h3>
          <v-text-field label="ຫົວຂໍ້" v-model="frm.title"></v-text-field>
          <v-textarea label="ລາຍລະອຽດ" rows="3" v-model="frm.description"></v-textarea>
          <v-btn @click="$router.back()"  color="error">ຍົກເລີກ</v-btn>
          <v-btn @click.prevent="addDoc()" :loading="loading" color="primary">ບັນທຶກ</v-btn>                   
      </v-container>
  </div>
</template>

<script>
export default {
    data() {
        return {
            loading: false,
            frm: {
                title: "",
                description: "",
            }
        };
    },
    methods: {
        async addDoc(){
            try {
                this.loading = true;
                let rs= await this.$axios.post("doc", {
                    doc: this.frm
                });
                console.log(rs);
                this.$toast.info(rs.data.message);
                this.loading = false;
                this.$router.back();
            } catch (error) {
                this.loading = false;
                this.$toast.error(`${error}`);
            }
        }
    },
};
</script>

<style>

</style>