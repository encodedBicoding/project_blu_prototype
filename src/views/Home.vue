<template>
  <div class="home">
    <div class="loader" v-if="isLoading">
      <img src="../assets/spinner.svg" width="130px" height="130px"/>
    </div>
    <div :class="hasResults ? 'form_container result' : 'form_container no_result'">
     <div class="form_main" v-if="!hasResults">
      <div class="form_item_container">
        <div class="form_item">
          <label class="label">No. of Dog beds sold per year</label>
          <input type="tel" class="form_input form_field" v-model="noOfDogBedsSold"/>
        </div>
        <div class="form_item">
          <label class="label">Average weight of Dog bed</label>
          <select class="form_field form_select" v-model="averageDogBedWeight">
            <option selected value="3.5">3.5kg</option>
            <option value="2.5">2.5kg</option>
          </select>
        </div>
      </div>
       <div class="form_item_container">
        <div class="form_item">
          <label class="label">No. of leather collar sold</label>
          <input type="tel" class="form_input form_field" v-model="noOfLeatherCollarSold"/>
        </div>
        <div class="form_item">
          <label class="label">No. of leather leashes sold</label>
          <input type="tel" class="form_input form_field" v-model="noOfLeatherLeashesSold"/>
        </div>
      </div>
      <div class="submit_container">
        <button class="button" type="submit" v-on:click="processData">proceed</button>
      </div>
     </div>
      <div class="results" v-if="hasResults">
        <div class="table">
          <label class="table_header_label">Carbon footprint analysis per year</label>
          <div class="table_content">
            <div class="table_key font_bold">
              <span>Raw Material: </span>
              <span>Dog beds made from virgin polyester</span>
            </div>
            <div class="table_value_container">
              <div class="table_value_item">
                <span>Co2 per ton: </span>
                <span>{{
                  formatCurrency(dog_beds_made_from_virgin_polyester.co2_per_ton)
                  }}</span>
              </div>
              <div class="table_value_item">
                <span>Water used (Bath tubs): </span>
                <span>{{
                  formatCurrency(dog_beds_made_from_virgin_polyester.water_used_bath_tubs)
                  }}</span>
              </div>
              <div class="table_value_item">
                <span>Barrels of oil: </span>
                <span>{{
                  formatCurrency(dog_beds_made_from_virgin_polyester.barrels_of_oil)
                }}</span>
              </div>
            </div>
          </div>
          <div class="table_content">
            <div class="table_key font_bold">
            <span>Raw Material: </span>
            <span>Dog beds made from RECYCLED polyester</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Co2 per ton: </span>
              <span>{{
                formatCurrency(dog_beds_made_from_recycled_polyester.co2_per_ton)
              }}</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>{{
                formatCurrency(dog_beds_made_from_recycled_polyester.water_used_bath_tubs)
              }}</span>
            </div>
            <div class="table_value_item">
              <span>Barrels of oil: </span>
              <span>{{
                formatCurrency(dog_beds_made_from_recycled_polyester.barrels_of_oil)
              }}</span>
            </div>
          </div>
          </div>
          <div class="table_content">
            <div class="table_key">
              <span>Total Saving</span>
            </div>
             <div class="table_value_container">
            <div class="table_value_item">
              <span>Co2 per ton: </span>
              <span>{{formatCurrency(total_saving.co2_per_ton)}}</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>{{formatCurrency(total_saving.water_used_bath_tubs)}}</span>
            </div>
            <div class="table_value_item">
              <span>Barrels of oil: </span>
              <span>{{formatCurrency(total_saving.barrels_of_oil)}}</span>
            </div>
          </div>
          </div>
        </div>
        <div class="table">
          <label class="table_header_label">Leather collar and leash analysis</label>
          <div class="table_content">
            <div class="table_key font_bold">
            <span>Raw Material: </span>
            <span>Traditional leather collar</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>{{
                formatCurrency(traditional_leather_collar.litres_of_water_used)
              }}</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>{{
                formatCurrency(traditional_leather_collar.water_used_bath_tubs)
              }}</span>
            </div>
          </div>
          </div>
          <div class="table_content">
            <div class="table_key font_bold">
            <span>Raw Material: </span>
            <span>Recycled leather collar</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>{{
                formatCurrency(recycled_leather_collar.litres_of_water_used)
                }}</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>{{
                formatCurrency(recycled_leather_collar.water_used_bath_tubs)
              }}</span>
            </div>
          </div>
          </div>
          <div class="table_content">
            <div class="table_key">
              <span>Water Saving</span>
            </div>
             <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>{{
                formatCurrency(collar_water_saving.litres_of_water_used)
              }}</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>{{formatCurrency(collar_water_saving.water_used_bath_tubs)}}</span>
            </div>
          </div>
          </div>
          <br/>
          <div class="table_content">
            <div class="table_key font_bold">
            <span>Raw Material: </span>
            <span>Traditional leather leash</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>{{
                formatCurrency(traditional_leather_leash.litres_of_water_used)
              }}</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>{{
                formatCurrency(traditional_leather_leash.water_used_bath_tubs)
              }}</span>
            </div>
          </div>
          </div>
          <div class="table_content">
            <div class="table_key font_bold">
            <span>Raw Material: </span>
            <span>Recycled leather leash</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>{{
                formatCurrency(recycled_leather_leash.litres_of_water_used)
              }}</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>{{
                formatCurrency(recycled_leather_leash.water_used_bath_tubs)
              }}</span>
            </div>
          </div>
          </div>
          <div class="table_content">
            <div class="table_key">
              <span>Water Saving</span>
            </div>
             <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>{{
                formatCurrency(leash_water_saving.litres_of_water_used)
              }}</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>{{
                formatCurrency(leash_water_saving.water_used_bath_tubs)
              }}</span>
            </div>
          </div>
          </div>
        </div>
        <div class="table">
          <label class="table_header_label">Co2 saving per item</label>
          <div class="table_content">
            <div class="table_key font_bold">
            <span>Raw Material: </span>
            <span>Recycled leather collar</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Co2 saved (tons): </span>
              <span>{{
                formatCurrency(co2_saving_per_item.recycled_leather_collar.co2_saved)
              }}</span>
            </div>
          </div>
        </div>
        <div class="table_content">
            <div class="table_key font_bold">
            <span>Raw Material: </span>
            <span>Recycled leather leash</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Co2 saved (tons): </span>
              <span>{{
                formatCurrency(co2_saving_per_item.recycled_leather_leash.co2_saved)
              }}</span>
            </div>
          </div>
        </div>
       </div>
      </div>
      <div class="submit_container" v-if="hasResults">
        <button class="button" type="submit" v-on:click="seen">seen</button>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import { AgGridVue } from 'ag-grid-vue';

