<template>
  <div class="form_business">
    <form 
      class="my-form"
      @submit.prevent="submit"
    >
      <div class="container">
        <div 
          class="box-half name"
          :class="{'invalid': text.name}"
        >
          <label>Your company name</label>
          <input type="text" v-model="project.name" placeholder="Type text" />
          <span v-show="text.name" class="invalid-span">The company name field must be 19 or less</span>
        </div>

        <div 
          class="box-half people"
          :class="{'invalid':!maxNumber, 'invalid':required.people }"
        >
          <label>Number of people<sup>*</sup></label>
          <input type="text" v-model="project.people" placeholder="1-99" />
          <div class="errors">
            <span v-show="!maxNumber" class="invalid-span">Please enter number from 1 to 99</span><br>
            <span v-show="required.people" class="invalid-span">The company name field must </span>
          </div>
          
        </div>

        <div 
          class="box-full"
          :class="{'invalid': required.business_area}"
        >
          <label>Business area<sup>*</sup></label>
          <input type="text" v-model="project.business_area" placeholder="Design, Development, etc." />
          <span v-show="required.business_area" class="invalid-span">This field in required</span>
        </div>

        <div 
          class="box-full description"
          :class="{'invalid': required.description}"
        >
          <label>Description<sup>*</sup></label>
          <input type="text" v-model="project.description" placeholder="Type text" />
          <span v-show="required.description" class="invalid-span">Max length 50</span>
        </div>

        <div class="box-full file">
          <div class="box">
            <span class="button-box">
              <svg width="24" height="21" viewBox="0 0 24 21" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M11.7 3.725H21.6C22.9236 3.725 24 4.8026 24 6.125V18.125C24 19.4486 22.9236 20.525 21.6 20.525H2.4C1.0764 20.525 0 19.4486 0 18.125V2.525C0 1.2026 1.0764 0.125 2.4 0.125H7.8C8.5512 0.125 9.27 0.4838 9.72 1.085L11.7 3.725ZM2.4 2.525V18.125H21.6012L21.6 6.125H11.7C10.9488 6.125 10.23 5.7662 9.78 5.165L7.8 2.525H2.4ZM11.0571 8.35391H12.9428V11.1825H15.7714V13.0682H12.9428V15.8968H11.0571V13.0682H8.22851V11.1825H11.0571V8.35391Z" fill="#333333"/>
              </svg>
              Add file as attachment
            </span>
            <span>{{ quantityFiles }} files attached</span>
            <input 
              class="file-input"
              type="file"
              ref="fileInput"
              @change="file"
            >
          </div>
        </div>

        <button class="submit">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
let text = /^(([a-zA-Z]{15,}))$/;
export default {
  
  data() {
    return {
      project: {
        name: '',
        people: '',
        business_area: '',
        description: '',
        files: []
      },
    }
  },
  
  computed: {
    quantityFiles () {
      return this.project.files.length;
    },
    required() {
      return {
        people: this.project.people <= 0,
        business_area: this.project.business_area <= 0,
        description: this.project.description <= 0,
      }
    },
    text() {
      return { 
        name: text.test(this.project.name)
      }
    },
    maxNumber() {
      return this.project.people >= 0 && this.project.people <= 99;
    },
    maxSymbol() {
      return this.project.description.length >= 50;
    },
  },
  methods: {
    submit() {
      if (
        this.quantityFiles && 
        this.maxNumber && 
        !this.required.people && 
        !this.required.business_area && 
        !this.required.description && 
        !this.text.name) {
        console.log(this.project)
      }
    },
    file (event) {
      const file = {...event.target.files}
      this.project.files.push(file);
    }
  }
}
</script>

<style lang="scss" scoped>
.form_business {
  background: #FFFFFF;
  max-width: 608px;
  width: 100%;
  margin: 0 auto;
  border-radius: 8px;
  .my-form {
    padding: 56px 48px 55px 56px;
  }
}

.container {
  display: flex;
  flex-flow: row wrap;
  justify-content: space-between;
  .box-half {
    display: flex;
    flex-flow: column;
    input {
      padding: 8px 16px 8px 16px;
    }
  }
  .box-full {
    display: flex;
    flex-flow: column;
    max-width: 496px;
    width: 100%;
    margin-left: 8px;
  }
  .name {
    width: 55.6%;
  }
  .people {
    width: calc(44.4% - 46px);
    margin-right: 8px;
  }
  .description {
    margin-left: 0px;
    input {
      padding-bottom: 122px;
      margin-right: 0;
    }
  }
  .file {
    margin-left: 0px;
  }
}

.box {
  position: relative;
  display: flex;
  justify-content: space-between;
  border: 0.65015px solid #D6D6D6;
  border-radius: 10px;
  padding: 14px 24px 14px 24px;
  font-family: 'OpenSans-Regular';
  font-size: 14px;
  color: #A7A7A7;
  margin-bottom: 40px;
  .file-input {
    position: absolute;
    top: 0px;
    left: -55px;
    width: 97%;
    opacity: 0;
    cursor: pointer;
    z-index: 2;
  }
  .button-box {
    color: #333333;
    cursor: pointer;
    z-index: 1;
  }
  svg {
    margin: -2px 12px -4px 0px;
  }
}

.submit {
  background: #DA3F5B;
  border-radius: 8px;
  border: none;
  align-items: center;
  text-align: center;
  color: #FFFFFF;
  font-size: 16px;
  line-height: 22px;
  font-family: 'OpenSans-Bold';
  width: 144px;
  padding: 16px 0px 16px 0;
}

.invalid {
  input{
    border: 1px solid #F15557;
  }
}

.invalid-span {
  font-size: 12px;
  font-family: 'OpenSans-Regular';
  color: #F15557;
  line-height: 100%;
  margin-top: -33px;
  margin-bottom: 20px;
}

label {
  font-family: 'OpenSans-SemiBold';
  font-size: 14px;
  line-height: 100%;
  color: #636363;
  margin-bottom: 8px;
  display: flex;
  sup {
    color: #F15557;
    display: block;
    margin: -2px 0px 0px 3px;
  }
}

input {
  background: #F9F9F9;
  padding: 16px 8px 16px 16px;
  border-radius: 8px;
  border: none;
  font-family: 'OpenSans-Regular';
  font-size: 16px;
  line-height: 100%;
  color: #A7A7A7;
  margin-bottom: 40px;
  outline: none;
}

.errors {
  margin-top: -36px;
}

@media all and (max-width: 600px) {
  .container {
    .name {
      width: 100%!important;
    }
    .people {
      width: 100%!important;
      margin-right: 0!important;
    }
    .box-full {
      margin-left: 0!important;
    }
  }
}

@media all and (max-width: 480px) {
  h1 {
    font-size: 35px!important;
    line-height: 64px;
  }

  .form_business {
    .my-form {
      padding: 30px 30px 30px 30px;
    }
  } 

  input {
    font-size: 12px;
  }

  .form-wizard {
    ul {
      li {
        a {
          margin-right: 90px;
          &:before {
            width: 74px;
          }
        }
      }
    }
  }   

  .container {
    .name {
      width: 100%!important;
    }
    .people {
      width: 100%!important;
      margin-right: 0!important;
    }
  }

  .box {
    flex-direction: column;
    text-align: center;
  }

  button {
    margin: 0 auto;
  }
}

</style>
