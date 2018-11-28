<template>
    <vk-table :data="students" justified>
        <vk-table-column class="uk-width-small" title="Name" cell="name"></vk-table-column>
        <vk-table-column title="第一志愿">
            <select class="uk-select" slot-scope="{ row }" v-model="row.firstMentor">
                <option v-for="m in mentors" :key="m.name"> 
                    {{m.name}}
                </option>
            </select>
        </vk-table-column>
        <vk-table-column title="第二志愿">
            <select class="uk-select" slot-scope="{ row }" v-model="row.secondMentor">
                <option v-for="m in mentors" :key="m.name"> 
                        {{m.name}}
                </option>
            </select>
        </vk-table-column>
        <vk-table-column title="第三志愿">
            <select class="uk-select" slot-scope="{ row }" v-model="row.thirdMentor">
                <option v-for="m in mentors" :key="m.name"> 
                        {{m.name}} 
                </option>
            </select>
        </vk-table-column>
        <vk-table-column title="Action">
            <vk-button slot-scope="{ row }" @click="confirm(row)">确认</vk-button>
        </vk-table-column>
    </vk-table>
</template>

<script>
    import {
        Card
    } from "vuikit/lib/card";
    import {
        Button
    } from "vuikit/lib/button";
    
    export default {
        components: {
            "vk-button": Button,
            "vk-card": Card
        },
        name: "app",
        props: {
            students: Array,
            mentors: Array
        },
        methods: {
            confirm: function(row) {
                console.log(row);
                this.$emit('confirmSelection', row);
            }
        },
        data() {
            return {
    
            };
        }
    };
</script>