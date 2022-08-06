<template>
  <div class="container">
    <BaseInputVue
      name="first_name"
      label="Name"
      v-model="firstName"
      :error="errors.firstName"
    />
    <BaseInputVue
      name="last_name"
      label="Last Name"
      v-model="lastName"
      :error="errors.lastName"
    />
    <BaseInputVue
      name="email"
      label="E-Mail"
      v-model="email"
      :lazy="true"
      :error="errors.email"
    />
    <BaseInputVue
      name="password"
      type="password"
      label="Password"
      v-model="password"
      :error="errors.password"
    />

    <button class="btn" @click="submit">Submit</button>
  </div>
</template>

<script setup>
import { useField, useForm } from "vee-validate";
import { object as yupObject, string as yupString } from "yup";

import BaseInputVue from "./BaseInput.vue";
import { validationMessages } from "./../utils/validation-messages.js";

const validationSchema = yupObject({
  firstName: yupString().min(5).required(),
  lastName: yupString().min(5).required(),
  email: yupString().email(validationMessages.email).required(),
  password: yupString().min(8).required(),
});

let { handleSubmit, errors } = useForm({ validationSchema });
let { value: firstName } = useField("firstName");
let { value: lastName } = useField("lastName");
let { value: email } = useField("email");
let { value: password } = useField("password");

const submit = handleSubmit((values) => console.log(values));
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  width: 500px;
  gap: 50px;
}
</style>
