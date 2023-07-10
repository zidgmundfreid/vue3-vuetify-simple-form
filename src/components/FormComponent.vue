<template>
  <v-container>
    <v-form @submit.prevent="submit">
    <v-row
      ><v-col cols="12" md="12"
        ><h1 class="text-center">Voice Provisioning</h1></v-col
      ></v-row
    >
    <v-row
      ><v-col cols="12" md="12">
        <v-select 
          v-model="partners.value.value"
          :items="partnersArray"
          :error-messages="partners.errorMessage.value"
          label="Select a Parter"
        ></v-select></v-col
    ></v-row>

    <v-row
      ><v-col cols="12" md="12"
        ><v-text-field
          v-model="accountNumber.value.value"
          :counter="10"
          :error-messages="accountNumber.errorMessage.value"
          label="Account Number"
        ></v-text-field></v-col
    ></v-row>

    <v-row
      ><v-col cols="12" md="6">
        <v-text-field
          v-model="firstName.value.value"
          :counter="10"
          :error-messages="firstName.errorMessage.value"
          label="First Name"
        ></v-text-field></v-col
      ><v-col cols="12" md="6">
        <v-text-field
          v-model="lastName.value.value"
          :counter="10"
          :error-messages="lastName.errorMessage.value"
          label="Last Name"
        ></v-text-field></v-col
    ></v-row>

    <v-row
      ><v-col cols="12" md="3">
        <v-text-field
          v-model="address.value.value"
          :counter="20"
          :error-messages="address.errorMessage.value"
          label="Address"
        ></v-text-field></v-col
      ><v-col cols="12" md="3">
        <v-select
          v-model="cities.value.value"
          :items="citiesArray"
          :error-messages="cities.errorMessage.value"
          label="City"
        ></v-select></v-col
      ><v-col cols="12" md="3">
        <v-text-field
          v-model="state.value.value"
          :counter="20"
          :error-messages="state.errorMessage.value"
          label="State"
        ></v-text-field></v-col
      ><v-col cols="12" md="3">
        <v-text-field
          v-model="zip.value.value"
          :counter="10"
          :error-messages="zip.errorMessage.value"
          label="Zip"
        ></v-text-field></v-col
    ></v-row>

    <v-row
      ><v-col cols="12" md="6">
        <v-text-field
          v-model="customerPhone.value.value"
          :counter="9"
          :error-messages="customerPhone.errorMessage.value"
          label="Contact Phone"
        ></v-text-field></v-col
      ><v-col cols="12" md="6">
        <v-text-field
          v-model="email.value.value"
          :error-messages="email.errorMessage.value"
          label="Contact Email"
        ></v-text-field></v-col
    ></v-row>

    <v-row
      ><v-col cols="12" md="4">
        <v-select
          v-model="customerTypes.value.value"
          :items="customerTypesArray"
          :error-messages="customerTypes.errorMessage.value"
          label="Customer Type"
        ></v-select></v-col
      ><v-col cols="12" md="4">
        <v-text-field
          v-model="provisionPhone.value.value"
          :counter="9"
          :error-messages="provisionPhone.errorMessage.value"
          label="Phone Number to Provision"
        ></v-text-field></v-col
      ><v-col cols="12" md="4">
        <v-text-field
          v-model="sipPassword.value.value"
          :error-messages="sipPassword.errorMessage.value"
          label="Sip Password"
          counter="20"
                    type="password"
        ></v-text-field></v-col
    ></v-row>

    <v-row
      ><v-col cols="12" md="4">
        <v-select
          v-model="ported.value.value"
          :items="portedArray"
          :error-messages="ported.errorMessage.value"
          label="Ported"
        ></v-select></v-col
    ></v-row>

    <v-row
      ><v-col cols="12" md="4">
        <v-checkbox
          v-model="checkbox.value.value"
          :error-messages="checkbox.errorMessage.value"
          value="1"
          label="Bypass E911 Address Automation"
          type="checkbox"
        ></v-checkbox></v-col
      ><v-col cols="12" md="8">
        <v-alert variant="outlined" type="warning" prominent border="top">
          (By checking "Bypass E911 Address Automation" you agree to manualy add
          this phone number and address to Bandwidth)
        </v-alert></v-col
      ></v-row
    >

    <v-row
      ><v-col cols="12" md="4">
        <v-btn color="#271e77" class="me-4 text-white" type="submit">
          PROVISION
        </v-btn></v-col
      ></v-row
    >
    </v-form>
  </v-container>
