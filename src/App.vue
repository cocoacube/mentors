<template>
  <div>
    <vk-modal :show.sync="show">
      <createmors @createDone="memberCreated" />
    </vk-modal>
    <vk-navbar>
      <vk-navbar-logo slot="center">Mentors</vk-navbar-logo>
    </vk-navbar>
    <div style="margin:20px">
      <div class="uk-margin-small">
        <vk-button @click="show = true" type="primary">新增成员</vk-button>
      </div>
      <div style="display: flex;">
        <div style="width: 50%">
          <h5 style="margin:10px">学生</h5>
          <vk-table :data="students">
            <vk-table-column title="Name" cell="name"></vk-table-column>
            <vk-table-column title="Role" cell="type"></vk-table-column>
          </vk-table>
        </div>
        <div style="width: 50%">
          <h5 style="margin:10px">导师</h5>
          <vk-table :data="mentors">
            <vk-table-column title="Name" cell="name"></vk-table-column>
            <vk-table-column title="Role" cell="type"></vk-table-column>
          </vk-table>
        </div>
      </div>
      <vk-tabs>
        <vk-tabs-item title="学生">
          <student-tab :students="students" :mentors="mentors" @confirmSelection="updateStudentsData" />
        </vk-tabs-item>
        <vk-tabs-item title="导师">
          <playground :students="students" :mentors="mentors" @chooseStudent="onChooseStudent" @addToMentor="onAddToMentor" />
        </vk-tabs-item>
      </vk-tabs>
    </div>
  </div>
</template>

<script>
  import {
    Card
  } from "vuikit/lib/card";
  import {
    Button
  } from "vuikit/lib/button";
  
  import Mentor from "../components/mentor.vue";
  import Playground from "../components/playground.vue";
  import CreateMorS from "../components/createMentorOrStudent.vue";
  import StudentTab from "../components/studentTab.vue";
  
  export default {
    components: {
      Playground,
      'createmors': CreateMorS,
      'student-tab': StudentTab
    },
    name: "app",
    methods: {
      createMember: function(event) {
        this.show = true;
      },
      memberCreated: function(val) {
        console.log(val);
        this.show = false;
        if (val.type === 'student') {
          this.students.push(val);
        } else {
          this.mentors.push(val);
        }
        console.log(this.students.length);
        console.log(this.mentors.length);
      },
      updateStudentsData(row) {
        for (let s of this.students) {
          if (s.name === row.name) {
            s.firstMentor = row.firstMentor;
            s.secondMentor = row.secondMentor;
            s.thirdMentor = row.thirdMentor;
          }
        }
        console.log(this.students);
      },
      onChooseStudent: function(student) {
        for (let s of this.students) {
          if (s.name === student.name) {
            s.isAvailable = false;
          }
        }
      },
      onAddToMentor: function(val) {
        for( let m of this.mentors) {
          if (m.name === val.mentor.name) {
            m.selectedStudents.push(val.student);
          }
        }
      }
    },
    data() {
      return {
        show: false,
        students: [],
        mentors: [],
        mockStudents: [{
            name: 'kim',
            type: 'student',
            firstMentor: '',
            secondMentor: '',
            thirdMentor: ''
          },
          {
            name: 'Jerry',
            type: 'student',
            firstMentor: '',
            secondMentor: '',
            thirdMentor: ''
          }
        ],
        mockMentors: [{
            name: 'Stefen',
            type: 'mentor',
            selectedStudents: []
          },
          {
            name: 'Johanson',
            type: 'mentor',
            selectedStudents: []
          }
        ]
      }
    }
  };
</script>