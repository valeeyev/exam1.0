<template>
  <div class="modal-backdrop" @click="closeOnBackdropClick">
    <div class="form-modal" @click.stop>
      <button class="close-button" @click="closeModal">✕</button>

      <h1 class="title">
        {{ isLoginForm ? "Kirish" : "Ro'yxatdan o'tish" }}
      </h1>

      <!-- Registration Form -->
      <form
        v-if="!isLoginForm"
        class="registration"
        @submit.prevent="submitStudentForm"
      >
        <div class="pair">
          <label for="name">Ism</label>
          <input required name="name" type="text" placeholder="Talaba ismi" />
        </div>
        <div class="pair">
          <label for="surname">Familiya</label>
          <input
            required
            name="surname"
            type="text"
            placeholder="Talaba familiyasi"
          />
        </div>
        <div class="pair">
          <label for="telnumber">Telefon raqami</label>
          <input type="tel" required placeholder="+998" />
        </div>
        <div class="pair">
          <label for="level">Bilim darajasi</label>
          <select required v-model="selectedLevel">
            <option value="" disabled selected>Darajani tanlang</option>
            <option
              v-for="level in levels"
              :key="level.value"
              :value="level.value"
            >
              {{ level.label }}
            </option>
          </select>
        </div>
        <button type="submit" class="register">Ro'yxatdan o'tish</button>
      </form>

      <!-- Login Form -->
      <form v-else class="login" @submit.prevent="submitLoginForm">
        <div class="pair">
          <label for="email">Elektron pochta</label>
          <input
            name="email"
            required
            type="email"
            placeholder="example@email.com"
          />
        </div>
        <div class="pair">
          <label for="password">Parolni kiriting</label>
          <input
            type="password"
            name="parol"
            required
            placeholder="Kirish parolini kiriting"
          />
        </div>
        <button class="kirish" type="submit">Kirish</button>
      </form>

      <button type="button" class="toggled" @click="toggleForm">
        {{ isLoginForm ? "Ro'yxatdan o'tish" : "Kirish" }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    initialLoginForm: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      isLoginForm: this.initialLoginForm,
      selectedLevel: "", // Store selected level
      // Array of levels
      levels: [
        { value: "beginner", label: "Beginner" },
        { value: "elementary", label: "Elementary" },
        { value: "intermediate", label: "Intermediate" },
        { value: "ielts", label: "IELTS" },
      ],
    };
  },
  methods: {
    toggleForm() {
      this.isLoginForm = !this.isLoginForm;
    },
    submitStudentForm() {
      alert(
        `Talaba muvaffaqiyatli ro'yxatdan o'tdi! Daraja: ${this.selectedLevel}`
      );
      this.closeModal(); // Close the modal after submission
    },
    submitLoginForm() {
      alert("Kirish muvaffaqiyatli amalga oshirildi!");
      this.closeModal(); // Close the modal after login
    },
    closeModal() {
      this.$emit("close"); // Emit close event to parent
    },
    closeOnBackdropClick(event) {
      if (event.target === event.currentTarget) {
        this.closeModal();
      }
    },
  },
};
</script>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(3px);
  display: flex;
  justify-content: center;
  align-items: center;
}
.form-modal {
  position: relative;
  background-color: #fff;
  padding: 40px 20px;
  border-radius: 8px;
  transition: all ease 0.3s;
  min-width: 400px;
  max-width: 500px;
  margin: 0 auto;
}
.pair {
  display: flex;
  flex-direction: column;
  margin-bottom: 1rem;
  width: 100%;
}
.pair input {
  font-size: 18px;
  padding: 0.2rem 0.7rem;
  margin-top: 0.2rem;
}
.pair label {
  font-size: 19px;
}
a {
  display: block;
}
.kirish,
.register {
  display: inline;
  background-color: rgb(13, 72, 153);
  color: #fff;
  font-size: 17px;
  margin-top: 0.5rem;
  padding: 0.5rem 1rem;
  width: 10rem;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}
.toggled {
  display: inline;
  background-color: #fff;
  color: rgb(13, 72, 153);
  font-size: 17px;
  margin-top: 0.5rem;
  padding: 0.2rem 1rem;
  width: fit-content;
  border: none;
  text-decoration: underline;
  cursor: pointer;
}

.close-button {
  padding: 10px;
  background-color: rgba(173, 10, 10, 0.766);
  position: absolute;
  top: 0px;
  right: 10px;
  border: none;
  font-size: 24px;
  cursor: pointer;
  font-size: small;
  color: #f5f5f5;
}
select,
option {
  padding: 0.2rem 0.3rem;
  font-size: 18px;
}
</style>
