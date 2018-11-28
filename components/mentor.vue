<template>
  <div style="width: 300px; margin: 20px">
    <h3 style="margin: 30px"> {{mentor.name}} </h3>
    <hr style="margin: 30px">
    <draggable v-model="studentList" :options="{draggable:'.item'}">
      <div v-for="student in students" :key="student.name" class="item">
        <vk-card v-if="ifShowStudent(student)" style="width:300px; margin: 30px">
          <vk-card-title>{{student.name}}</vk-card-title>
          <div slot="footer">
            <vk-button size="small" @click="chooseCandidate(student)">Choose</vk-button>
          </div>
        </vk-card>
      </div>
    </draggable>
  </div>
</template>

<script>
  import draggable from 'vuedraggable';
  export default {
    components: {
      draggable
    },
    name: "mentor",
    props: {
      mentor: Object,
      students: Array
    },
    methods: {
      getMentorStudents: function() {
        let mStudents = this.students.map(student => {
          if (student.firstMentor === this.mentor.name || student.secondMentor === this.mentor.name || student.thirdMentor === this.mentor.name) {
            return student;
          }
        });
        console.log(mStudents);
      },
      chooseCandidate: function(student) {
        this.$emit('chooseStudent', student);
        this.$emit('addToMentor', {mentor: this.mentor, student: student})
      },
      ifShowStudent: function( student ) {
        for(let s of this.mentor.selectedStudents) {
          if( s.name === student.name) {
            return true;
          }
        }

        return student.isAvailable;
      }
    },
    computed: {
      studentList: function() {
        return this.getMentorStudents();
      }
    },
    data() {
      return {}
    }
  };
</script>