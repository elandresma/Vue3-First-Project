<script setup>
import { ref, computed } from 'vue'

const name = 'vue dyn';
let estiloh2 = 'color:blue;font-size:40px';
const arrayColores = ['Blue', 'red', 'melo']
const activo = false;
const mostrar = false;
//estoy creando una variable reactiva, le dice al navegador que tiene que estar escuchando cambios
let contador = ref(0);
let arrayNums = ref([]);
const arrayFrutasFor = [
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        stock: 0,
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
        stock: 10,
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
        stock: 20,
    },
];
const arrayFrutas = [
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
    },
];

const objFruta = {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
}


//metodo -methods

const handleClick = (mensaje) => {
    alert(mensaje);
}

const increment = () => contador.value++;
const decrement = () => contador.value--;
const reset = () => contador.value = 0;
const add = () => arrayNums.value.push(contador.value);


//una propiedad computada es una especie de escuchador cuando una variable cambie de valor. con datos reactivos se recomienda usar computed, para no llamar metodos
const classCounter = computed(() => {
    if (contador.value === 0) {
        return "zero";
    }
    return contador.value > 0 ? "positivo" : "negativo";
});
const tranqui = computed(() => {
    return arrayNums.value.some(element => element == contador.value);
});
</script>

<template>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
    <h1>
        Hola Primera practica de Vue
    </h1><br>
    <!--<h2 :style="estiloh2">
        soy azul
    </h2>
    <h2 v-if="activo">
        Si esta activo
    </h2>
    <h2 v-else-if="!activo">
        no esta activo
    </h2>
    <h2 v-else>
        indeciso
    </h2>-->
    <div class="container">
        <!-- Renderiza pero lo oculta con css. si se va a mostrar y ocultar muchas veces en la ejecucion es mas optimo usar
vshow. si es una condicion inicial preferir v-if-->
        <!--<h2 v-show="mostrar">
        si se va a mostrar
    </h2>

    <h2>
        {{ activo? "Si esta activo": "no no esta" }}
    </h2>-->
        <ul>
            <!-- El key se envia por temas de optimizacion de vue, le ayuda a identificar los nodos  -->
            <!-- El key se envia por temas de optimizacion de vue, le ayuda a identificar los nodos  duplicar linea ctrl+shtfit+flechabajo-->
            <li v-for="{ name, price } in arrayFrutas" :key="name">
                la fruta {{ name }} tiene un valor de {{ price }}
            </li>

        </ul>

        <!-- Recorrer un obj  -->
        <li v-for="(value, prop) in objFruta" :key="value">
            {{ prop }} = {{ value }}
        </li>

        <!-- El template recorre un objeto o arreglo sin agregar ningun elemento html -->
        <div class="row">
            <div class="col">
                <template v-for="{ name, price, stock } in arrayFrutasFor" :key="name">
                    <li v-if="stock > 0">
                        {{ name }} vale {{ stock }}
                    </li>
                </template>
                <div class="btn-group">
                    <button class="btn btn-primary" @click.right.prevent="handleClick('Texto derecho')">
                        Dame click derecho
                    </button>
                    <button class="btn btn-success" @click.middle="handleClick('Texto medio')">
                        Dame click medio
                    </button>
                    <button class="btn btn-danger" @click.left="handleClick('Texto izquierdo')">
                        Dame click izquierdo
                    </button>
                </div>
            </div>
            <div class="row">
                <h2 :class="classCounter">{{ contador }}</h2>
                <div class="btn-group">
                    <button type="button" class="btn btn-primary" @click="increment">
                        BtnAumentar
                    </button>
                    <button type="button" class="btn btn-success" @click="decrement">
                        BtnDisminuir
                    </button>
                    <button type="button" class="btn btn-danger" @click="reset">
                        BtnReset
                    </button>
                    <button type="button" class="btn btn-primary" :disabled="tranqui" @click="add">
                        BtnAdd
                    </button>
                </div>
                <div class="row">
                    <div class="col-md-6 mt-4">
                        <ul class="list-group">
                            <li class="list-group-item" v-for="num in arrayNums" :key="num">
                                {{ num }}
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>



    </div>

</template>

<style>
h1 {
    color: red;
}

.positivo {
    color: green
}

.negativo {
    color: red;
}

.zero {
    color: peru;
}
</style>