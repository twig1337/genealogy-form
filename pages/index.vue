<template>
  <!-- Form-->
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
            ref="imageUploader"
            :preview="true"
            :className="['fileinput', { 'fileinput--loaded': hasImage }, 'd-print-none']"
            capture="environment"
            doNotResize="gif"
            :autoRotate="true"
            outputFormat="verbose"
            @input="setImage"
        >
          <label for="fileInput" slot="upload-label" id="img-upload-trigger"
                 :class="['d-print-none', { uploaded: hasImage }]">
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
            Choose
            <span v-if="hasImage">a different</span>
            <span v-else>an</span>
            image
          </label>
        </image-uploader>
      </b-col>

      <b-col>
        <b-form inline class="mb-3 text-black-50" style="padding-left: 110px;">
          <label>Info From:</label>
          <b-form-input v-model="inputData.author.name" placeholder="Enter your name"></b-form-input>
          <label>Date:</label>
          <date-picker :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY"
                       v-model="inputData.author.date" value=""></date-picker>
        </b-form>
        <h5>Basic Information</h5>
        <b-form>
          <b-form-group label="Name:">
            <b-form-input v-model="inputData.name" placeholder="Enter name"></b-form-input>
          </b-form-group>
          <b-form-group label="Nickname:">
            <b-form-input v-model="inputData.nickname" placeholder="Enter nickname"></b-form-input>
          </b-form-group>
          <b-form-group label="Spouse Maiden Name:">
            <b-form-input v-model="inputData.spouseName" placeholder="Enter spouse's maiden name"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
    </b-row>

    <b-row class="mt-4">
      <b-col>
        <b-form>
          <b-form-group label="Last Known Address:">
            <b-form-input v-model="inputData.address.street" placeholder="Enter street address"></b-form-input>
            <b-form-input v-model="inputData.address.apt" placeholder="Enter apt. #"></b-form-input>
            <b-form-input v-model="inputData.address.city" placeholder="Enter city"></b-form-input>
            <b-form-input v-model="inputData.address.state" placeholder="Enter state"></b-form-input>
            <b-form-input v-model="inputData.address.zip" placeholder="Enter zip code"></b-form-input>
          </b-form-group>
          <b-form-group label="Last Known Phone Number:">
            <b-form-input v-model="inputData.phone" type="tel" placeholder="+1 (555) 555-5555"></b-form-input>
          </b-form-group>
          <b-form-group label="Religion:">
            <b-form-input v-model="inputData.religion" placeholder="Enter religion"></b-form-input>
          </b-form-group>
          <b-form-group label="Occupation:">
            <b-form-input v-model="inputData.occupation" placeholder="Enter occupation"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
      <b-col style="border-left: 1px solid grey">
        <b-form>
          <b-form-group label="Father:">
            <b-form-input v-model="inputData.father" placeholder="Enter father's name"></b-form-input>
          </b-form-group>
          <b-form-group label="Mother:">
            <b-form-input v-model="inputData.mother" placeholder="Enter mother's name"></b-form-input>
          </b-form-group>
        </b-form>
        <b-form-group label="Birth:">
          <b-form inline>
            <label>Date:</label>
            <date-picker v-model="inputData.birth.date" :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
            <label>City:</label>
            <b-form-input v-model="inputData.birth.city" placeholder="Enter city"></b-form-input>
            <label>State:</label>
            <b-form-input v-model="inputData.birth.state" placeholder="Enter state"></b-form-input>
          </b-form>
        </b-form-group>
        <b-form-group label="Death:">
          <b-form inline class="condensed-inputs">
            <label>Date:</label>
            <date-picker v-model="inputData.death.date" :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
            <label>City:</label>
            <b-form-input v-model="inputData.death.city" placeholder="Enter city"></b-form-input>
          </b-form>
          <b-form inline>
            <label>State:</label>
            <b-form-input v-model="inputData.death.state" placeholder="Enter state"></b-form-input>
          </b-form>
        </b-form-group>
        <b-form-group label="Buried:">
          <b-form inline class="condensed-inputs">
            <label>Date:</label>
            <date-picker v-model="inputData.burial.date" :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
            <label>Cemetery:</label>
            <b-form-input v-model="inputData.burial.cemetery" placeholder="Enter cemetery"></b-form-input>
            <label>City:</label>
            <b-form-input v-model="inputData.burial.city" placeholder="Enter city"></b-form-input>
            <label>State:</label>
            <b-form-input v-model="inputData.burial.state" placeholder="Enter state"></b-form-input>
          </b-form>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">Published:</h5>
        <b-form-textarea v-model="inputData.published" placeholder="Enter details..."></b-form-textarea>
      </b-col>
      <b-col>
        <h5 class="mt-4">Special Recognitions:</h5>
        <b-form-textarea v-model="inputData.special" placeholder="Enter details..."></b-form-textarea>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">
          Education
          <span class="text-grey">
            <span class="d-print-none pointer" @click="inputData.schools.push({})">+</span>
            <span class="d-print-none pointer" @click="inputData.schools.pop()">-</span>
          </span>
        </h5>
        <div v-for="index in inputData.schools.length">
          <b-form :id="`${index}-school-form`" inline>
            <label>School Name:</label>
            <b-input v-model="inputData.schools[index - 1].name" placeholder="Enter school name"></b-input>
            <label>Degree:</label>
            <b-input v-model="inputData.schools[index - 1].degree" placeholder="Enter degree"></b-input>
            <label>Graduation Year:</label>
            <b-input v-model="inputData.schools[index - 1].graduation" type="number" placeholder="Enter graduation year"></b-input>
          </b-form>
        </div>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">
          Work History
          <span class="text-grey">
            <span class="d-print-none pointer" @click="inputData.jobs.push({})">+</span>
            <span class="d-print-none pointer" @click="inputData.jobs.pop()">-</span>
          </span>
        </h5>
        <div v-for="index in inputData.jobs.length">
          <b-form :id="`${index}-job-form`" inline>
            <label>Title:</label>
            <b-input v-model="inputData.jobs[index - 1].title" placeholder="Enter job title"></b-input>
            <label>Employer:</label>
            <b-input v-model="inputData.jobs[index - 1].employer" placeholder="Enter employer name"></b-input>
            <label>Years Employed:</label>
            <b-input v-model="inputData.jobs[index - 1].years" type="number" placeholder="Enter years of employment"></b-input>
          </b-form>
        </div>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">
          Military Service
          <span class="text-grey">
            <span class="d-print-none pointer" @click="inputData.militaryService.push({})">+</span>
            <span class="d-print-none pointer" @click="inputData.militaryService.pop()">-</span>
          </span>
        </h5>
        <div v-for="index in inputData.militaryService.length">
          <b-form :id="`${index}-military-form`" inline>
            <label>Branch:</label>
            <b-input v-model="inputData.militaryService[index - 1].branch" placeholder="Enter branch:"></b-input>
            <label>Years:</label>
            <b-input v-model="inputData.militaryService[index - 1].years" type="number" placeholder="Enter years served"></b-input>
            From:
            <date-picker v-model="inputData.militaryService[index - 1].from" :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
            To:
            <date-picker v-model="inputData.militaryService[index - 1].to" :config="{format:'MM/DD/YYYY'}" placeholder="MM/DD/YYYY" value=""></date-picker>
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
              <span class="d-print-none pointer" @click="inputData.militaryAwards.push({})">+</span>
              <span class="d-print-none pointer" @click="inputData.militaryAwards.pop()">-</span>
            </span>
          </label>
          <b-form-group>
            <div v-for="index in inputData.militaryAwards.length">
              <b-form-input v-model="inputData.militaryAwards[index - 1].award" :id="`${index}-maward-form`" placeholder="Enter award"></b-form-input>
            </div>
          </b-form-group>
          <b-form-group label="Highest Rank:">
            <b-form-input v-model="inputData.military.rank" placeholder="Enter rank"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
      <b-col style="border-left: 1px solid grey">
        <b-form>
          <label>
            Combat Tours:
            <span class="text-grey">
              <span class="d-print-none pointer" @click="inputData.combatTours.push({})">+</span>
            <span class="d-print-none pointer" @click="inputData.combatTours.pop()">-</span>
            </span>
          </label>
          <b-form-group>
            <div v-for="index in inputData.combatTours.length">
              <b-form-input v-model="inputData.combatTours[index - 1].tour" :id="`${index}-combat-tour-form`" placeholder="Enter tour"></b-form-input>
            </div>
          </b-form-group>
        </b-form>
        <b-form>
          <label>
            Military Recognitions or Tabs:
            <span class="text-grey">
              <span class="d-print-none pointer" @click="inputData.militaryTabs.push({})">+</span>
            <span class="d-print-none pointer" @click="inputData.militaryTabs.pop()">-</span>
            </span>
          </label>
          <b-form-group>
            <div v-for="index in inputData.militaryTabs.length">
              <b-form-input v-model="inputData.militaryTabs[index - 1].tab" :id="`${index}-mtabs-form`" placeholder="Enter recognition"></b-form-input>
            </div>
          </b-form-group>
        </b-form>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5 class="mt-4">Medical Challenges:</h5>
        <b-form-textarea v-model="inputData.medical" placeholder="Enter details..."></b-form-textarea>
      </b-col>
    </b-row>

    <b-row>
      <b-col><h5 class="mt-4">Favorites</h5></b-col>
    </b-row>

    <b-row>
      <b-col>
        <b-form>
          <b-form-group label="Color:">
            <b-form-input v-model="inputData.color" placeholder="Enter color"></b-form-input>
          </b-form-group>
          <b-form-group label="Food:">
            <b-form-input v-model="inputData.food" placeholder="Enter food"></b-form-input>
          </b-form-group>
          <b-form-group label="Place:">
            <b-form-input v-model="inputData.place" placeholder="Enter place"></b-form-input>
          </b-form-group>
          <b-form-group label="President:">
            <b-form-input v-model="inputData.president" placeholder="Enter president"></b-form-input>
          </b-form-group>
          <b-form-group label="School Subject:">
            <b-form-input v-model="inputData.subject" placeholder="Enter subject"></b-form-input>
          </b-form-group>
          <b-form-group label="TV Show:">
            <b-form-input v-model="inputData.tv" placeholder="Enter show"></b-form-input>
          </b-form-group>
          <b-form-group label="Place to Visit:">
            <b-form-input v-model="inputData.visit" placeholder="Enter place"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
      <b-col style="border-left: 1px solid grey">
        <b-form-group label="Animal:">
          <b-form-input v-model="inputData.animal" placeholder="Enter animal"></b-form-input>
        </b-form-group>
        <b-form-group label="Hobby:">
          <b-form-input v-model="inputData.hobby" placeholder="Enter hobby"></b-form-input>
        </b-form-group>
        <b-form-group label="Firearm:">
          <b-form-input v-model="inputData.firearm" placeholder="Enter firearm"></b-form-input>
        </b-form-group>
        <b-form-group label="Instrument:">
          <b-form-input v-model="inputData.instrument" placeholder="Enter instrument"></b-form-input>
        </b-form-group>
        <b-form-group label="Musical Group:">
          <b-form-input v-model="inputData.band" placeholder="Enter group"></b-form-input>
        </b-form-group>
        <b-form-group label="Book:">
          <b-form-input v-model="inputData.book" placeholder="Enter book"></b-form-input>
        </b-form-group>
        <b-form-group label="Most proud of:">
          <b-form-input v-model="inputData.pride" placeholder="Enter item of pride"></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>

    <b-row>
      <b-col><h5 class="mt-4">Least Favorites</h5></b-col>
    </b-row>

    <b-row>
      <b-col>
        <b-form-group label="Politician:">
          <b-form-input v-model="inputData.leastPolitician" placeholder="Enter politician"></b-form-input>
        </b-form-group>
        <b-form-group label="Food:">
          <b-form-input v-model="inputData.leastFood" placeholder="Enter food"></b-form-input>
        </b-form-group>
      </b-col>
      <b-col style="border-left: 1px solid grey">
        <b-form>
          <b-form-group label="Thing to do:">
            <b-form-input v-model="inputData.leastThing" placeholder="Enter activity"></b-form-input>
          </b-form-group>
          <b-form-group label="Worst Bad Habit:">
            <b-form-input v-model="inputData.leastHabit" placeholder="Enter habit"></b-form-input>
          </b-form-group>
        </b-form>
      </b-col>
    </b-row>

    <b-row>
      <b-col>
        <h5 class="mt-4">Personal Narrative:</h5>
        <small class="text-grey d-print-none">What you want others to remember about you or other facts</small>
        <b-form-textarea v-model="inputData.narrative" placeholder="Enter details..."></b-form-textarea>
      </b-col>
    </b-row>

    <!-- Import / Export -->
    <div id="io-wrapper">
      <b-button variant="outline-primary" class="d-print-none" v-b-modal.import>Import</b-button>
      <b-button variant="outline-primary" class="d-print-none" @click="exportData">Export</b-button>
    </div>

    <b-modal id="import" title="Import Data" class="d-print-none">
      <b-alert variant="danger" show="true">
        <strong>Warning!</strong><br>Importing a saved file will erase all current values!
      </b-alert>
      <b-form-file v-model="uploadFile" @input="() => {importData(); this.$bvModal.hide('import')}"></b-form-file>
    </b-modal>
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
                uploadFile: null,
                inputData: {
                    author: {},
                    address: {},
                    birth: {},
                    death: {},
                    burial: {},
                    military: {},
                    schools: [{}],
                    jobs: [{}],
                    militaryService: [{}],
                    militaryAwards: [{}],
                    combatTours: [{}],
                    militaryTabs: [{}],
                }
            };
        },
        methods: {
            setImage: function (file) {
                this.hasImage = true;
                this.inputData.image = file;
            },
            importData: function () {
                let reader = new FileReader();
                reader.onloadend = () => {
                    console.log(this.inputData = JSON.parse(reader.result));
                    this.$refs.imageUploader.handleFile(this.convert(this.inputData.image.dataUrl));
                };

                reader.readAsBinaryString(this.uploadFile);
            },
            exportData: function () {
                if (!this.inputData.name) {
                    return alert('Please fill in the "Basic Information -> Name" field.');
                }

                let a = document.createElement("a");
                a.href = URL.createObjectURL(new Blob([JSON.stringify(this.inputData)], {type: 'text/json'}));
                a.download = this.inputData.name + '.json';
                a.click();
            },
            convert: function dataURItoBlob(dataURI) {
                // convert base64 to raw binary data held in a string
                // doesn't handle URLEncoded DataURIs - see SO answer #6850276 for code that does this
                var byteString = atob(dataURI.split(',')[1]);

                // separate out the mime component
                var mimeString = dataURI.split(',')[0].split(':')[1].split(';')[0];

                // write the bytes of the string to an ArrayBuffer
                var ab = new ArrayBuffer(byteString.length);
                var ia = new Uint8Array(ab);
                for (var i = 0; i < byteString.length; i++) {
                    ia[i] = byteString.charCodeAt(i);
                }

                return new Blob([ab], {type: mimeString});
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

  #io-wrapper {
    position: fixed;
    right: 0;
    top: 0;
    margin: 15px;
  }

  .container {
    padding: 96px;
  }

  @media print {
    .container {
      padding: 0;

    }
  }

  .condensed-inputs input {
    max-width: 170px;
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

  .pointer {
    cursor: pointer;
  }

  .text-grey {
    color: grey;
  }
</style>
