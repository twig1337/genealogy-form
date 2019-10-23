<template>
  <div class="container">
    <div class="b-row">
      <div class="b-col">
        <h3 class="text-center mb-4">GENEALOGY REFERENCE FORM</h3>
      </div>
    </div>
    <b-row>
      <b-col cols="3">
        <b-img v-if="!hasImage" class="img-placeholder img-thumbnail h-90"></b-img>
        <image-uploader
            :preview="true"
            :className="['fileinput', { 'fileinput--loaded': hasImage }, 'd-print-none']"
            capture="environment"
            doNotResize="gif"
            :autoRotate="true"
            outputFormat="verbose"
            @input="setImage"
        >
          <label slot="upload-label" id="img-upload-trigger" :class="['d-print-none', { uploaded: hasImage }]">
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="32"
                height="32"
                viewBox="0 0 32 32"
            >
              <path
                  class="path1"
                  d="M9.5 19c0 3.59 2.91 6.5 6.5 6.5s6.5-2.91 6.5-6.5-2.91-6.5-6.5-6.5-6.5 2.91-6.5 6.5zM30 8h-7c-0.5-2-1-4-3-4h-8c-2 0-2.5 2-3 4h-7c-1.1 0-2 0.9-2 2v18c0 1.1 0.9 2 2 2h28c1.1 0 2-0.9 2-2v-18c0-1.1-0.9-2-2-2zM16 27.875c-4.902 0-8.875-3.973-8.875-8.875s3.973-8.875 8.875-8.875c4.902 0 8.875 3.973 8.875 8.875s-3.973 8.875-8.875 8.875zM30 14h-4v-2h4v2z"
              ></path>
            </svg>
            Upload an image
          </label>
        </image-uploader>
      </b-col>

      <b-col>
        <b-form inline class="mb-3 text-black-50" style="padding-left: 110px;">
          <label>Info From:</label>
          <b-form-input placeholder="Enter your name"></b-form-input>
          <label>Date:</label>
          <date-picker :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
        </b-form>
        <h5>Basic Information</h5>
        <b-form>
          <b-form-group label="Name:">
            <b-form-input placeholder="Enter name"></b-form-input>
          </b-form-group>
          <b-form-group label="Nickname:">
            <b-form-input placeholder="Enter nickname"></b-form-input>
          </b-form-group>
          <b-form-group label="Spouse Maiden Name:">
            <b-form-input placeholder="Enter spouse's maiden name"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
    </b-row>

    <b-row class="mt-4">
      <b-col>
        <b-form>
          <b-form-group label="Last Known Address:">
            <b-form-input placeholder="Enter street address"></b-form-input>
            <b-form-input placeholder="Enter apt. #"></b-form-input>
            <b-form-input placeholder="Enter city"></b-form-input>
            <b-form-input placeholder="Enter state"></b-form-input>
            <b-form-input placeholder="Enter zip code"></b-form-input>
          </b-form-group>
          <b-form-group label="Last Known Phone Number:">
            <b-form-input type="tel" placeholder="+1 (555) 555-5555"></b-form-input>
          </b-form-group>
          <b-form-group label="Religion:">
            <b-form-input placeholder="Enter religion"></b-form-input>
          </b-form-group>
          <b-form-group label="Occupation:">
            <b-form-input placeholder="Enter occupation"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
      <b-col style="border-left: 1px solid grey">
        <b-form>
          <b-form-group label="Father:">
            <b-form-input placeholder="Enter father's name"></b-form-input>
          </b-form-group>
          <b-form-group label="Mother:">
            <b-form-input placeholder="Enter mother's name"></b-form-input>
          </b-form-group>
          <b-form-group label="Date Of Birth:">
            <date-picker :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
          </b-form-group>
          <b-form-group label="Place of Birth:">
            <b-form-input placeholder="Enter street address"></b-form-input>
            <b-form-input placeholder="Enter apt. #"></b-form-input>
            <b-form-input placeholder="Enter city"></b-form-input>
            <b-form-input placeholder="Enter state"></b-form-input>
            <b-form-input placeholder="Enter zip code"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">Published:</h5>
        <b-form-textarea placeholder="Enter details..."></b-form-textarea>
      </b-col>
      <b-col>
        <h5 class="mt-4">Special Recognitions:</h5>
        <b-form-textarea placeholder="Enter details..."></b-form-textarea>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">
          Education
          <span class="text-grey">
            <span class="d-print-none" @click="schoolCounter++">+</span>
            <span class="d-print-none" @click="schoolCounter && schoolCounter--">-</span>
          </span>
        </h5>
        <div v-for="index in schoolCounter">
          <b-form :id="`${index}-school-form`" inline>
            <label>School Name:</label>
            <b-input placeholder="Enter school name"></b-input>
            <label>Degree:</label>
            <b-input placeholder="Enter degree"></b-input>
            <label>Graduation Year:</label>
            <b-input type="number" placeholder="Enter graduation year"></b-input>
          </b-form>
        </div>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">
          Work History
          <span class="text-grey">
            <span class="d-print-none" @click="jobCounter++">+</span>
            <span class="d-print-none" @click="jobCounter && jobCounter--">-</span>
          </span>
        </h5>
        <div v-for="index in jobCounter">
          <b-form :id="`${index}-job-form`" inline>
            <label>Title:</label>
            <b-input placeholder="Enter job title"></b-input>
            <label>Employer:</label>
            <b-input placeholder="Enter employer name"></b-input>
            <label>Years Employed:</label>
            <b-input type="number" placeholder="Enter years of employment"></b-input>
          </b-form>
        </div>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">
          Military Service
          <span class="text-grey">
            <span class="d-print-none" @click="militaryCounter++">+</span>
            <span class="d-print-none" @click="militaryCounter && militaryCounter--">-</span>
          </span>
        </h5>
        <div v-for="index in militaryCounter">
          <b-form :id="`${index}-military-form`" inline>
            <label>Branch:</label>
            <b-input placeholder="Enter branch:"></b-input>
            <label>Years:</label>
            <b-input type="number" placeholder="Enter years served"></b-input>
            (from:
            <date-picker :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
            to:
            <date-picker :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
            )
          </b-form>
        </div>
      </b-col>
    </b-row>
    <b-row class="mt-4">
      <b-col>
        <b-form>
          <label>
            Military Awards:
            <span class="text-grey">
              <span class="d-print-none" @click="militaryAwards++">+</span>
              <span class="d-print-none" @click="militaryAwards && militaryAwards--">-</span>
            </span>
          </label>
          <b-form-group>
            <div v-for="index in militaryAwards">
              <b-form-input :id="`${index}-maward-form`" placeholder="Enter award"></b-form-input>
            </div>
          </b-form-group>
          <b-form-group label="Highest Rank:">
            <b-form-input placeholder="Enter rank"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
      <b-col style="border-left: 1px solid grey">
        <b-form>
          <label>
            Combat Tours:
            <span class="text-grey">
              <span class="d-print-none" @click="combatTours++">+</span>
              <span class="d-print-none" @click="combatTours && combatTours--">-</span>
            </span>
          </label>
          <b-form-group>
            <div v-for="index in combatTours">
              <b-form-input :id="`${index}-combat-tour-form`" placeholder="Enter tour"></b-form-input>
            </div>
          </b-form-group>
        </b-form>
        <b-form>
          <label>
            Military Recognitions or Tabs:
            <span class="text-grey">
              <span class="d-print-none" @click="mtabs++">+</span>
              <span class="d-print-none" @click="mtabs && mtabs--">-</span>
            </span>
          </label>
          <b-form-group>
            <div v-for="index in mtabs">
              <b-form-input :id="`${index}-mtabs-form`" placeholder="Enter recognition"></b-form-input>
            </div>
          </b-form-group>
        </b-form>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">Medical Challenges:</h5>
        <b-form-textarea placeholder="Enter details..."></b-form-textarea>
      </b-col>
    </b-row>

    <b-row>
      <b-col><h5 class="mt-4">Favorites</h5></b-col>\
    </b-row>

    <b-row>
      <b-col>
        <b-form>
          <b-form-group label="Color:">
            <b-form-input placeholder="Enter color"></b-form-input>
          </b-form-group>
          <b-form-group label="Food:">
            <b-form-input placeholder="Enter food"></b-form-input>
          </b-form-group>
          <b-form-group label="Place:">
            <b-form-input placeholder="Enter place"></b-form-input>
          </b-form-group>
          <b-form-group label="President:">
            <b-form-input placeholder="Enter president"></b-form-input>
          </b-form-group>
          <b-form-group label="School Subject:">
            <b-form-input placeholder="Enter subject"></b-form-input>
          </b-form-group>
          <b-form-group label="TV Show:">
            <b-form-input placeholder="Enter show"></b-form-input>
          </b-form-group>
          <b-form-group label="Place to Visit:">
            <b-form-input placeholder="Enter place"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
      <b-col style="border-left: 1px solid grey">
        <b-form-group label="Animal:">
          <b-form-input placeholder="Enter animal"></b-form-input>
        </b-form-group>
        <b-form-group label="Hobby:">
          <b-form-input placeholder="Enter hobby"></b-form-input>
        </b-form-group>
        <b-form-group label="Firearm:">
          <b-form-input placeholder="Enter firearm"></b-form-input>
        </b-form-group>
        <b-form-group label="Instrument:">
          <b-form-input placeholder="Enter instrument"></b-form-input>
        </b-form-group>
        <b-form-group label="Musical Group:">
          <b-form-input placeholder="Enter group"></b-form-input>
        </b-form-group>
        <b-form-group label="Book:">
          <b-form-input placeholder="Enter book"></b-form-input>
        </b-form-group>
        <b-form-group label="Most proud of:">
          <b-form-input placeholder="Enter item of pride"></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>

    <b-row>
      <b-col><h5 class="mt-4">Least Favorites</h5></b-col>
    </b-row>

    <b-row>
      <b-col>
        <b-form-group label="Politician:">
          <b-form-input placeholder="Enter politician"></b-form-input>
        </b-form-group>
        <b-form-group label="Food:">
          <b-form-input placeholder="Enter food"></b-form-input>
        </b-form-group>
      </b-col>
      <b-col style="border-left: 1px solid grey">
        <b-form>
          <b-form-group label="Thing to do:">
            <b-form-input placeholder="Enter activity"></b-form-input>
          </b-form-group>
          <b-form-group label="Worst Bad Habit:">
            <b-form-input placeholder="Enter habit"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
    </b-row>

    <b-row>
      <b-col>
        <h5 class="mt-4">Personal Narrative:</h5>
        <small class="text-grey d-print-none">What you want others to remember about you or other facts</small>
        <b-form-textarea placeholder="Enter details..."></b-form-textarea>
      </b-col>
    </b-row>
  </div>