export default {
  name: 'Home',
  components: {
    // AgGridVue,
  },
  beforeMount() {},
  data() {
    return {
      isLoading: false,
      hasResults: false,
      noOfDogBedsSold: 0,
      averageDogBedWeight: '3.5',
      noOfLeatherCollarSold: 0,
      noOfLeatherLeashesSold: 0,
      dog_beds_made_from_virgin_polyester: {
        co2_per_ton: 18750,
        water_used_bath_tubs: 32305000,
        barrels_of_oil: 3500,
      },
      dog_beds_made_from_recycled_polyester: {
        co2_per_ton: 18750,
        water_used_bath_tubs: 32305000,
        barrels_of_oil: 3500,
      },
      total_saving: {
        co2_per_ton: 18750,
        water_used_bath_tubs: 32305000,
        barrels_of_oil: 3500,
      },
      traditional_leather_collar: {
        litres_of_water_used: 18750,
        water_used_bath_tubs: 32305000,
      },
      recycled_leather_collar: {
        litres_of_water_used: 18750,
        water_used_bath_tubs: 32305000,
      },
      collar_water_saving: {
        litres_of_water_used: 18750,
        water_used_bath_tubs: 32305000,
      },
      traditional_leather_leash: {
        litres_of_water_used: 18750,
        water_used_bath_tubs: 32305000,
      },
      recycled_leather_leash: {
        litres_of_water_used: 18750,
        water_used_bath_tubs: 32305000,
      },
      leash_water_saving: {
        litres_of_water_used: 18750,
        water_used_bath_tubs: 32305000,
      },
      co2_saving_per_item: {
        recycled_leather_collar: {
          co2_saved: 558,
        },
        recycled_leather_leash: {
          co2_saved: 558,
        },
      },
    };
  },
  methods: {
    seen() {
      this.noOfDogBedsSold = 0;
      this.averageDogBedWeight = '3.5';
      this.noOfLeatherCollarSold = 0;
      this.noOfLeatherLeashesSold = 0;
      this.hasResults = false;
    },
    async processData() {
      try {
        const url = 'https://staging.bloverse.com/extraction/dog_details';
        this.isLoading = true;
        const response = await this.axios.post(
          url,
          {
            num_dog_beds_sold: this.noOfDogBedsSold,
            avg_bed_weight: Number(this.averageDogBedWeight),
            lea_lea_sold: this.noOfLeatherLeashesSold,
            lea_col_sold: this.noOfLeatherCollarSold,
          },
          {
            headers: {
              'Content-type': 'application/json',
            },
          },
        ).then((res) => res);
        this.isLoading = false;
        console.log(response);
        if (response.status === 200) {
          // dog bed;
          const dogBed = response.data.data[1];
          console.log(dogBed);
          this.dog_beds_made_from_virgin_polyester = dogBed.dog_beds_made_from_virgin_polyester;
          this.dog_beds_made_from_recycled_polyester = dogBed.dog_beds_made_from_recycled_polyester;
          this.total_saving = dogBed.total_saving;
          const collarLeash = response.data.data[3];
          this.collar_water_saving = collarLeash.collar_water_saving;
          this.leash_water_saving = collarLeash.leash_water_saving;
          this.recycled_leather_collar = collarLeash.recycled_leather_collar;
          this.recycled_leather_leash = collarLeash.recycled_leather_leash;
          this.traditional_leather_collar = collarLeash.traditional_leather_collar;
          this.traditional_leather_leash = collarLeash.traditional_leather_leash;
          this.hasResults = true;
        } else {
          this.isLoading = false;
          this.hasResults = false;
        }
      } catch (err) {
        this.isLoading = false;
        this.hasResults = false;
        console.log(err);
      }
    },
    formatCurrency(number) {
      return new Intl.NumberFormat('en-IN').format(number);
    },
  },
};
</script>
<style scoped >
.home {
  width: 100%;
  height: 100%;
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.results{
  width: 100%;
  position: relative;
  margin: 1rem;
  border: 1px solid rgba(128, 128, 128, 0.336);
  border-radius: 5px;
  overflow: scroll;
  max-height: calc(100vh - 10vh);
}
.form_container{
  height: auto;
  border-radius: 4px;
}
.form_container.no_result {
  display: flex;
  width: 36%;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  padding: .7rem;
}
.form_container.result {
  display: flex;
  width: 50%;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}
.form_main{
  width: 100%;
  border: 1px solid rgba(128, 128, 128, 0.336);
}
.form_item_container{
  display: flex;
  flex-direction: row;
  width: 100%;
}
.form_item{
  width: 100%;
  margin: .5rem .5rem 1.2rem .5rem;
}
.form_input,
.form_select{
  width: 95%;
}
.form_field{
  padding: .4rem;
  border-radius: 4px;
  outline: none;
  border: 1px solid gray;
}
.form_input {
  padding: .48rem;
}
.form_field:focus {
    border: 1px solid green;
}
.label{
  font-size: .7rem;
  font-weight: 700;
  text-transform: uppercase;
}
.submit_container{
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: .8rem;
}
.button{
  padding: .6rem;
  outline: none;
  width: 180px;
  border: 1px solid grey;
  border-radius: 5px;
  text-transform: uppercase;
  font-size: .7rem;
  background-color: green;
  color: #fff;
  font-weight: 600;
  cursor: pointer;
}
.table{
  border-bottom: 1px solid gray;
  margin: 1rem .4rem;
  padding-bottom: .6rem;
}
.table_header_label{
  font-weight: 600;
  font-size: 1.32rem;
  margin: .6rem 0;
}
.table_content{
  margin-top: .7rem;
}
.table_value_item{
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: space-between;
}
.loader{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.795);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.font_bold {
  font-weight: 700;
}
</style>
