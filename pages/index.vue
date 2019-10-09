<template>
  <div class="container">
    <div class="b-row">
      <div class="b-col">
        <h3 class="text-center mb-4">GENEALOGY REFERENCE FORM</h3>
      </div>
    </div>
    <b-row>
      <b-col cols="3">
        <b-img class="img-placeholder img-thumbnail"></b-img>
        <image-uploader
            :preview="true"
            :className="['fileinput', { 'fileinput--loaded': hasImage }]"
            capture="environment"
            doNotResize="gif"
            :autoRotate="true"
            outputFormat="verbose"
            @input="setImage"
        >
          <label for="fileInput" slot="upload-label" id="img-upload-trigger" :class="{ uploaded: hasImage }">
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
          <b-form-group label="Current Address:">
            <b-form-input placeholder="Enter street address"></b-form-input>
            <b-form-input placeholder="Enter apt. #"></b-form-input>
            <b-form-input placeholder="Enter city"></b-form-input>
            <b-form-input placeholder="Enter state"></b-form-input>
            <b-form-input placeholder="Enter zip code"></b-form-input>
          </b-form-group>
          <b-form-group label="Current Phone Number:">
            <b-form-input type="tel" placeholder="+1 (555) 555-5555"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
      <b-col>
        <b-form>
          <b-form-group label="Father's Name:">
            <b-form-input placeholder="Enter father's name"></b-form-input>
          </b-form-group>
          <b-form-group label="Mother's Name:">
            <b-form-input placeholder="Enter mother's name"></b-form-input>
          </b-form-group>
          <b-form-group label="Date Of Birth:">
            <date-picker></date-picker>
          </b-form-group>
        </b-form>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">Education</h5>
        <div v-for="index in schoolCounter">
          <b-form inline>
            <label>School Name:</label>
            <b-input placeholder="Enter school name"></b-input>
            <label>Degree:</label>
            <b-input placeholder="Enter degree"></b-input>
            <label>Graduation Year</label>
            <b-input type="number" placeholder="Enter graduation year"></b-input>
          </b-form>
        </div>
        <b-button variant="secondary" class="mt-4" @click="schoolCounter++">Add School</b-button>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">Work History</h5>
        <div v-for="index in jobCounter">
          <b-form inline>
            <label>Title:</label>
            <b-input placeholder="Enter job title"></b-input>
            <label>Employer:</label>
            <b-input placeholder="Enter employer name"></b-input>
            <label>Years Employed</label>
            <b-input type="number" placeholder="Enter years of employment"></b-input>
          </b-form>
        </div>
        <b-button variant="secondary" class="mt-4" @click="jobCounter++">Add Job</b-button>
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
                jobCounter: 1
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
</style>
