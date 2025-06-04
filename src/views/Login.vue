<template>
  <div class="login-wrapper">
    <div class="login-card">
      <h1>🚀 Portal Acadêmico</h1>
      <p class="subtitle">Acesse com sua conta institucional</p>
      <button @click="loginGoogle">Entrar com Google</button>
    </div>
  </div>
</template>

<script>
import { getAuth, GoogleAuthProvider, signInWithPopup } from "firebase/auth";

export default {
  methods: {
    loginGoogle() {
      const auth = getAuth();
      const provider = new GoogleAuthProvider();
      signInWithPopup(auth, provider)
        .then(() => this.$router.push("/dashboard"))
        .catch((error) => console.error("Erro no login:", error));
    }
  }
};
</script>

<style scoped>
.login-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(to right, #f0f4ff, #e6ecfa);
}

.login-card {
  background: #fff;
  padding: 3rem 2rem;
  border-radius: 16px;
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.1);
  text-align: center;
  width: 100%;
  max-width: 360px;
}

h1 {
  margin-bottom: 0.5rem;
  font-size: 1.8rem;
  font-weight: 700;
  color: #1a237e;
}

.subtitle {
  font-size: 0.95rem;
  color: #555;
  margin-bottom: 2rem;
}

button {
  padding: 0.75rem 2rem;
  font-size: 1rem;
  background: #4285f4;
  color: #fff;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  box-shadow: 0 6px 12px rgba(66, 133, 244, 0.3);
  transition: all 0.3s ease;
}

button:hover {
  background: #3367d6;
  box-shadow: 0 8px 18px rgba(66, 133, 244, 0.4);
  transform: scale(1.03);
}
</style>
