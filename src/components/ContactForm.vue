<template>
  <div>
    <h3 class="teal--text">New Contact</h3>
    <v-form @submit.prevent="handleSubmit">
      <v-text-field
        outlined
        label="First Name"
        v-model="form.firstName"
        :rules="validators.firstName"
      />
      <v-text-field
        outlined
        label="Last Name"
        v-model="form.lastName"
        :rules="validators.lastName"
      />
      <v-text-field
        type="number"
        outlined
        label="Phone"
        v-model="form.phone"
        :rules="validators.phone"
      />
      <v-select
        outlined
        label="Phone Type"
        :items="phoneTypeOptions"
        v-model="form.type"
      />
      <v-text-field
        outlined
        label="Email"
        v-model="form.email"
        :rules="validators.email"
      />
      <v-btn type="submit" color="teal" dark>Submit</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        firstName: "",
        lastName: "",
        phone: "",
        type: "",
        email: "",
      },
      phoneTypeOptions: ["Home", "Cell", "Office"],
      validators: {
        firstName: [
          (val) => !!val || "A first name is required",
          (val) =>
            val.length < 25 || "First name must be less than 25 characters",
        ],
        lastName: [
          (val) =>
            val.length < 25 || "Last name must be less than 25 characters",
        ],
        phone: [
          (val) => !!val || "Please include a phone number",
          (val) => val.length === 10,
        ],
        email: [(val) => val.includes("@")],
      },
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("contact-submit", this.form);
      this.form = {
        firstName: "",
        lastName: "",
        phone: "",
        type: "",
        email: "",
      };
    },
  },
};
</script>

<style></style>
