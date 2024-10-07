<template>
    <div class="card" role="group" aria-label="contact">
      <h1 id="contact">Contact Us</h1>
      <form @submit.prevent="handleSubmit" novalidate>
        <div>
          <label for="name">Name:</label>
          <input
            type="text"
            id="name"
            v-model="formData.name"
            @input="validateField('name')"
            :aria-invalid="errors.name ? 'true' : 'false'"
            aria-required="true"
            aria-describedby="nameError"
          />
          <span class="error" id="nameError" v-if="errors.name">{{ errors.name }}</span>
        </div>
        <div>
          <label for="email">Email:</label>
          <input
            type="email"
            id="email"
            v-model="formData.email"
            @input="validateField('email')"
            :aria-invalid="errors.email ? 'true' : 'false'"
            aria-required="true"
            aria-describedby="emailError"
          />
          <span class="error" id="emailError" v-if="errors.email">{{ errors.email }}</span>
        </div>
        <div>
        <label for="phone">Phone:</label>
        <input
            type="text"
            id="phone"
            v-model="formData.phone"
            @input="validateField('phone')"
            :aria-invalid="errors.phone ? 'true' : 'false'"
            aria-required="true"
            aria-describedby="phoneError"
        />
        <span class="error" id="phoneError" v-if="errors.phone">{{ errors.phone }}</span>
        </div>

        <div>
          <label for="message">Message:</label>
          <textarea
            id="message"
            v-model="formData.message"
            @input="validateField('message')"
            :aria-invalid="errors.message ? 'true' : 'false'"
            aria-required="true"
            aria-describedby="messageError"
          ></textarea>
          <span class="error" id="messageError" v-if="errors.message">{{ errors.message }}</span>
        </div>
        <button type="submit">Submit</button>
        <button type="reset" @click="resetForm">Reset</button>
      </form>
    </div>
  </template>
  
  <script>
import { ref } from 'vue';

export default {
  setup() {
    const formData = ref({
      name: '',
      email: '',
      phone: '',
      message: '',
    });
    
    const errors = ref({
      name: null,
      email: null,
      phone: null,
      message: null,
    });

    const validateField = (field) => {
      if (formData.value[field].trim() === '') {
        errors.value[field] = `Please enter your ${field}.`;
      } else if (field === 'email' && !isValidEmail(formData.value.email)) {
        errors.value[field] = 'Please enter a valid email.';
      } else if (field === 'phone' && !isValidPhone(formData.value.phone)) {
        errors.value[field] = 'Please enter a valid phone number.';
      } else {
        errors.value[field] = null;
      }
    };

    const isValidEmail = (email) => {
      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return emailPattern.test(email);
    };

    const isValidPhone = (phone) => {
      const phonePattern = /^\+?[1-9]\d{0,2}[ -]?\(?\d{1,4}?\)?[ -]?\d{1,4}[ -]?\d{1,4}[ -]?\d{1,9}$/;
      return phonePattern.test(phone);
    };

    const handleSubmit = () => {
      Object.keys(errors.value).forEach((field) => {
        validateField(field);
      });

      if (!Object.values(errors.value).some((error) => error)) {
        alert('Form submitted successfully!'); // Replace this with your form submission logic
        resetForm();
      } else {
        const firstInvalidField = Object.keys(errors.value).find((field) => errors.value[field]);
        document.getElementById(firstInvalidField).focus();
      }
    };

    const resetForm = () => {
      formData.value = { name: '', email: '', phone: '', message: '' };
      errors.value = { name: null, email: null, phone: null, message: null };
      alert('Form reset successfully!')
    };

    return {
      formData,
      errors,
      validateField,
      handleSubmit,
      resetForm,
    };
  },
};
</script>

  
  <style scoped>
  body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  
  .card {
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    padding: 20px;
    width: 100%;
    max-width: 100%; /* Set max width for larger screens */
    box-sizing: border-box; /* Include padding in width */
  }
  
  h1 {
    font-size: 1.5em;
    margin-bottom: 20px;
    text-align: center;
  }
  
  div {
    margin-bottom: 15px;
  }
  
  label {
    margin-bottom: 5px;
    display: block;
  }
  
  input,
  textarea {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box; /* Include padding in width */
  }
  
  input:focus,
  textarea:focus {
    border-color: #007BFF;
    outline: none;
  }
  
  .error {
    color: red;
    font-size: 0.9em;
  }
  
  button {
    background-color: #007BFF;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 4px;
    cursor: pointer;
    width: 100%;
    margin-bottom: 10px; /* Space between buttons */
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  .reset-button {
    margin-top: 10px; /* Space above the reset button */
  }
  </style>
  