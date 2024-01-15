<template>
    <section>
        <h3>Aniadir Profesor</h3>
        <div> <label>Nombre:</label><input type="text" v-model="teacher.teacherName"/></div>
        <div> <label>Apellidos:</label><input type="text" v-model="teacher.surname"/></div>
        <div> <label>Ci:</label><input type="text" v-model="teacher.ci"/></div>
        <div> <label>Materias:</label><input type="text" v-model="subject"/><button @click="handleSubjet()">Agregar</button></div>
        <div>
            <ul>
                <li v-for="(elm, index ) in teacher.subjects" :key="index">
                {{ elm }}
                </li>
            </ul>
        </div>
        <input type="checkbox" v-model="teacher.doc"/>Documentacion entregada
        <button @click="handleAddTeacher()">Agregar</button>
    </section>
    <section>
        <h3>Listado de profesores</h3>
        <table>
            <tr>
                <th>Nombre</th>
                <th>Apellidos</th>
                <th>Ci</th>
                <th>Materias</th>
                <th>Documentacion entregada</th>
            </tr>
            <tr v-for="elm in teachers" :key="elm.ci">
            <th>{{ elm.teacherName }}</th>
            <th>{{ elm.surname }}</th>
            <th>{{ elm.ci }}</th>
            <th>
                <ul>
                    <li v-for="(item, index) in elm.subjects" :key="index">{{ item }}</li>
                </ul>
            </th>
            <th v-if="elm.doc">Entregada</th>
            <th v-else>No entregada</th>
            </tr>
        </table>

    </section>
    
</template>

<script setup>
  import{ref} from 'vue'

  let teacher =ref({
    teacherName:'',
    surname:'',
    ci:'',
    subjects:[],
    doc:false
  })

  let teachers = ref([])
  let subject =ref('')

  const handleSubjet=()=>{
    teacher.value.subjects.push(subject.value)
    subject.value=''
  }
  const handleAddTeacher=()=>{
    teachers.value.push({
        teacherName: teacher.value.teacherName,
        surname:teacher.value.surname,
        ci:teacher.value.ci,
        subjects:teacher.value.subjects,
        doc:teacher.value.doc

    })
    teacher.value.teacherName=''
    teacher.value.surname=''
    teacher.value.ci=''
    teacher.value.subjects=[]
    teacher.value.doc=false
  }


</script>
<style scoped>

</style>
