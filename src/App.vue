/* EXERCÍCIO 1 (0.5 pontos a serem adicionados na avaliação 1) 

     - Faça um formulário com 4 campos: nome, cpf, email e senha e um botão de salvar
     - O botão de salvar só pode ser habilitado com as seguintes condições:
     -  1. todos os campos preenchidos
     -  2. o campo senha deve ter no mínimo 8 caracteres contendo:
     -  2.1 no mínimo 1 maiúscula, 1 minúscula, 1 número e 1 carácter especial.
     -  2.2 deve haver uma lista indicando que cada regra da senha foi cumprido ou não.

    dica: utilize regex ou não.
    */
<template>
    <div class="wrapper">
        <h1>Exercício 1</h1> 
        <form @submit.prevent="onSubmit">
            <div class="group">
                <label for="nome">Nome</label>
                <input type="text" id="nome" v-model="name" placeholder="Digite seu nome"/>
            </div>
            <div class="group">
                <label for="cpf">CPF</label>
                <input type="text" id="cpf" v-model="cpf" placeholder="Digite seu cpf"/>
            </div>
            <div class="group">
                <label for="email">Email</label>
                <input type="text" id="email" v-model="email" placeholder="Digite seu email"/>
            </div>
            <div class="group">
                <label for="senha">Senha</label>
                <input type="password" id="senha" v-model="password" placeholder="Digite sua senha"/>
            </div>
            <ul>
                <li :class="passwordLength">8 ou mais caracteres</li>
                <li :class="passwordUppercase">1+ letra maiúscula</li>
                <li :class="passwordLowercase">1+ letra minúscula</li>
                <li :class="passwordSpecial">1+ carácter especial</li>
                <li :class="passwordNumber">1+ número</li>
            </ul>
            <button :disabled="!completed" type="submit">Salvar</button>
        </form>
        
    </div>
</template>

<script setup>
    import { ref, computed } from 'vue'
    
    const name = ref("");
    const cpf = ref("");
    const email = ref("");
    const password = ref("");

    function onSubmit(){
        alert("Formulário enviado com sucesso!");
    }

    const completed = computed(
        () => {
            if(name.value && cpf.value && email.value && password.value && 
            passwordLength.value && passwordUppercase.value && passwordLowercase.value && 
            passwordSpecial.value && passwordNumber.value)
                return true;
            return false;
        }
    );

    const passwordLength = computed(
        () => {
            if(password.value.length >= 8)
                return "check";
            return '';
        }
    );

    const passwordUppercase = computed(
        () => {
            if((/[A-Z]/g).test(password.value))
                return "check";
            return '';
        }
    );

    const passwordLowercase = computed(
        () => {
            if((/[a-z]/g).test(password.value))
                return "check";
            return '';
        }
    );

    const passwordSpecial = computed(
        () => {
            if((/[!@#$%&*()_+^~{}]/g).test(password.value))
                return "check";
            return '';
        }
    );

    const passwordNumber = computed(
        () => {
            if((/[\d]/g).test(password.value))
                return "check";
            return '';
        }
    );
</script>

<style>
    .wrapper{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    form{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .group{
        display: flex;
        flex-direction: column;
        align-items: flex-start;

    }
    label{
        margin-top: 10px;
        font-weight: bold;
    }
    input{
        margin-bottom: 10px;
        padding: 5px;
        border-radius: 5px;
        width: 200px;
        outline: none;
    }
    input:placeholder{
        color: gray;
    }
    button{
        margin-top: 10px;
        padding: 5px;
        border-radius: 5px;
        width: 200px;
        background-color: orange;
        border: none;
        cursor: pointer;
        font-weight: bold;
        color: var(--color-text)
    }
    button:disabled{
        background-color: gray;
        cursor: not-allowed;
    }
    ul{
        list-style: none;
        display: flex;
        flex-direction: column;
        align-items: center;

    }
    li{
        color:gray;
        text-decoration: line-through;

    }
    .check{
        color:limegreen;
        text-decoration: none;
        font-weight: bold;
    }
</style>