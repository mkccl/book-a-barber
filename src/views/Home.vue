<template>
  <MultiStepHeader :step="1" />
  <PlzHannover />

  <div class="primaryFeature">
    <article class="firstPage">
      <h1>Dein Barbier <br />kommt zu dir!</h1>
      <section class="plzSearch">
        <label for="PLZ"></label>
        <input
          placeholder="Your postcode"
          type="text"
          id="PLZ"
          v-model="postcode"
          @keypress.enter="findPlz()"
        />

        <router-link to="/Services"> </router-link
        ><button @click="findPlz()">Search</button>
        <div class="overlay" v-if="validation">
          <div class="validationTxt">
            {{ validation }}
            <button class="validBtn" @click="this.validation = false">
              Okay
            </button>
          </div>
        </div>
      </section>
    </article>
  </div>
</template>

<script>
import PlzHannover from "@/components/PlzHannover.js";
import MultiStepHeader from "@/components/MultiStepHeader.vue";

export default {
  name: "Home",
  data() {
    return {
      postcode: "",
      validation: "",
    };
  },
  components: {
    MultiStepHeader,
  },

  methods: {
    findPlz() {
      const plzAsNumber = Number.parseInt(this.postcode);
      if (PlzHannover.includes(plzAsNumber)) {
        this.$router.push("/Services");
      } else {
        //alert("Sorry, this is not Hannover");
        this.validation = "Sorry, this is not Hannover";
      }
    },
  },
};
</script>

<style>
.primaryFeature {
  display: flex;
  align-items: center;
  justify-content: center;
  background-image: url("https://baerte.info/wp-content/uploads/2019/06/barber.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  margin: auto;
  width: 100%;
  min-width: 70vw;
  min-height: 60vw;
}
.firstPage {
  display: flex;
  flex-direction: column;
  /* justify-content: center;
  align-items: center; */
  color: white;
  margin: 0;
  width: 100%;
}

.overlay {
  position: relative;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.validationTxt {
  position: absolute;
  display: flex;
  font-size: 1.5rem;
  width: 35vw;
  height: 25vw;
  padding: 1.5rem;
  text-align: center;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(40px);
  margin: auto;
  border-radius: 10%;
}

.validBtn {
  display: flex;
  position: absolute;
  align-self: flex-end;
  background: rgb(181, 181, 181);
  border: rgb(131, 131, 131) solid 2px;
  padding: 0.3rem 0.6rem;
}

.validBtn:hover {
  background-color: rgb(131, 131, 131);
}

/* input {
  display: block;
  width: 80%;
  justify-content: center;
}
button {
  display: block; */

.plzSearch {
  display: flex;
  justify-content: center;
  width: 80%;
}

h1 {
  width: 100%;
  justify-content: left;
}

@media screen and (min-width: 768px) {
  .primaryFeature {
    display: flex;
    align-items: center;
    justify-content: center;
    background-image: url("https://baerte.info/wp-content/uploads/2019/06/barber.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    margin: auto;
    min-width: 70vw;
    min-height: 60vw;
  }
}
</style>
