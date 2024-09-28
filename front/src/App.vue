<template>
  <div>
    <div class="hero">
      <h1>
        O'quv markazlari uchun fanlardan <span>avtomatlashtirilgan</span> onlayn
        kirish testi
      </h1>

      <!-- Buttons to open modal -->
      <div class="registration">
        <button @click="openRegistrationModal">Ro'yxatdan f vo'tish</button>
        <button class="kirish" @click="openLoginModal">Kirish</button>
      </div>
    </div>

    <!-- Single Modal Instance -->
    <div v-if="showModal">
      <FormModal :initialLoginForm="isLoginForm" @close="closeModal" />
    </div>
  </div>
</template>

<script>
import FormModal from "@/components/ModalForm.vue";

export default {
  components: { FormModal },
  data() {
    return {
      showModal: false, // To track if the modal is shown
      isLoginForm: false, // To track if it should open as login form
    };
  },
  methods: {
    openRegistrationModal() {
      this.isLoginForm = false; // Set to false to open registration form
      this.showModal = true; // Show modal
    },
    openLoginModal() {
      this.isLoginForm = true; // Set to true to open login form
      this.showModal = true; // Show modal
    },
    closeModal() {
      this.showModal = false; // Hide modal when closed
    },
  },
};
</script>

<style scoped>
.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  height: 100vh;
}
h1 {
  width: 80%;
  margin: 2rem auto;
  font-size: 50px;
  text-align: center;
  font-weight: 500;
  color: rgb(3, 69, 162);
}
h1 span {
  color: rgb(88, 143, 87);
}
button {
  background-color: rgb(13, 72, 153);
  color: #fff;
  font-size: 20px;
  padding: 0.7rem 1.5rem;
  width: fit-content;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}
.kirish {
  background: #fff;
  font-weight: 500;
  border: 3px solid rgb(13, 72, 153);
  color: rgb(13, 72, 153);
}
.registration {
  display: flex;
  justify-content: center;
  gap: 1rem;
}
</style>
