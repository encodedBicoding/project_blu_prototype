<template>
  <div class="home">
    <div class="loader" v-if="isLoading">
      <img src="../assets/spinner.svg" width="130px" height="130px"/>
    </div>
    <div class="modal" v-if="showEditDataModal">
      <div class="analysis_form">
        <h4 name="dog bed analysis">Dog Bed Analysis</h4>
        <div class="form_item_container">
          <div class="form_item">
            <label class="label">Number of Dog beds sold per year</label>
            <input
              type="tel"
              class="form_input form_field"
              placeholder="Enter Amount"
              v-model="noOfDogBedsSold"/>
          </div>
          <div class="form_item">
            <label class="label">Average weight of Dog bed ( kg )</label>
            <select class="form_field form_select" v-model="averageDogBedWeight">
              <option value="4.5">4.5kg</option>
              <option selected value="3.5">3.5kg</option>
              <option value="2.5">2.5kg</option>
            </select>
          </div>
        </div>
        <br/>
          <h4 name="dog bed analysis">Leather collars and leash analysis</h4>
          <div class="form_item_container">
          <div class="form_item">
            <label class="label">Number of leather collars sold</label>
            <input
              type="tel"
              class="form_input form_field"
              placeholder="Enter Amount"
              v-model="noOfLeatherCollarSold"
            />
          </div>
          <div class="form_item">
            <label class="label">Number of leather leashes sold</label>
            <input type="tel"
            class="form_input form_field"
            placeholder="Enter Amount"
            v-model="noOfLeatherLeashesSold"
            />

          </div>
        </div>
        <div class="submit_container">
          <button class="button" type="submit" v-on:click="processData">Calculate</button>
        </div>
         <div class="close_container">
          <button class="close_button" type="submit" v-on:click="hideEditModal">Close</button>
        </div>
      </div>
    </div>
    <div class="modal" v-if="showCompanyModal" name="modal_for_company">
      <div class="modal_container">
        <div class="closer">
          <p class="closer_btn" v-on:click="toggleCompanyModal">x</p>
        </div>
        <h4 name="dog bed analysis">Select Company</h4>
        <div class="row_space_btwn_center">
          <div class="com_mod_img_con" v-on:click="selectCompany('pets_co')">
            <img src="../assets/petco_img.png" width="100%" height="100%"/>
          </div>
          <div class="com_mod_img_con" v-on:click="selectCompany('pets_at_home')">
            <img src="../assets/pets_at_home.png" width="100%" height="100%"/>
          </div>
        </div>
      </div>
    </div>
    <div v-if="!hasResults" class="starter_page">
      <NavBar/>
      <div class="main_container">
        <div class="analysis_form">
          <h4 name="dog bed analysis">Dog Bed Analysis</h4>
          <div class="form_item_container">
            <div class="form_item">
              <label class="label">Number of Dog beds sold per year</label>
              <input
                type="tel"
                class="form_input form_field"
                placeholder="Enter Amount"
                v-model="noOfDogBedsSold"/>
            </div>
            <div class="form_item">
              <label class="label">Average weight of Dog bed ( kg )</label>
              <select class="form_field form_select" v-model="averageDogBedWeight">
                <option value="4.5">4.5kg</option>
                <option selected value="3.5">3.5kg</option>
                <option value="2.5">2.5kg</option>
              </select>
            </div>
          </div>
          <br/>
           <h4 name="dog bed analysis">Leather collars and leash analysis</h4>
           <div class="form_item_container">
            <div class="form_item">
              <label class="label">Number of leather collars sold</label>
              <input
                type="tel"
                class="form_input form_field"
                placeholder="Enter Amount"
                v-model="noOfLeatherCollarSold"
              />
            </div>
            <div class="form_item">
              <label class="label">Number of leather leashes sold</label>
              <input type="tel"
              class="form_input form_field"
              placeholder="Enter Amount"
              v-model="noOfLeatherLeashesSold"
              />
            </div>
          </div>
          <div class="submit_container">
            <button class="button" type="submit" v-on:click="processData">Process</button>
          </div>
        </div>
        <div class="ecom_analysis_form">
          <h4 name="dog bed analysis">Ecommerce analysis</h4>
           <div class="form_item_container">
            <div class="form_item">
              <label class="label">Select company name</label>
              <div class="row_space_btwn_center ea_cont">
                <p class="ea_t">{{determineSelectedCompany()}}</p>
                <div class="ea_btn" v-on:click="toggleCompanyModal">
                  <p>Change</p>
                </div>
              </div>
            </div>
            <div class="form_item">
              <label class="label">Upload CSV</label>
              <input hidden v-on:change="selectCSV" accept=".csv" type="file" id="comp_csv"/>
              <div class="row_space_btwn_center ea_cont">
                <p class="ea_t">{{csvFileName}}</p>
                <div class="ea_btn" onclick="document.getElementById('comp_csv').click()">
                  <p>{{this.csvFile === null ? 'Select file' : 'Update file'}}</p>
                </div>
              </div>
            </div>
          </div>
           <div class="submit_container">
            <button class="button" type="submit" v-on:click="processDataCSV">Process</button>
          </div>
        </div>
      </div>
    </div>
    <div v-if="hasResults" class="results_page">
      <NavBar/>
      <div class="results_container">
        <h3 class="font_white">Processed Analysis</h3>
        <br/>
        <div class="result_cc">
          <div class="row_space_btwn_center result_cc_h wd_100">
            <div class="header_title">
              <h2>Project Blu</h2>
              <h2>Sustainability Report</h2>
            </div>
            <div class="sm_btn" v-on:click="showEditModal">
              Edit Data Input
            </div>
          </div>
          <section class="carbon_analysis">
            <h3 class="ct_p">Total Saving</h3>
            <div class="carbon_total">
              <div class="ct_data_container">
                <div class="ct_data_content_container bg_green">
                  <div class="icon_holder">
                    <img src="../assets/shp_4.svg" width="100%" height="100%"/>
                  </div>
                  <div class="ts_cc">
                    <p>c02 per ton</p>
                    <p class="cc_value">
                      {{formatCurrency(total_saving.co2_per_ton)}}
                    </p>
                  </div>
                </div>
                <div class="ct_data_content_container bg_blue">
                  <div class="icon_holder">
                    <img src="../assets/shp_5.svg" width="100%" height="100%"/>
                  </div>
                  <div class="ts_cc">
                    <p>WATER USED (BATH TUBS)</p>
                    <p class="cc_value">
                      {{formatCurrency(total_saving.water_used_bath_tubs)}}
                    </p>
                  </div>
                </div>
                <div class="ct_data_content_container bg_brown bottom">
                  <div class="icon_holder">
                    <img src="../assets/shp_6.svg" width="100%" height="100%"/>
                  </div>
                  <div class="ts_cc">
                    <p>BARRELS OF OIL</p>
                    <p class="cc_value">
                      {{formatCurrency(total_saving.barrels_of_oil)}}
                    </p>
                  </div>
                </div>
              </div>
            </div>
            <div class="table_container">
              <div class="ct_data_container">
                <h4 class="table_h">Raw material</h4>
                <p class="font_black font_small">Here's the breakdown of the calculation</p>
              </div>
              <div class="table_content_container">
                <div class="table_content">
                  <div class="tch">
                    <p>Dog beds made from virgin polyester</p>
                  </div>
                  <div class="tc_body">
                    <div class="tcb_content_container bg_light_green">
                      <img src="../assets/shp_1.svg" width="auto" height="25%" class="shp_icon"/>
                      <p>c02 per ton</p>
                      <p class="cc_value">
                        {{formatCurrency(dog_beds_made_from_virgin_polyester.co2_per_ton)}}
                      </p>
                    </div>
                    <div class="tcb_content_container bg_light_faint">
                      <img src="../assets/shp_2.svg" width="auto" height="25%" class="shp_icon"/>
                      <p>WATER USED (BATH TUBS)</p>
                      <p class="cc_value">
                        {{formatCurrency(dog_beds_made_from_virgin_polyester.water_used_bath_tubs)}}
                      </p>
                    </div>
                    <div class="tcb_content_container bg_light_cream bottom">
                      <img src="../assets/shp_3.svg" width="auto" height="25%" class="shp_icon"/>
                      <p>BARRELS OF OIL</p>
                      <p class="cc_value">
                        {{formatCurrency(dog_beds_made_from_virgin_polyester.barrels_of_oil)}}
                      </p>
                    </div>
                  </div>
                </div>
                <div class="table_content">
                  <div class="tch">
                    <p>Dog beds made from RECYCLED polyester</p>
                  </div>
                  <div class="tc_body">
                    <div class="tcb_content_container bg_light_green">
                      <img src="../assets/shp_1.svg" width="auto" height="25%" class="shp_icon"/>
                      <p>c02 per ton</p>
                      <p class="cc_value">
                        {{formatCurrency(dog_beds_made_from_recycled_polyester.co2_per_ton)}}
                      </p>
                    </div>
                    <div class="tcb_content_container bg_light_faint">
                      <img src="../assets/shp_2.svg" width="auto" height="25%" class="shp_icon"/>
                      <p>WATER USED (BATH TUBS)</p>
                      <p class="cc_value">
                        {{
                          formatCurrency(dog_beds_made_from_recycled_polyester.water_used_bath_tubs)
                        }}
                      </p>
                    </div>
                    <div class="tcb_content_container bg_light_cream bottom">
                      <img src="../assets/shp_3.svg" width="auto" height="25%" class="shp_icon"/>
                      <p>BARRELS OF OIL</p>
                      <p class="cc_value">
                        {{formatCurrency(dog_beds_made_from_recycled_polyester.barrels_of_oil)}}
                      </p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </section>
        </div>
        <div class="result_cc_second">
          <div class="cc_grid_container">
            <div class="grid_item">
              <p class="ct_p">Water Saving</p>
              <div class="row_space_btwn_start gi_card_bottom">
                <div class="wd_100">
                  <div class="bg_dark_blue gi_c_bottom_c">
                    <div class="icon_holder">
                      <img src="../assets/shp_7.svg" width="100%" height="100%"/>
                    </div>
                    <div class="ts_cc">
                      <p>LITRES OF WATER USED</p>
                      <p class="cc_value">
                        {{formatCurrency(collar_water_saving.litres_of_water_used)}}
                      </p>
                    </div>
                  </div>
                  <div class="bg_blue gi_c_bottom_c">
                    <div class="icon_holder">
                      <img src="../assets/shp_5.svg" width="100%" height="100%"/>
                    </div>
                    <div class="ts_cc">
                      <p>WATER USED (BATH TUBS)</p>
                      <p class="cc_value">
                        {{formatCurrency(collar_water_saving.water_used_bath_tubs)}}
                      </p>
                    </div>
                  </div>
                </div>
              </div>
              <div class="gi_content">
                <div class="tch">
                  <p>Traditional leather collar</p>
                </div>
                <div class="row_space_btwn_center">
                  <div class="tcb_content_container bg_light_green">
                    <img src="../assets/shp_8.svg" width="auto" height="25%" class="shp_icon"/>
                    <p>litres of water used</p>
                    <p class="cc_value">
                      {{formatCurrency(traditional_leather_collar.litres_of_water_used)}}
                    </p>
                  </div>
                  <div class="tcb_content_container bg_light_faint">
                    <img src="../assets/shp_2.svg" width="auto" height="25%" class="shp_icon"/>
                    <p>WATER USED (BATH TUBS)</p>
                    <p class="cc_value">
                      {{formatCurrency(traditional_leather_collar.water_used_bath_tubs)}}
                      </p>
                  </div>
                </div>
              </div>
              <div class="gi_content">
                <div class="tch">
                  <p>Recycled leather collar</p>
                </div>
                <div class="row_space_btwn_center">
                  <div class="tcb_content_container bg_light_green">
                    <img src="../assets/shp_8.svg" width="auto" height="25%" class="shp_icon"/>
                    <p>litres of water used</p>
                    <p class="cc_value">
                      {{formatCurrency(recycled_leather_collar.litres_of_water_used)}}
                    </p>
                  </div>
                  <div class="tcb_content_container bg_light_faint">
                    <img src="../assets/shp_2.svg" width="auto" height="25%" class="shp_icon"/>
                    <p>WATER USED (BATH TUBS)</p>
                    <p class="cc_value">
                      {{formatCurrency(recycled_leather_collar.water_used_bath_tubs)}}
                      </p>
                  </div>
                </div>
              </div>
            </div>
            <div class="grid_item">
              <p class="ct_p">Water Saving</p>
              <div class="row_space_btwn_start gi_card_bottom">
                <div class="wd_100">
                  <div class="bg_dark_blue gi_c_bottom_c">
                    <div class="icon_holder">
                      <img src="../assets/shp_7.svg" width="100%" height="100%"/>
                    </div>
                    <div class="ts_cc">
                      <p>LITRES OF WATER USED</p>
                      <p class="cc_value">
                        {{formatCurrency(leash_water_saving.litres_of_water_used)}}
                      </p>
                    </div>
                  </div>
                  <div class="bg_blue gi_c_bottom_c">
                    <div class="icon_holder">
                      <img src="../assets/shp_5.svg" width="100%" height="100%"/>
                    </div>
                    <div class="ts_cc">
                      <p>WATER USED (BATH TUBS)</p>
                      <p class="cc_value">
                        {{formatCurrency(leash_water_saving.water_used_bath_tubs)}}
                      </p>
                    </div>
                  </div>
                </div>
              </div>
              <div class="gi_content">
                <div class="tch">
                  <p>Traditional leather leash</p>
                </div>
                <div class="row_space_btwn_center">
                  <div class="tcb_content_container bg_light_green">
                    <img src="../assets/shp_8.svg" width="auto" height="25%" class="shp_icon"/>
                    <p>litres of water used</p>
                    <p class="cc_value">
                      {{formatCurrency(traditional_leather_leash.litres_of_water_used)}}
                    </p>
                  </div>
                  <div class="tcb_content_container bg_light_faint">
                    <img src="../assets/shp_2.svg" width="auto" height="25%" class="shp_icon"/>
                    <p>WATER USED (BATH TUBS)</p>
                    <p class="cc_value">
                      {{formatCurrency(traditional_leather_leash.water_used_bath_tubs)}}
                      </p>
                  </div>
                </div>
              </div>
              <div class="gi_content">
                <div class="tch">
                  <p>Recycled leather leash</p>
                </div>
                <div class="row_space_btwn_center">
                  <div class="tcb_content_container bg_light_green">
                    <img src="../assets/shp_8.svg" width="auto" height="25%" class="shp_icon"/>
                    <p>litres of water used</p>
                    <p class="cc_value">
                      {{formatCurrency(recycled_leather_leash.litres_of_water_used)}}
                    </p>
                  </div>
                  <div class="tcb_content_container bg_light_faint">
                    <img src="../assets/shp_2.svg" width="auto" height="25%" class="shp_icon"/>
                    <p>WATER USED (BATH TUBS)</p>
                    <p class="cc_value">
                      {{formatCurrency(recycled_leather_leash.water_used_bath_tubs)}}
                      </p>
                  </div>
                </div>
              </div>
            </div>
            <div class="grid_item h_fit">
              <h4 class="table_h">Co2 saving per item</h4>
              <div class="tch">
                <p>Recycled leather collar</p>
              </div>
              <div class="tcb_content_container_mini bg_light_faint">
                <img src="../assets/shp_9.svg" width="auto" height="25%" class="shp_icon"/>
                <p>c02 saved (tons)</p>
                <p class="cc_value">
                  {{formatCurrency(
                    co2_saving_per_item.recycled_leather_collar.co2_saved
                  )}}
                </p>
              </div>
              <br/>
              <div class="tch">
                <p>Recycled leather leash</p>
              </div>
              <div class="tcb_content_container_mini bg_light_faint">
                <img src="../assets/shp_9.svg" width="auto" height="25%" class="shp_icon"/>
                <p>c02 saved (tons)</p>
                <p class="cc_value">
                  {{formatCurrency(
                    co2_saving_per_item.recycled_leather_leash.co2_saved
                  )}}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from '@/components/NavBar.vue';

