<template>
    <div>
        <div>
            <form id="burger-form">
                <div class="input-container">
                    <label for="nome">Seu nome:</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
                </div>
                <div class="input-container">
                    <label for="pao">Escolha o pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="carne">Escolha a carne do seu Burger:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                </div>
                <div id="opicionais-container" class="input-container">
                    <label id="opcionais-title" for="opicionais">Selecione os opicionais</label>
                    <div class="chama">
                        <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                            <input  type="checkbox" name="opiconais" v-model="opcionais" :value="opcional.tipo">
                            <span>{{ opcional.tipo }}</span>
                        </div>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu Burger">
                </div>
            </form>
        </div>
    </div>
    
</template>

<script setup>
import { onMounted, ref } from "vue";


let paes= ref();
let carnes= ref();
let opcionaisdata= ref();
let nome= ref();
let pao = ref();
let carne= ref();
let opcionais= ref([]);
let status= ref("Solocitado");
let msg = ref();

async function getingredientes(){
    const req = await fetch("http://localhost:3000/ingredientes");
    const data = await req.json();

    console.log(data);
    console.log(data.paes);

    paes.value = data.paes;
    carnes.value = data.carnes;
    opcionaisdata.value = data.opcionais;
    console.log(opcionaisdata.value);
}

onMounted(()=>{
    getingredientes();
})
</script>

<style scoped>
#burger-form{
    max-width: 400px;
    margin: 0 auto;
}

.chama {
    display: flex;
    align-items: cente;
    gap: 12px;
    flex-wrap: wrap;
    width: 60%;
    justify-content: space-between;
}

.input-container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label{
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

input,select{
    padding: 5px 10px;
    width: 300px;
}

#opicionais-title{
    width: 100%;
    align-items: flex-start;
    

}

.checkbox-container span,
.checkbox-container input{
    width: auto;
    
}

.checkbox-container span{
    margin-left: 6px;
    font-weight: bold;
}

.checkbox-container{
    display: flex;
    flex-direction: row;

}

.submit-btn{
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
    
}

.submit-btn:hover{
    background-color: transparent;
    color: #222;
}
</style>