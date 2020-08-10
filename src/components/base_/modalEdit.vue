<template>
  <div class="edit-page">
    <form class="form">
      <div class="form-group">
        <label for="number">Nama Penyewa</label>
        <input
          type="text"
          v-model="form.name"
          name=""
          value=""
          id="number"
          placeholder="Salman"
        />
      </div>
      <div class="form-group">
        <label for="color">No. KTP</label>
        <input
          type="text"
          v-model="form.number"
          number=""
          value=""
          id="color"
          placeholder="102030405060"
        />
      </div>
      <div class="form-group">
        <label for="type">Alamat</label>
        <input
          type="text"
          v-model="form.address"
          address=""
          value=""
          id="type"
          placeholder="Vila Bekasi Indah Blok A No.12 Kota Bekasi"
        />
      </div>
      <div class="form-group">
        <label for="date">No. Telepon</label>
        <input
          type="text"
          v-model="form.telp"
          telp=""
          value=""
          id="date"
          placeholder="082218318835"
        />
      </div>
      <div class="form-group">
        <label for="no">Email</label>
        <input
          type="text"
          v-model="form.email"
          email=""
          value=""
          id="no"
          placeholder="salman@gmail.com"
        />
      </div>
      <div class="button-group">
        <button class="update">UBAH</button>
        <button @click="$emit('close-modal')" class="cancel">BATAL</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "modal-edit"
};
</script>

<style lang="scss" scoped>
.edit-page {
  background: rgba(0, 0, 0, 0.4);
  width: 100vw;
  height: 100vh;
  position: fixed;
  display: flex;
  z-index: 999;
  justify-content: center;
  align-items: center;
  visibility: visible;
  opacity: 0;
  transition: linear 0.3s;
  .form {
    width: 700px;
    height: 450px;
    position: relative;
    background: white;
    display: flex;
    align-items: left;
    flex-direction: column;
    padding: 20px;
    border-radius: 10px;
  }
}

.edit-page-active {
  visibility: visible;
  opacity: 1;
  top: 0;
  left: 0;
}
</style>
