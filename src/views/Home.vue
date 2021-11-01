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
            <div class="table_key">
            <span>Raw Material: </span>
            <span>Dog beds made from virgin polyester</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Co2 per ton: </span>
              <span>18,750</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>32,305,000</span>
            </div>
            <div class="table_value_item">
              <span>Barrels of oil: </span>
              <span>3,500</span>
            </div>
          </div>
          </div>
          <div class="table_content">
            <div class="table_key">
            <span>Raw Material: </span>
            <span>Dog beds made from RECYCLED polyester</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Co2 per ton: </span>
              <span>4,687</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>4,522,700</span>
            </div>
            <div class="table_value_item">
              <span>Barrels of oil: </span>
              <span>1,050</span>
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
              <span>14,062</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>27,782,300</span>
            </div>
            <div class="table_value_item">
              <span>Barrels of oil: </span>
              <span>2,450</span>
            </div>
          </div>
          </div>
        </div>
        <div class="table">
          <label class="table_header_label">Leather collar and leash analysis</label>
          <div class="table_content">
            <div class="table_key">
            <span>Raw Material: </span>
            <span>Traditional leather collar</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>5,296,000</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>68,848</span>
            </div>
          </div>
          </div>
          <div class="table_content">
            <div class="table_key">
            <span>Raw Material: </span>
            <span>Recycled leather collar</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>529,600</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>6,885</span>
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
              <span>4,766,400</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>61,963</span>
            </div>
          </div>
          </div>
          <br/>
          <div class="table_content">
            <div class="table_key">
            <span>Raw Material: </span>
            <span>Traditional leather leash</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>16,020,400</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>208,265</span>
            </div>
          </div>
          </div>
          <div class="table_content">
            <div class="table_key">
            <span>Raw Material: </span>
            <span>Recycled leather leash</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Litres of water used: </span>
              <span>1,456,400</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>18,933</span>
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
              <span>14,564,000</span>
            </div>
            <div class="table_value_item">
              <span>Water used (Bath tubs): </span>
              <span>189,332</span>
            </div>
          </div>
          </div>
        </div>
        <div class="table">
          <label class="table_header_label">Co2 saving per item</label>
          <div class="table_content">
            <div class="table_key">
            <span>Raw Material: </span>
            <span>Recycled leather collar</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Co2 saved (tons): </span>
              <span>558</span>
            </div>
          </div>
        </div>
        <div class="table_content">
            <div class="table_key">
            <span>Raw Material: </span>
            <span>Recycled leather leash</span>
          </div>
          <div class="table_value_container">
            <div class="table_value_item">
              <span>Co2 saved (tons): </span>
              <span>1536</span>
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
              'Access-Control-Allow-Origin': '*',
              'Access-Control-Allow-Headers': 'Origin, Accept, Content-Type, X-Requested-With, X-CSRF-Token',
              'Access-Control-Allow-Methods': 'PUT, GET, POST, DELETE, OPTIONS',
            },
          },
        ).then((res) => res);
        this.isLoading = false;
        console.log(response);
      } catch (err) {
        this.isLoading = false;
        console.log(err);
      }
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
</style>
