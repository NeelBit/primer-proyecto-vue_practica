<script setup>

    import { ref, computed } from 'vue';

    let horaCompleta = ref('');

    function hora() {
        let date = new Date();
        
        let hora = date.getHours().toString();
        let min = date.getMinutes().toString();
        let sec = date.getSeconds().toString();
        
        //console.log(`${hora}:${min}:${sec} hs`);

        horaCompleta.value = `${hora}:${min}:${sec}hs`;
    };

    //setTimeout(hora(), 1000);

    const name = "Cosme";

    const miStyle = "color: green";

    const hola = ()=> {
        alert("hola");
    }

    const arrayColores = ["blue", "red", "green", "yellow"];

    const activo = false;

    const arrayFrutas = ["manzana", "banana", "pera", "pomelo", "naranja"];

    const objetoUno = {"uno": 1, "dos": 2, "tres": 3, "cuatro": 4};

    const objetoDos = {
        name: "cosito",
        apellido: "coso",
        stock: 1
    }

    const arrayDeObjeto = [
        {   nombre: "juan",
            apellido: "peres",
            dni: 323412341234
        },
        {
            nombre: "julian",
            apellido: "alvarez",
            dni: 443434334343
        },
        {
            nombre: "dibu",
            apellido: "martinez",
            dni: 89987878799
        }
    ];

    const clickeaste = () => {
        console.log("hiciste click");
    };

    const saludo = (name) => {
        alert(`Hola, como estas ${name}`);
    }

    function click(text) {
        console.log(`Hiciste click ${text}`);
    }

    // variables reactivas: con ref (hacer importacion)
    let counter = ref(0);
    const increment = () => {
        // importante el .value para acceder al valor de ref()
        counter.value++;
        console.log(counter.value);
    }

    // computed siempre retorna, va a computar.
    /* se usa computed para evitar la logica en plantillas. se almacena en cache */
    const classCounter = computed(() => {

        if (counter.value === 0) {
            return 'claseZero';
        } else if (counter.value > 0){
            return 'verdecito';
        } else if (counter.value < 0) {
            return 'rojito';
        }

    });


    // practica:
    let arrayNumFav = ref([]);
    let numFav = ref(0);

    function changeNum(accion) {
        switch (accion) {
            case '+':
                numFav.value++;
                break;

            case '-':
            numFav.value--;
            break;

            case 'r':
            numFav.value = 0;
            break;
        
            default:
                break;
        }
    }

    function agregaNumFav() {
        arrayNumFav.value.push(numFav.value);
    }

    const mismoNum = computed( () => {
        if (arrayNumFav.value[arrayNumFav.value.length-1] == numFav.value) {
            return true;
        } else {
            return false;
        }

        // para revisar si se encuentra en la lista, sin importar posicion
        /* const numSearch = arrayNumFav.value.find(n => { n === counter.value});
        if (numSearch === 0) {return true};
        return numSearch ? true : false; */

    });


    /* anfn atajo para funcion anonima */

</script>


<template>
    <header>
        <h1>Hola mundo Vue.js</h1>

        <h2 @click="hola()">Bienvenido {{name.toUpperCase()}}, hace click</h2>
        <h2 >Bienvenido {{name.toUpperCase()}}</h2>

    </header>

    <section>
        
        <!-- acortar con : -->
        <!-- <h3 v-bind:style="miStyle">{{hora()}}</h3> -->
        <h3 :style="miStyle">{{hora()}}</h3>

        <!-- devuelve el array literalmente -->
        <h4>{{arrayColores}}</h4>

        <p :style="`color: ${arrayColores[0]}`">Hola {{name}}</p>

        <!-- v-show para siempre renderizar, pero ocultar por css (display none) -->
        <p v-if="activo">Esta activo?</p>
        <p v-else-if="activo === 'null'">desactivo/null</p>
        <p v-else>esta inactivo</p>

        <!-- operador ternario -->
        <p>{{activo ? "estoy activo" : "estoy inactivo"}}</p>

        <!-- v-for -->
        <ul>
            <li v-for="f in arrayFrutas"> {{f}}</li>
        </ul>

        <h3>lista de objeto:</h3>
        <ul> <!-- :key="identificador unico (generalmente item.id) para que no tenga conflico si se repiten valores" -->
            <li v-for="(value, key, index) in objetoUno">{{key}} tiene el valor de {{value}} y se encuentra en index: {{index}}</li>
        </ul>

        <h3>lista de objeto de jugadores:</h3>
        <ul>
            <li v-for="jugador in arrayDeObjeto" :key="jugador.dni"> {{jugador.nombre}} {{jugador.apellido}} tiene el dni: {{jugador.dni}}</li>
        </ul>

        <h3>lista objeto2</h3>
        <ul>

            <!-- <template></template> con for, si se quiere usar un if adentro, para que no pinte li -->

            <li v-for="(value, key, index) in objetoDos">
                key: {{key}}, valor: {{value}} en el index {{index}}
            </li>
        </ul>

        <!-- v-on se puede resumir con @ osea @click="clickeaste" -->
        <h3>evento click</h3> <!-- cuando no tenemos parametros se puede omitir los parentesis -->
        <button v-on:click="clickeaste">hace click</button>
        <button v-on:click="saludo('juancito')">hace click alert saludo</button>

        <div> <!-- modificadores para click, derecho izq o el del medio   -   .prevent para evitar el efecto por defecto -->
            <button @click.right="click('derecho')">click btn right</button>
            <button @click.right.prevent="click('derecho')">click btn right con prevent</button>
            <button @click.left="click('izq')">click btn left</button>
            <button @click.middle="click('medio')">click btn middle</button>
        </div>

        <!-- variable reactiva  con ref() no necesita .value -->
        <button @click="increment">suma contador</button>
        <button @click="counter--">resta contador</button>
        <button @click="(counter=0)">reset</button>
        <!-- <span>{{counter}}</span> -->

        <!-- contador en verde si es positivo o rojo si es negativo -->
        <!-- <span :style="counter < 0 ? 'color:red' : 'color:green'">{{counter}}</span> -->
        <!-- <span :class="counter < 0 ? 'rojito' : 'verdecito'">{{counter}}</span> -->
        <!-- código mas elegante: -->
        <span :class="classCounter">{{counter}}</span>

        <!-- ver hora -->
        <div>
            <button @click="hora">ver hora</button>
            <span>{{horaCompleta}}</span>
        </div>

        <!-- practica agregar a un array los números favoritos y mostrar -->
        <h2>números favoritos</h2>
        <button @click="changeNum('+')">+</button>
        <button @click="changeNum('-')">-</button>
        <button @click="changeNum('r')">reset</button>

        <p>{{numFav}}</p>

        <button @click="agregaNumFav" :disabled="mismoNum">agregar número a favoritos</button>

        <ul>
            <li v-for="(n, index) in arrayNumFav" :key="index">{{ n }}</li>
        </ul>

        <div v-if="(arrayNumFav.length > 0)">
            <button @click="(arrayNumFav = [])">vaciar lista</button>
        </div>

    </section>

</template>


<style>

    header {
        border: 5px solid blue;
    }
    h1 {
        background-color: red;
    }

    .rojito {
        color:red;
    }

    .verdecito {
        color: green;
    }

    .claseZero {
        color: orange;
    }

</style>

