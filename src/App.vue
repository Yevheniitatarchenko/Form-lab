<template>
  <div class="wrapper">
    <h1>Your first project</h1>
    <WizardForm />
    <BusinessForm />
  </div>
</template>

<script>
import BusinessForm from './components/BusinessForm.vue'
import WizardForm from './components/WizardForm.vue'

export default {
  name: 'app',
  components: {
    BusinessForm,
    WizardForm
  }
}
</script>

<style lang="scss">

h1 {
  color: #fff;
  text-align: center;
  font-size: 40px;
  line-height: 64px;
}

@media all and (max-width: 480px) {
  h1 {
    color: #fff;
    text-align: center;
    font-size: 34px;
    line-height: 40px;
  }
}

</style>
