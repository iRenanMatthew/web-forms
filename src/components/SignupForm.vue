<template>
  <h1>Forms</h1>
  <form @submit.prevent="submitForm">
    <label for="email">Email:</label>
    <input
      v-model="email"
      type="email"
      placeholder="example@gmail.com"
      required
    />

    <label for="password">Password:</label>
    <input v-model="password" type="password" required />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label for="role">Role:</label>
    <select v-model="role">
      <option value="Web Developer">Web Developer</option>
      <option value="Web Designer">Web Designer</option>
    </select>

    <label>Skills</label>
    <input
      type="text"
      v-model="tempSkill"
      @keyup="addSkill"
      placeholder="Add your skill, if done press to add"
    />

    <div class="skill-pill">
      <div v-for="skill in skills" :key="skill">
        <span class="pill" @click="deleteSkill(skill)"
          >{{ skill }} <span class="close-pill">X</span></span
        >
      </div>
    </div>

    <div class="terms">
      <input v-model="terms" type="checkbox" required />
      <label>Accept <strong>Terms and Conditions</strong></label>
    </div>

    <div class="submit">
      <button type="submit">Create an Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "Web Developer",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "Enter" && this.tempSkill) {
        if (this.skills.includes(this.tempSkill)) {
          return;
        } else {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
        console.log(this.skills);
      }
    },
    deleteSkill(id) {
      this.skills = this.skills.filter((item) => item !== id);
      console.log(this.skill);
    },

    submitForm() {
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 characters long";

      console.log("test");
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}

.skill-pill {
  display: flex;
}

.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background-color: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #1c1c1c;
  cursor: pointer;
}

span.close-pill {
  color: darkgray;
  font-weight: bolder;
}

button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}

.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
