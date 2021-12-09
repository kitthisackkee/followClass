<template>
  <div>
    <v-container>
      <h3>ແກ້ໄຂເອກະສານ</h3>
      <v-text-field label="ຫົວຂໍ້" v-model="frm.title"></v-text-field>
      <v-textarea
        label="ລາຍລະອຽດ"
        rows="3"
        v-model="frm.description"
      ></v-textarea>
      <v-btn @click="$router.back()" color="error">ຍົກເລີກ</v-btn>
      <v-btn @click.prevent="updateDoc()" :loading="loading" color="primary"
        >ບັນທຶກ</v-btn
      >
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
      },
    };
  },
  mounted() {
    this.getId();
  },
  methods: {
    async getId() {
      try {
        let rs = await this.$axios.get("doc", {
          params: {
            id: this.$route.params.id,
          },
        });
        this.frm = rs.data.doc;
        console.log(rs);
      } catch (error) {}
    },
    async updateDoc() {
      try {
        this.loading = true;
        let rs = await this.$axios.put("doc", {
          doc: {
            title: this.frm.title,
            description: this.frm.description,
          },
          id: this.frm.id
        });
        console.log(rs);
        this.$toast.info(rs.data.message);
        this.loading = false;
        this.$router.back();
      } catch (error) {
        this.loading = false;
        this.$toast.error(`${error}`);
      }
    },
  },
};
</script>

<style>
</style>