</template>



<script setup >
import { ref } from "vue";
import { useField, useForm } from "vee-validate";

const { handleSubmit, handleReset } = useForm({
  validationSchema: {
    firstName(value) {
      if (value?.length >= 2 && value?.length <= 10) return true;

      return "First Name needs to be at least 2 characters and less than 10.";
    },
    lastName(value) {
      if (value?.length >= 2 && value?.length <= 10) return true;

      return "Last Name needs to be at least 2 characters and less than 10.";
    },
        address(value) {
      if (value?.length >= 2 && value?.length <= 20) return true;

      return "Last Name needs to be at least 2 characters and less than 20.";
    },
            state(value) {
      if (value?.length >= 2 && value?.length <= 20) return true;

      return "Last Name needs to be at least 2 characters and less than 20.";
    },
                zip(value) {
      if (value?.length >= 2 && value?.length <= 10) return true;

      return "Last Name needs to be at least 2 characters and less than 10.";
    },
    accountNumber(value) {
      if (value?.length >= 9 && /[0-9-]+/.test(value)) return true;

      return "Phone number needs to be at least 9 digits.";
    },
    customerPhone(value) {
      if (value?.length >= 9 && /[0-9-]+/.test(value)) return true;

      return "Phone number needs to be at least 9 digits.";
    },
        provisionPhone(value) {
      if (value?.length >= 9 && /[0-9-]+/.test(value)) return true;

      return "Phone number needs to be at least 9 digits.";
    },
                    sipPassword(value) {
      if (value?.length >= 2 && value?.length <= 20) return true;

      return "Last Name needs to be at least 2 characters and less than 10.";
    },
    email(value) {
      if (/^[a-z.-]+@[a-z.-]+\.[a-z]+$/i.test(value)) return true;

      return "Must be a valid e-mail.";
    },
    partners(value) {
      if (value) return true;

      return "Select an item.";
    },
        cities(value) {
      if (value) return true;

      return "Select an item.";
    },
            customerTypes(value) {
      if (value) return true;

      return "Select an item.";
    },
        ported(value) {
      if (value) return true;

      return "Select an item.";
    },
    checkbox(value) {
      if (value === "1") return true;

      return "Must be checked.";
    },
  },
});
const firstName = useField("firstName");
const lastName = useField("lastName");
const address = useField("address");
const state = useField("state");
const zip = useField("zip");
const accountNumber = useField("accountNumber");
const customerPhone = useField("customerPhone");
const provisionPhone = useField("provisionPhone");
const sipPassword = useField("sipPassword");
const email = useField("email");
const partners = useField("partners");
const cities = useField("cities");
const customerTypes = useField("customerTypes");
const ported = useField("ported");
const checkbox = useField("checkbox");

const partnersArray = ref(["Sprout 1", "Sprout 2", "Sprout 3", "Sprout 4"]);
const citiesArray = ref(["Odesa", "New-York", "London", "Kongo"]);
const customerTypesArray = ref(["Good", "Bad", "Normal", "Mad"]);
const portedArray = ref(["Ported 1", "Ported 2", "Ported 3", "Ported 4"]);

const submit = handleSubmit((values) => {
  alert(JSON.stringify(values, null, 2));
});
</script>

<style>

.v-field__overlay {
  background-color: #eef3f9 !important;
  opacity: 1 !important;
  border-radius: 5px !important;
  box-shadow: 0em 0.1em 0.1em rgba(0,0,0,0.3);
}

.v-field__outline {
display: none !important;
}

.v-btn__overlay {
  background-color: #271e77 !important;
}
</style>
