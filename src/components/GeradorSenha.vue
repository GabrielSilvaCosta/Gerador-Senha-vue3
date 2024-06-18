<template>
  <div class="container text-center mt-5 mb-5 p-5 bg-light rounded shadow">
    <h1 class="display-4 mb-3">Gerador de Senha</h1>
    <div
      class="row mb-3 justify-content-center text-center p-3 rounded shadow bg-light"
    >
      <div class="col-12 p-3 mb-3 text-center shadow bg-light rounded p-3 mb-3">
        <label class="form-label">Tamanho da senha</label>
        <input
          type="number"
          class="form-control"
          placeholder="Tamanho da senha"
          v-model="passwordLength"
        />
      </div>

      <div class="col-12 p-3">
        <label class="form-label">Incluir maiúsculas</label>
        <input
          type="checkbox"
          class="form-check-input"
          v-model="includeUppercase"
        />
      </div>

      <div class="col-12 p-3">
        <label class="form-label">Incluir minúsculas</label>
        <input
          type="checkbox"
          class="form-check-input"
          v-model="includeLowercase"
        />
      </div>

      <div class="col-12 p-3">
        <label class="form-label">Incluir números</label>
        <input
          type="checkbox"
          class="form-check-input"
          v-model="includeNumbers"
        />
      </div>

      <div class="col-12 p-3">
        <label class="form-label">Incluir símbolos</label>
        <input
          type="checkbox"
          class="form-check-input"
          v-model="includeSymbols"
        />
      </div>

      <div class="col-12 p-3">
        <button type="button" class="btn btn-primary" @click="generatePassword">
          Gerar senha
        </button>
      </div>

      <div class="col-12 p-3">
        <label class="form-label">Senha gerada</label>
        <input
          type="text"
          class="form-control"
          placeholder="Senha gerada"
          v-model="generatedPassword"
          readonly
        />
      </div>

      <div class="col-12 p-3">
        <button type="button" class="btn btn-secondary" @click="copyPassword">
          Copiar senha
        </button>
      </div>

      <div class="col-12 p-3">
        <button type="button" class="btn btn-danger" @click="clearPassword">
          Limpar senha
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "GeradorSenha",
  data() {
    return {
      passwordLength: 12,
      includeUppercase: true,
      includeLowercase: true,
      includeNumbers: true,
      includeSymbols: true,
      generatedPassword: "",
    };
  },
  methods: {
    generatePassword() {
      let generatedPassword = "";
      let characters = "";
      if (this.includeUppercase) {
        characters += "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
      }
      if (this.includeLowercase) {
        characters += "abcdefghijklmnopqrstuvwxyz";
      }
      if (this.includeNumbers) {
        characters += "0123456789";
      }
      if (this.includeSymbols) {
        characters += "!@#$%^&*()_+";
      }

      if (characters.length === 0) {
        alert("Por favor, selecione pelo menos uma opção de caractere.");
        return;
      }

      for (let i = 0; i < this.passwordLength; i++) {
        generatedPassword += characters.charAt(
          Math.floor(Math.random() * characters.length)
        );
      }
      this.generatedPassword = generatedPassword;
    },
    copyPassword() {
      navigator.clipboard.writeText(this.generatedPassword);
      alert("Senha copiada para a área de transferência!");
    },
    clearPassword() {
      this.generatedPassword = "";
    },
  },
};
</script>

<style>
body {
  background: #f2f6fc;
  font-family: "Arial", sans-serif;
}

.container {
  background: #ffffff;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  padding: 30px;
  max-width: 600px;
  margin: 0 auto;
}

h1 {
  font-size: 2.5rem;
  color: #333333;
}

.form-label {
  font-weight: bold;
  font-size: 1.1rem;
  color: #555555;
}

input[type="number"],
input[type="text"] {
  border: 2px solid #dddddd;
  border-radius: 5px;
  padding: 10px;
  width: 100%;
  margin-top: 5px;
}

input[type="checkbox"] {
  transform: scale(1.2);
  margin-left: 10px;
}

input[readonly] {
  background-color: #eeeeee;
}

button {
  width: 100%;
  padding: 10px;
  font-size: 1rem;
  margin-top: 10px;
}

button.btn-primary {
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  transition: background-color 0.3s;
}

button.btn-primary:hover {
  background-color: #0056b3;
}

button.btn-secondary {
  background-color: #6c757d;
  border: none;
  border-radius: 5px;
  transition: background-color 0.3s;
}

button.btn-secondary:hover {
  background-color: #565e64;
}

button.btn-danger {
  background-color: #dc3545;
  border: none;
  border-radius: 5px;
  transition: background-color 0.3s;
}

button.btn-danger:hover {
  background-color: #b02a37;
}

@media (max-width: 576px) {
  .container {
    padding: 20px;
  }

  h1 {
    font-size: 2rem;
  }

  .form-label {
    font-size: 1rem;
  }
}
</style>
