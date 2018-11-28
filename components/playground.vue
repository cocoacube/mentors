<template>
    <div style="display:flex" >
        <div v-for="mentor in mentors" :key="mentor.name"> 
            <mentor :mentor="mentor" :students="students" @chooseStudent="onChooseStudent" @addToMentor="onAddToMentor"/>
        </div>
    </div>
</template>

<script>
    import draggable from 'vuedraggable';
    import Mentor from '../components/mentor.vue';
    
    export default {
        components: {
            draggable,
            Mentor
        },
        name: "app",
        props: {
            students: Array,
            mentors: Array
        },
        data: function() {
            return {
            };
        },
        methods: {
            onChooseStudent: function(student) {
                this.$emit('chooseStudent', student);
            },
            onAddToMentor: function(val){
                this.$emit('addToMentor', val);
            }
        }
    };
</script>