</template>

<script>

    // Import required dependencies
    import 'bootstrap/dist/css/bootstrap.css';
    // Import date picker css
    import 'pc-bootstrap4-datetimepicker/build/css/bootstrap-datetimepicker.css';

    import DatePicker from "vue-bootstrap-datetimepicker/src/component";

    export default {
        components: {DatePicker},
        data() {
            return {
                hasImage: false,
                image: null,
                schoolCounter: 1,
                jobCounter: 1,
                militaryCounter: 1,
                militaryAwards: 1,
                combatTours: 1,
                mtabs: 1
            };
        },
        methods: {
            setImage: function () {
                this.hasImage = true;
            }
        }
    };
</script>

<style>
  input {
    border-top: none !important;
    border-right: none !important;
    border-left: none !important;
    border-radius: 0 !important;
  }

  #fileInput {
    display: none;
  }

  #img-upload-trigger {
    cursor: pointer;
  }

  #img-upload-trigger.uploaded {
    cursor: pointer;
    position: absolute;

    top: -30px;
    left: -30px;
  }

  #img-upload-trigger.uploaded svg {
    fill: lightgrey;
  }

  .container {
    padding: 96px;
  }

  @media print {
    .container {
      padding: 0;

    }
  }

  .img-preview {
    padding: 0.25rem;
    background-color: #fff;
    border: 1px solid #dee2e6;
    border-radius: 0.25rem;
    max-width: 100%;
    height: auto;
  }

  .img-placeholder {
    min-height: 200px;
    min-width: 200px;
  }

  .h-90 {
    height: 90% !important;
  }

  .text-grey {
    color: grey;
  }
</style>
