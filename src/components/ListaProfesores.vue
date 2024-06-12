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
            <div>
                <ul>
                    <li v-for="item in teacher.subjects" :key="item">{{ item }}</li>
                </ul>
            </div>
        </div>
        <div>
            <label>Documentos</label>
            <input type="checkbox" v-model="teacher.docs">
            <button @click="handleTeacher()">Agregar</button>
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

const handleSubject = () => {
    if (subject.value.trim()) {
        teacher.value.subjects.push(subject.value.trim());
    }
    subject.value = '';
};

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
</script>

<style scoped>
</style>
