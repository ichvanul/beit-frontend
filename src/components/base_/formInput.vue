<template>
  <div class="form-page">
    <section class="title">
      <h1>Input Data Penyewa</h1>
    </section>
    <div class="input-renter" v-bind:class="{ addexpand: expanded }">
      <form @submit.prevent="save()" class="form">
        <div class="form-group">
          <label for="name">Nama Penyewa</label>
          <input
            type="text"
            v-model="form.name"
            v-model.trim="$v.name.$model"
            name=""
            value=""
            id="name"
            placeholder="Salman"
          />
        </div>
        <div class="form-group">
          <label for="card_id">No. KTP</label>
          <input
            type="number"
            v-model="form.card_id"
            number=""
            value=""
            id="card_id"
            placeholder="102030405060"
          />
        </div>
        <div class="form-group">
          <label for="address">Alamat</label>
          <input
            type="text"
            v-model="form.address"
            address=""
            value=""
            id="address"
            placeholder="Vila Bekasi Indah Blok A No.12 Kota Bekasi"
          />
        </div>
        <div class="form-group">
          <label for="phone">No. Telepon</label>
          <input
            type="number"
            v-model="form.phone"
            telp=""
            value=""
            id="phone"
            placeholder="082218318835"
          />
        </div>
        <div class="form-group">
          <label for="email">Email</label>
          <input
            type="email"
            v-model="form.email"
            email=""
            value=""
            id="email"
            placeholder="salman@gmail.com"
          />
        </div>
        <div class="button-group">
          <button type="submit" class="save">SIMPAN</button>
          <button class="cancel">HAPUS</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { required, minLength, between } from "vuelidate/lib/validators";

export default {
  name: "form-input",
  props: ["expanded"],
  data() {
    return {
      form: {
        name: "",
        card_id: "",
        phone: "",
        address: "",
        email: ""
      }
    };
  },
  validations: {
    name: {
      required,
      minLength: minLength(4)
    },
    age: {
      between: between(20, 30)
    }
  },
  methods: {
    save() {
      axios
        .post(
          `https://www.penyewaankapal.attayasagroup.co.id/public/api/renter`,
          this.form
        )
        .then(() => {
          alert("Data Masuk");
          this.form = {};
          // this.$router.push({ path: "/" });
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.form-page {
  display: none;
  flex-direction: column;
  width: 100%;
  background: #f2f3f5;
  .title {
    padding: 15px;
  }
  .input-renter {
    background: white;
    width: 1060px;
    margin-left: 30px;
    margin-bottom: 175px;
    border-radius: 10px;
    box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.25);
    padding: 20px;
    box-sizing: border-box;
    transition: 0.5s;
    .form {
      display: flex;
      flex-wrap: wrap;
      width: 100%;
      border: #c7c2c2 1px solid;
      border-radius: 10px;
      padding: 10px;
      box-sizing: border-box;
      .form-group {
        display: flex;
        flex-direction: column;
        margin: 0 8px;
        input {
          border: 1px solid #c7c2c2;
          border-radius: 5px;
          width: 470px;
          height: 35px;
          margin: 5px 0;
          padding-left: 10px;
        }
      }
    }
    .button-group {
      margin-top: 23px;
      margin-left: 8px;
      .cancel {
        border: 1px solid rgba(247, 10, 10, 0.842);
        color: rgba(247, 10, 10, 0.842);
        background: #ffffff;
        padding: 10px 20px;
        border-radius: 5px;
        margin-left: 20px;
        cursor: pointer;
      }
      .save {
        border: none;
        color: #ffffff;
        background: #0066ff;
        padding: 10px 20px;
        border-radius: 5px;
        cursor: pointer;
      }
    }
  }
  .addexpand {
    width: 1290px;
    .form {
      .form-group {
        input {
          width: 1190px;
        }
      }
    }
  }
}

@media only screen and (max-width: 1024px) {
  .form-page {
    display: none;
    flex-direction: column;
    width: 100%;
    background: #f2f3f5;
    .title {
      padding: 15px;
    }
    .input-car {
      background: white;
      width: 700px;
      margin-left: 30px;
      margin-top: 10px;
      margin-bottom: 70px;
      border-radius: 10px;
      box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.25);
      padding: 20px;
      box-sizing: border-box;
      transition: 0.5s;
      .form {
        display: flex;
        flex-wrap: wrap;
        width: 100%;
        border: #c7c2c2 1px solid;
        border-radius: 10px;
        padding: 10px;
        box-sizing: border-box;
        .form-group {
          display: flex;
          flex-direction: column;
          margin: 0 8px;
          input {
            border: 1px solid #c7c2c2;
            border-radius: 5px;
            width: 600px;
            height: 35px;
            margin: 5px 0;
          }
        }
      }
      h3 {
        margin-top: 10px;
      }
      .ticket {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 380px;
        border: 1px solid #c7c2c2;
        border-radius: 8px;
        padding: 20px;
        box-sizing: border-box;
        margin-top: 10px;
        h1 {
          margin-bottom: 5px;
        }
        .info {
          margin-bottom: 10px;
        }
        .note {
          font-size: 10px;
        }
      }
      .button-group {
        margin-top: 20px;
        .cancel {
          border: 1px solid rgba(247, 10, 10, 0.842);
          color: rgba(247, 10, 10, 0.842);
          background: #ffffff;
          padding: 10px 20px;
          border-radius: 5px;
          margin-left: 20px;
          cursor: pointer;
        }
        .print {
          border: none;
          color: #ffffff;
          background: #0066ff;
          padding: 10px 20px;
          border-radius: 5px;
          cursor: pointer;
        }
        .save {
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
}
</style>
