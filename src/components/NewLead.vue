<template>
  <div>
    <!-- Conditionally render the buttons -->
    <div v-if="!showForm" class="button-container">
      <Button label="Refresh" />
      <Button label="Create New Lead" @click="toggleForm" />
    </div>

    <!-- Conditionally render the form -->
    <div v-if="showForm" class="form-container">
      <!-- Back Button -->
      <div class="back-button-container">
        <Button label="Back" icon="pi pi-arrow-left" @click="toggleForm" />
      </div>

      <h1>Create New Lead</h1>

      <form @submit.prevent="onSubmit">
        <!-- Username -->
        <div class="form-group p-grid">
          <label for="username" class="p-col-12 p-md-4">
            Enter the name for your new Lead:
          </label>
          <div class="p-col-12 p-md-8">
            <InputText
              id="username"
              v-model="username"
              placeholder="Enter a name"
            />
            <span class="error">{{ errors.username }}</span>
          </div>
        </div>

        <!-- Email -->
        <div class="form-group p-grid">
          <label for="email" class="p-col-12 p-md-4">Enter the Email:</label>
          <div class="p-col-12 p-md-8">
            <InputText
              id="email"
              v-model="email"
              placeholder="Enter your email"
            />
            <span class="error">{{ errors.email }}</span>
          </div>
        </div>

        <!-- URL -->
        <div class="form-group full-width">
          <label for="url">Add URL's:</label>
          <div class="url-container">
            <InputText id="url" v-model="url" placeholder="Enter a URL" />
            <Button type="button" label="Add URL" @click="addUrl" />
          </div>
          <span class="error">{{ errors.url }}</span>

          <!-- Display added URLs as Chips -->
          <div class="chips-container">
            <Chip
              v-for="(addedUrl, index) in addedUrls"
              :key="index"
              :label="addedUrl"
              removable
              @remove="removeUrl(index)"
            />
          </div>
        </div>

        <!-- Submit Button -->
        <div class="form-actions">
          <Button label="Create New Lead" />
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useForm, useField } from "vee-validate";
import * as yup from "yup";
import Button from "primevue/button";
import InputText from "primevue/inputtext";
import Chip from "primevue/chip";

// Define validation schema
const schema = yup.object({
  username: yup.string().required("Username is required"),
  email: yup
    .string()
    .email("Enter a valid email")
    .required("Email is required"),
  url: yup
    .string()
    .matches(
      /^(https?:\/\/)?([\w\-]+\.)+[\w\-]{2,}(\/.*)?$/,
      "Enter a valid URL"
    )
    .required("URL is required"),
});

// Form state and validation
const { handleSubmit, resetForm, errors } = useForm({
  validationSchema: schema,
});

const { value: username } = useField("username");
const { value: email } = useField("email");
const { value: url } = useField("url");

// State for added URLs
const addedUrls = ref([]);

// Toggles the form visibility
const showForm = ref(false);
const toggleForm = () => {
  showForm.value = !showForm.value;
  if (!showForm.value) {
    // Clear the addedUrls array when closing the form
    addedUrls.value = [];
  }
};

// Adds the current URL to the list
const addUrl = async () => {
  try {
    // Validate the URL using the schema
    addedUrls.value.push(url.value); // Add the URL if valid
    url.value = ""; // Clear the input
  } catch (validationError) {
    // Show error message if validation fails
    errors.url = validationError.message;
  }
};

// Removes the URL from the list
const removeUrl = (index) => {
  addedUrls.value.splice(index, 1);
};

// Handles form submission
const onSubmit = (values) => {
  console.log("Form submitted with values:", values);
  resetForm();
  addedUrls.value = []; // Reset added URLs after form submission
  showForm.value = false;
};
</script>

<style>
.button-container {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
  padding: 10px;
}

.form-container {
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.form-group {
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
}

.full-width {
  display: flex;
  flex-direction: column;
}

.url-container {
  display: flex;
  align-items: center;
  gap: 10px;
}

.url-container input {
  flex-grow: 1;
}

.form-actions {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.error {
  color: red;
  font-size: 0.85rem;
}
</style>
