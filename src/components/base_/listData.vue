<template>
  <div class="rent-page">
    <section class="title">
      <h1>Data Penyewa</h1>
    </section>
    <div class="form-edit" v-show="updateSubmit">
      <p>Ubah Data Penyewa</p>
      <form class="form">
        <div class="form-group">
          <input type="hidden" v-model="form.id" />
        </div>
        <div class="form-group">
          <input
            type="text"
            v-model="form.name"
            id="name"
            placeholder="Salman"
          />
        </div>
        <div class="form-group">
          <input
            type="text"
            v-model="form.card_id"
            id="card"
            placeholder="102030405060"
          />
        </div>
        <div class="form-group">
          <input
            type="text"
            v-model="form.address"
            id="address"
            placeholder="Vila Bekasi Indah Blok A No.12 Kota Bekasi"
          />
        </div>
        <div class="form-group">
          <input
            type="text"
            v-model="form.phone"
            id="number"
            placeholder="082218318835"
          />
        </div>
        <div class="button-group">
          <button @click="update(form)" class="update">SIMPAN</button>
          <button @click="cancel" class="exit">BATAL</button>
        </div>
      </form>
    </div>
    <div class="data-renter" v-bind:class="{ addexpand: expanding }">
      <section class="renter">
        <div class="reg">
          <input
            type="text"
            class="search"
            v-model="search"
            placeholder="Cari Berdasarkan Nama..."
          />
          <div class="blue"><i class="fas fa-search"></i></div>
        </div>
        <section class="list-renter" v-for="renter in renters" :key="renter.id">
          <div class="image">
            <img src="../../assets/img/profile.png" />
          </div>
          <div class="info">
            <p>Nama: {{ renter.name }}</p>
            <p>No. KTP: {{ renter.card_id }}</p>
            <p>Alamat: {{ renter.address }}</p>
            <p>No. Telepon: {{ renter.phone }}</p>
          </div>
          <div class="button-group">
            <button @click="edit(renter)" class="edit">UBAH</button>
            <button @click="del(renter)" class="delete">HAPUS</button>
          </div>
          <!-- <div v-show="deleteSubmit" class="delete-pop">
            <section class="confirm-delete">
              <p>Yakin ingin dihapus?</p>
              <button class="delete" @click="del(renter)">HAPUS</button>
              <button class="exit" @click="exit()">BATAL</button>
            </section>
          </div> -->
        </section>
      </section>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "list-data",
  props: ["expanding"],
  data() {
    return {
      form: {
        id: "",
        card_id: "",
        name: "",
        address: "",
        phone: ""
      },
      renters: [],
      search: "",
      updateSubmit: false,
      deleteSubmit: false
    };
  },
  mounted() {
    this.load();
  },
  computed: {
    filteredRenter() {
      return this.renters.filter(renter => {
        return renter.name.match(this.search);
      });
    }
  },
  methods: {
    load() {
      axios
        .get("https://www.penyewaankapal.attayasagroup.co.id/public/api/renter")
        .then(res => {
          this.renters = res.data;
          console.log("data: ", res.data);
        })
        .catch(err => {
          console.log("error: ", err);
        });
    },
    cancel() {
      this.updateSubmit = false;
    },
    edit(renter) {
      this.updateSubmit = true;
      this.form.id = renter.id;
      this.form.name = renter.name;
      this.form.phone = renter.phone;
      this.form.card_id = renter.card_id;
      this.form.address = renter.address;
    },
    update(form) {
      return (
        axios
          .put(
            "https://www.penyewaankapal.attayasagroup.co.id/public/api/renter/" +
              form.id,
            {
              name: this.form.name,
              phone: this.form.phone,
              address: this.form.address,
              card_id: this.form.card_id
            }
          )
          // eslint-disable-next-line no-unused-vars
          .then(res => {
            this.load();
            this.form.id = "";
            this.form.name = "";
            this.form.phone = "";
            this.form.card_id = "";
            this.form.address = "";
            this.updateSubmit = false;
          })
          .catch(err => {
            console.log(err);
          })
      );
    },
    confirm() {
      this.deleteSubmit = true;
    },
    exit() {
      this.deleteSubmit = false;
    },
    del(renter) {
      axios
        .delete(
          "https://www.penyewaankapal.attayasagroup.co.id/public/api/renter/" +
            renter.id
        )
        // eslint-disable-next-line no-unused-vars
        .then(res => {
          this.load();
          this.deleteSubmit = false;
          // eslint-disable-next-line no-undef
          let index = this.users.indexOf(form.name);
          this.users.splice(index, 1);
          alert("Data telah dihapus...");
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.form-edit {
  background-color: #4a4a4a;
  width: 50vw;
  height: 50vh;
  position: fixed;
  display: flex;
  flex-direction: column;
  z-index: 999;
  margin: 70px 0 0 230px;
  border-radius: 10px;
  p {
    margin: 15px 0 0 25px;
    color: #ffffff;
  }
  .form {
    position: relative;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    width: 80%;
    border: #c7c2c2 1px solid;
    border-radius: 10px;
    background-color: #ffffff;
    padding: 10px;
    box-sizing: border-box;
    margin: 15px 0 0 60px;
    .form-group {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      input {
        border: 1px solid #c7c2c2;
        border-radius: 5px;
        width: 470px;
        height: 30px;
        margin: 5px 0;
        padding-left: 10px;
      }
    }
    .button-group {
      display: flex;
      .exit {
        border: 1px solid rgba(247, 10, 10, 0.842);
        color: rgba(247, 10, 10, 0.842);
        background: #ffffff;
        padding: 10px 20px;
        border-radius: 5px;
        margin-left: 10px;
        cursor: pointer;
      }
      .update {
        border: none;
        color: #ffffff;
        background: #0066ff;
        padding: 10px 20px;
        border-radius: 5px;
        cursor: pointer;
      }
    }
  }
}

// .delete-pop {
//   background-color: #4a4a4a;
//   width: 50vw;
//   height: 50vh;
//   position: fixed;
//   display: flex;
//   justify-content: center;
//   align-items: center;
//   flex-direction: column;
//   z-index: 999;
//   margin: 70px 0 0 230px;
//   border-radius: 10px;
//   .confirm-delete {
//     position: fixed;
//     z-index: 999;
//     display: flex;
//     flex-direction: column;
//     justify-content: center;
//     flex-wrap: wrap;
//     width: 40%;
//     border: #c7c2c2 1px solid;
//     border-radius: 10px;
//     background-color: #ffffff;
//     padding: 10px;
//     box-sizing: border-box;
//     p {
//       margin-bottom: 10px;
//     }
//     .exit {
//       border: 1px solid rgba(247, 10, 10, 0.842);
//       color: rgba(247, 10, 10, 0.842);
//       background: #ffffff;
//       padding: 10px 20px;
//       border-radius: 5px;
//       cursor: pointer;
//     }
//     .delete {
//       border: none;
//       color: #ffffff;
//       background: #0066ff;
//       padding: 10px 20px;
//       border-radius: 5px;
//       margin-bottom: 10px;
//       cursor: pointer;
//     }
//   }
// }

.rent-page {
  display: none;
  flex-direction: column;
  width: 100%;
  background: #f2f3f5;
  .title {
    padding: 15px;
  }
  .data-renter {
    background: white;
    width: 1060px;
    margin-left: 30px;
    margin-bottom: 50px;
    border-radius: 10px;
    box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.25);
    padding: 20px;
    box-sizing: border-box;
    transition: 0.5s;
    .renter {
      display: flex;
      flex-wrap: wrap;
      width: 100%;
      padding: 10px;
      box-sizing: border-box;
      .reg {
        display: flex;
        align-items: center;
        margin-right: 50px;
        .search {
          height: 30px;
          width: 945px;
          border: 0.5px solid #bababa;
          border-radius: 5px 0 0 5px;
          padding: 0 0 0 10px;
          color: #bababa;
          font-size: 14px;
        }
        .blue {
          display: flex;
          align-items: center;
          justify-content: center;
          background: #0066ff;
          height: 32px;
          width: 31px;
          color: #ffffff;
          border-radius: 0 10px 10px 0;
        }
      }
    }
    .list-renter {
      display: flex;
      position: relative;
      width: 100%;
      height: 150px;
      box-shadow: 0px 5px 9px -2px rgba(0, 0, 0, 0.1);
      padding: 15px;
      box-sizing: border-box;
      margin-bottom: 10px;
      .image {
        img {
          width: 120px;
        }
      }
      .info {
        display: flex;
        flex-direction: column;
        height: 100%;
        margin-left: 15px;
        justify-content: space-between;
        padding: 3px;
        box-sizing: border-box;
        font-size: 14px;
        .phone {
          display: flex;
          p {
            font-size: 12px;
          }
          .or {
            color: #0066ff;
            margin-right: 5px;
          }
        }
        .status {
          display: flex;
          p {
            font-size: 12px;
          }
          .vi {
            color: #82bf96;
            margin-right: 5px;
            font-size: 12px;
          }
        }
      }
      .button-group {
        display: flex;
        position: absolute;
        right: 30px;
        top: 30px;
        flex-direction: column;
        .delete {
          border: 1px solid rgba(247, 10, 10, 0.842);
          color: rgba(247, 10, 10, 0.842);
          background: #ffffff;
          padding: 10px 20px;
          border-radius: 5px;
          cursor: pointer;
        }
        .edit {
          border: none;
          color: #ffffff;
          background: #0066ff;
          padding: 10px 20px;
          border-radius: 5px;
          cursor: pointer;
          margin-bottom: 10px;
        }
      }
    }
  }
  .addexpand {
    width: 1290px;
    .list-renter {
      .info {
        .data {
          margin-left: 170px;
        }
      }
    }
  }
}

@media only screen and (max-width: 1024px) {
  .color-page {
    display: none;
    flex-direction: column;
    width: 100%;
    background: #f2f3f5;
    .title {
      padding: 15px;
    }
    .car-color {
      background: white;
      width: 700px;
      margin-left: 30px;
      margin-bottom: 50px;
      border-radius: 10px;
      box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.25);
      padding: 20px;
      box-sizing: border-box;
      transition: 0.5s;
      .color {
        display: flex;
        flex-wrap: wrap;
        width: 100%;
        padding: 10px;
        box-sizing: border-box;
        .reg {
          display: flex;
          align-items: center;
          margin-right: 50px;
          .warna {
            height: 30px;
            width: 150px;
            border: 0.5px solid #bababa;
            border-radius: 5px 0 0 5px;
            color: #bababa;
          }
          .blue {
            display: flex;
            align-items: center;
            justify-content: center;
            background: #0066ff;
            height: 30px;
            width: 30px;
            color: #ffffff;
            border-radius: 0 10px 10px 0;
          }
        }
      }
      .list-color {
        display: flex;
        width: 100%;
        height: 100px;
        box-shadow: 0px 5px 9px -2px rgba(0, 0, 0, 0.1);
        padding: 15px;
        box-sizing: border-box;
        margin-bottom: 10px;
        .info {
          display: flex;
          height: 100%;
          justify-content: space-between;
          padding: 3px;
          box-sizing: border-box;
          font-size: 14px;
          .data {
            margin-left: 81px;
          }
          .phone {
            display: flex;
            p {
              font-size: 12px;
            }
            .or {
              color: #0066ff;
              margin-right: 5px;
            }
          }
          .status {
            display: flex;
            p {
              font-size: 12px;
            }
            .vi {
              color: #82bf96;
              margin-right: 5px;
              font-size: 12px;
            }
          }
        }
      }
    }
  }
}
</style>
