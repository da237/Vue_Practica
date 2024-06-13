<template>
    <section>
        <h1>Anadir Profesor</h1>
        <div>
            <label for="name">Nombre Completo</label>
            <input type="text" v-model="teacher.ticherName" value="name" placeholder="Diguite nombre">
        </div>
        <div>
            <label for="dni">Dni</label>
            <input type="text" v-model="teacher.ticherDni" value="dni" placeholder="Diguite Dnni">
        </div>
        <div>
            <label for="materias">Materias</label>
            <input type="text" v-model="subject" value="materias" placeholder="Diguite Materias">
            <button @click="handleSubject()">Agregar</button>
            <button @click="change()">{{ isEditing ? Hola : Dos }}Hola</button>
            <div>
                <ul>
                    <li v-for="item in teacher.subjects" :key="item">{{ item }}</li>
                </ul>
            </div>
        </div>
        <div>
            <label>Documentos</label>
            <input type="checkbox" v-model="teacher.docs">
            <button @click="handleTeacher">{{ isEditing ? 'Actualizar' : 'Agregar' }}</button>
        </div>
    </section>
    <section>
        <h3>Listado de profesores</h3>
        <table>
            <tr>
                <th>Nombre</th>
                <th>Dni</th>
                <th>Materias</th>
                <th>Documentos</th>
                <th>Acciones</th>
            </tr>
           <tr v-for="elm in teachers" :key="elm.dni">
            <th>{{ elm.ticherName }}</th>
            <th>{{ elm.ticherDni }}</th>
            <th>
                <ul>
                    <li v-for="item in elm.subjects" :key="item">{{ item }}</li>
                </ul>
            </th>
            <th v-if="elm.docs">Entregado</th>
            <th v-else>No entregado</th>
            <th><button >Editar</button></th>
            <th><button @click="eliminar(elm)">Eliminar</button></th>
           </tr>
        </table>
    </section>
</template>

<script setup>
import { ref } from 'vue'

let teacher = ref({
    ticherName: '',
    ticherDni: '',
    subjects: [],
    docs: false,
})

let teachers = ref ([])

let subject  = ref ('');
let isEditing = ref (false);

const handleSubject = () => {
    if (subject.value.trim()) {
        teacher.value.subjects.push(subject.value.trim());
    }
    subject.value = '';
};

const change = () => {
    isEditing.value =  !isEditing.value
}
const handleTeacher = () => { 
    teachers.value.push({
        ticherName: teacher.value.ticherName,
        ticherDni: teacher.value.ticherDni,
        subjects: teacher.value.subjects,
        docs: teacher.value.docs,
    })
    teacher.value.ticherName = "",
    teacher.value.ticherDni = "",
    teacher.value.subjects = []
    teacher.value.docs = false;
}

const eliminar = (elm) => {
    teachers.value.splice(elm)
}
</script>

<style scoped>
</style>