export default {
  name: 'Home',
  components: {
    NavBar,
  },
  beforeMount() {},
  data() {
    return {
      isLoading: false,
      hasResults: false,
      noOfDogBedsSold: null,
      showEditDataModal: false,
      averageDogBedWeight: '3.5',
      noOfLeatherCollarSold: null,
      noOfLeatherLeashesSold: null,
      selectedCompany: 'pets_at_home',
      showCompanyModal: false,
      csvFile: null,
      csvFileName: '',
      formErrors: {},
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
    selectCSV(e) {
      const file = e.target.files[0];
      this.csvFile = file;
      this.csvFileName = file.name;
    },
    toggleCompanyModal() {
      this.showCompanyModal = !this.showCompanyModal;
    },
    selectCompany(val) {
      this.selectedCompany = val;
      this.toggleCompanyModal();
    },
    determineSelectedCompany() {
      switch (this.selectedCompany) {
        case 'pets_at_home':
          return 'Pets at Home';
        default:
          return 'Pet co';
      }
    },
    showEditModal() {
      this.showEditDataModal = true;
    },
    hideEditModal() {
      this.showEditDataModal = false;
    },
    seen() {
      this.noOfDogBedsSold = 0;
      this.averageDogBedWeight = '3.5';
      this.noOfLeatherCollarSold = 0;
      this.noOfLeatherLeashesSold = 0;
      this.hasResults = false;
    },
    handleParsingForm() {
      const formErrors = {};
      if (!this.noOfDogBedsSold) {
        formErrors.noOfDogBedsSold = true;
        formErrors.noOfDogBedsSoldError = 'Please type in figures';
      }
      if (!this.noOfLeatherCollarSold) {
        formErrors.noOfLeatherCollarSold = true;
        formErrors.noOfLeatherCollarSoldError = 'Please type in figures';
      }
      if (!this.noOfLeatherLeashesSold) {
        formErrors.noOfLeatherLeashesSold = true;
        formErrors.noOfLeatherLeashesSoldError = 'Please type in figures';
      }

      const canProceed = Object.keys(formErrors).length;
      if (canProceed > 0) {
        this.formErrors = formErrors;
        return false;
      }
      this.formErrors = {};
      return true;
    },
    async processDataCSV() {
      try {
        const url = 'https://staging.bloverse.com/extraction/dog_details_csv';
        if (!this.csvFile) {
          return;
        }
        this.isLoading = true;
        const formData = new FormData();
        formData.append('csv_file', this.csvFile);
        const response = await this.axios.post(
          url,
          formData,
          {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          },
        );
        this.isLoading = false;
        if (response.status === 200) {
          // dog bed;
          const dogBed = response.data.data[0];
          this.dog_beds_made_from_virgin_polyester = dogBed.dog_beds_made_from_virgin_polyester;
          this.dog_beds_made_from_recycled_polyester = dogBed
            .dog_beds_made_from_recycled_polyester;
          this.total_saving = dogBed.total_saving;
          const collarLeash = response.data.data[1];
          this.collar_water_saving = collarLeash.collar_water_saving;
          this.leash_water_saving = collarLeash.leash_water_saving;
          this.recycled_leather_collar = collarLeash.recycled_leather_collar;
          this.recycled_leather_leash = collarLeash.recycled_leather_leash;
          this.traditional_leather_collar = collarLeash.traditional_leather_collar;
          this.traditional_leather_leash = collarLeash.traditional_leather_leash;
          this.hasResults = true;
          const co2PerSaving = response.data.data[2];
          this.co2_saving_per_item.recycled_leather_collar.co2_saved = co2PerSaving
            .recycled_leather_collar;
          this.co2_saving_per_item.recycled_leather_leash.co2_saved = co2PerSaving
            .recycled_leather_leash;
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
    async processData() {
      try {
        if (this.handleParsingForm()) {
          if (this.showEditDataModal) {
            this.showEditDataModal = false;
          }
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
          if (response.status === 200) {
            // dog bed;
            const dogBed = response.data.data[1];
            this.dog_beds_made_from_virgin_polyester = dogBed.dog_beds_made_from_virgin_polyester;
            this.dog_beds_made_from_recycled_polyester = dogBed
              .dog_beds_made_from_recycled_polyester;
            this.total_saving = dogBed.total_saving;
            const collarLeash = response.data.data[3];
            this.collar_water_saving = collarLeash.collar_water_saving;
            this.leash_water_saving = collarLeash.leash_water_saving;
            this.recycled_leather_collar = collarLeash.recycled_leather_collar;
            this.recycled_leather_leash = collarLeash.recycled_leather_leash;
            this.traditional_leather_collar = collarLeash.traditional_leather_collar;
            this.traditional_leather_leash = collarLeash.traditional_leather_leash;
            this.hasResults = true;
            const co2PerSaving = response.data.data[4];
            this.co2_saving_per_item.recycled_leather_collar.co2_saved = co2PerSaving
              .recycled_leather_collar;
            this.co2_saving_per_item.recycled_leather_leash.co2_saved = co2PerSaving
              .recycled_leather_leash;
          } else {
            this.isLoading = false;
            this.hasResults = false;
          }
        }
      } catch (err) {
        this.isLoading = false;
        this.hasResults = false;
        console.log(err);
      }
    },
    formatCurrency(number) {
      return new Intl.NumberFormat('en-US').format(number);
    },
  },
};
</script>
<style scoped>
 @import url('../styles/main.css');
</style>
