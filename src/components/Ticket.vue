<template>
  <div id="main">
    <div class="header">
      <div class="headImage" style=""></div>
      <div class="eventDate">
        <div>
          <div class="calendar">
            <i class="far fa-calendar-alt"></i>
          </div>
          <div style="text-align: center">
            <p>
              08.05.2020 <br />
              13.45
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="mainContent">
      <div class="title">
        <p>
          "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
          minim veniam, quis nostrud exercitation ullamco laboris nisi ut
          aliquip ex ea commodo consequat. Duis aute irure dolor in
          reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
          pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
          culpa qui officia deserunt mollit anim id est laborum."
        </p>
      </div>
      <div class="map">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3011.455545334259!2d29.06739131533601!3d40.99340142828909!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x14cac7ea2920a553%3A0x655f531b1807e040!2sBusiness%20%C4%B0stanbul!5e0!3m2!1str!2str!4v1620417572775!5m2!1str!2str"
          width="300"
          height="250"
          style="border:0;"
          allowfullscreen=""
          loading="lazy"
        ></iframe>
      </div>
    </div>
    <div class="buyTicket">
      <div>
        <div class="location">
          <b-button style="margin-right:10px">loc 1</b-button>
          <b-button style="margin-right:10px" disabled>loc 2</b-button>
          <b-button style="margin-right:10px" disabled>loc 3</b-button>
        </div>
        <div class="seatComp">
          <div id="seats-container">
            <div
              v-for="(seat, index) in seats"
              :key="index"
              :class="seat.class"
              @click="foo(seat)"
            >
              {{ seat.name }}
            </div>
          </div>
        </div>
        <div
          class="credentials"
          v-for="(seat, index) in this.selectedSeats"
          :key="index"
        >
          <div class="col-md-12 subTitle">
            <h3>Alan: loc1 - Koltuk Numarası: {{ seat.name }}</h3>
          </div>
          <div class="subIninput" style="margin: 0 auto;">
            <div class="inputField">
              <input type="text" placeholder="İsim" v-model="seat.firstname" />

              <input
                type="text"
                placeholder="Soyisim"
                v-model="seat.lastname"
              />
            </div>

            <div class="clear"></div>
            <div class="inputField">
              <input type="text" placeholder="E-mail" v-model="seat.email" />

              <input type="text" placeholder="Telefon" v-model="seat.tel" />
            </div>

            <div class="clear">&nbsp;</div>
          </div>
        </div>
        <div style="margin-top:10px;" v-if="this.selectedSeats.length != 0">
          <h3>Fatura Detayları</h3>
        </div>
        <div class="credentials" v-if="this.selectedSeats.length != 0">
          <div class="col-md-12 subTitle"></div>
          <div class="subIninput">
            <div style="width:fit-content; margin:0 auto;">
              <label for="Kişisel"
                ><input type="radio" id="Kişisel" checked />Kişisel</label
              >
              <label style="margin: 12px;" for="Kurumsal"
                ><input type="radio" id="Kurumsal" disabled />Kurumsal</label
              >
            </div>
            <div class="clear"></div>
            <div class="inputField">
              <input
                type="text"
                placeholder="İsim Soyisim"
                v-model="billing.name"
              />

              <input
                type="text"
                placeholder="Kimlik No"
                v-model="billing.personalId"
              />
            </div>

            <div class="clear"></div>

            <div class="inputField">
              <input type="text" placeholder="E-mail" v-model="billing.email" />

              <input type="text" placeholder="Telefon" v-model="billing.tel" />
            </div>

            <div class="clear">&nbsp;</div>
          </div>
        </div>
        <div style="margin-top:10px;" v-if="this.selectedSeats.length != 0">
          <h3>Ödeme Bilgileri</h3>
        </div>
        <div class="credentials" v-if="this.selectedSeats.length != 0">
          <div class="col-md-12 subTitle"></div>
          <div class="subIninput">
            <div class="clear"></div>
            <div class="inputField" style="width:95%">
              <input
                type="text"
                placeholder="Kart Sahibi"
                v-model="cardDetails.owner"
                style="width: 100%;margin: 10px 0px 10px 13px;"
              />
            </div>

            <div class="clear"></div>

            <div class="inputField" style="width:95%">
              <input
                type="text"
                placeholder="Kart Numarası"
                v-model="cardDetails.number"
              />

              <input
                type="text"
                placeholder="Ay"
                v-model="cardDetails.expMonth"
              />
              <input
                type="text"
                placeholder="Yıl"
                v-model="cardDetails.expYear"
              />
              <input type="text" placeholder="CVV" v-model="cardDetails.cvv" />
            </div>

            <div class="clear">&nbsp;</div>

            <b-button style="float:right" @click="finishPayment"
              >Ödemeyi Tamamla</b-button
            >

            <div class="clear">&nbsp;</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Ticket App",
  data() {
    return {
      billing: {
        name: null,
        personalId: null,
        email: null,
        telephone: null,
      },
      cardDetails: {
        owner: null,
        number: null,
        expMonth: null,
        expYear: null,
        cvv: null,
      },
      selectedSeats: [],
      seats: [
        { class: "emptyseat", name: "" },
        { class: "emptyseat", name: "" },
        { class: "emptyseat", name: "" },
        { class: "seat", name: "1" },
        { class: "seat", name: "2" },
        { class: "seat", name: "3" },
        { class: "seat", name: "4" },
        { class: "seat", name: "5" },
        { class: "seat", name: "6" },
        { class: "seat", name: "7" },
        { class: "seat", name: "8" },
        { class: "seat gap", name: "9" },
        { class: "seat", name: "10" },
        { class: "seat", name: "11" },
        { class: "seat", name: "12" },
        { class: "seat", name: "13" },
        { class: "seat", name: "14" },
        { class: "seat", name: "15" },
        { class: "clear", name: "" },
        { class: "emptyseat", name: "" },
        { class: "seat", name: "16" },
        { class: "seat", name: "17" },
        { class: "seat", name: "18" },
        { class: "seat", name: "19" },
        { class: "seat", name: "20" },
        { class: "seat", name: "21" },
        { class: "seat", name: "22" },
        { class: "seat", name: "23" },
        { class: "seat", name: "24" },
        { class: "seat", name: "25" },
        { class: "seat gap", name: "26" },
        { class: "seat", name: "27" },
        { class: "seat", name: "28" },
        { class: "seat", name: "29" },
        { class: "seat", name: "30" },
        { class: "seat", name: "31" },
        { class: "seat", name: "32" },
        { class: "seat", name: "33" },
        { class: "clear", name: "" },
        { class: "seat", name: "34" },
        { class: "seat", name: "35" },
        { class: "seat", name: "36" },
        { class: "seat", name: "37" },
        { class: "seat", name: "38" },
        { class: "seat", name: "39" },
        { class: "seat", name: "40" },
        { class: "seat", name: "41" },
        { class: "seat", name: "42" },
        { class: "seat", name: "43" },
        { class: "seat", name: "44" },
        { class: "seat gap", name: "45" },
        { class: "seat", name: "46" },
        { class: "seat", name: "47" },
        { class: "seat", name: "48" },
        { class: "seat", name: "49" },
        { class: "seat", name: "50" },
        { class: "seat", name: "51" },
        { class: "seat", name: "52" },
        { class: "seat", name: "53" },
        { class: "clear", name: "" },
        { class: "seat", name: "54" },
        { class: "seat", name: "55" },
        { class: "seat", name: "56" },
        { class: "seat", name: "57" },
        { class: "seat", name: "58" },
        { class: "seat", name: "59" },
        { class: "seat", name: "60" },
        { class: "seat", name: "61" },
        { class: "seat", name: "62" },
        { class: "seat", name: "63" },
        { class: "seat", name: "64" },
        { class: "seat gap", name: "65" },
        { class: "seat", name: "66" },
        { class: "seat", name: "67" },
        { class: "seat", name: "68" },
        { class: "seat", name: "69" },
        { class: "seat", name: "70" },
        { class: "seat", name: "71" },
        { class: "seat", name: "72" },
        { class: "seat", name: "73" },
        { class: "seat", name: "74" },
        { class: "clear", name: "" },
        { class: "emptyseat", name: "" },
        { class: "seat", name: "75" },
        { class: "seat", name: "76" },
        { class: "seat", name: "77" },
        { class: "seat", name: "78" },
        { class: "emptyseat", name: "" },
        { class: "seat", name: "79" },
        { class: "seat", name: "80" },
        { class: "seat", name: "81" },
        { class: "seat", name: "82" },
        { class: "seat", name: "83" },
        { class: "seat gap", name: "84" },
        { class: "seat", name: "85" },
        { class: "seat", name: "86" },
        { class: "seat", name: "87" },
        { class: "emptyseat", name: "" },
        { class: "seat", name: "88" },
        { class: "seat", name: "89" },
        { class: "clear", name: "" },
      ],
    };
  },
  methods: {
    foo(item) {
      if (this.selectedSeats != []) {
        if (this.selectedSeats.some((x) => x.name == item.name)) {
          item.class = item.class.replace("seatSelected", "");
          this.removeElement(this.selectedSeats, item.name);
        } else {
          this.selectedSeats.push({
            name: item.name,
            firstname: "",
            lastname: "",
            email: "",
            tel: "",
          });
          item.class = item.class + " " + "seatSelected";
        }
      }
    },
    removeElement(array, elem) {
      var index = array.findIndex((k) => k.name == elem);
      while (index > -1) {
        array.splice(index, 1);
        index = array.indexOf(elem);
      }
    },
    finishPayment() {
      if (
        Object.values(this.billing).every((x) => x === null || x === "") ||
        Object.values(this.selectedSeats).every(
          (x) => x === null || x === ""
        ) ||
        Object.values(this.cardDetails).every((x) => x === null || x === "")
      ) {
        alert("Lütfen Bütün boş alanları doldurun");
        console.log(this);
      } else {
        this.selectedSeats = [];
        for (var seat in this.seats) {
          this.seats[seat].class = this.seats[seat].class.replace(
            "seatSelected",
            ""
          );
        }
        this.billing = {
          name: null,
          personalId: null,
          email: null,
          telephone: null,
        };
        this.cardDetails = {
          owner: null,
          number: null,
          expMonth: null,
          expYear: null,
          cvv: null,
        };
        alert("Ödeme İşlemi Başarıyla Gerçekleştirilmiştir");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#main {
  width: 90%;
  margin: 0 auto;
}
.header {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}
.headImage {
  height: 250px;
  width: 835px;
  background: url("https://img.imageus.dev/https://images.theconversation.com/files/67096/original/image-20141212-6033-1xtql1v.jpg?width=835&height=250&mode=cover");
}
.eventDate {
  height: 250px;
  width: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.calendar {
  text-align: center;
  font-size: 70px;
  margin-bottom: 20px;
}

.mainContent {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.title {
  height: 250px;
  width: 835px;
  text-align: center;
  display: flex;
  align-items: center;
}

.map {
  height: 250px;
  width: 300px;
}

.buyTicket {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px auto;
}
.seatComp {
  border: 1px solid black;
}

#seats-container {
  width: 1110px;
  margin: auto;
}

.emptyseat {
  width: 50px;
  height: 50px;
  float: left;
}

.seat {
  width: 40px;
  height: 40px;
  border: 1px solid black;
  float: left;
  margin: 5px;
  background-color: #eee;
  padding-left: 7px;
  padding-top: 4px;
  -webkit-transition: background-color 500ms linear;
  -ms-transition: background-color 500ms linear;
  transition: background-color 500ms linear;
  cursor: pointer;
}
.seatSelected {
  background: darkred;
  color: white;
}

.clear {
  clear: both;
}

.gap {
  margin-left: 65px;
}
.credentials {
  border: 1px solid black;
  margin-top: 10px;
}
.subTitle > h3 {
  margin: 12px;
}
.subIninput label {
  padding: 5px;
}
.subIninput label > input {
  padding: 3px;
  margin-right: 6px;
}
.inputField {
  display: flex;
  justify-content: space-around;
}
.inputField input {
  float: left;
  width: 300px;
  align-items: center;
  margin-bottom: 12px;
  margin-left: 12px;
}
</style>
