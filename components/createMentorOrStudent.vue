<template>
    <div>
        <vk-modal-title>创建成员</vk-modal-title>
        <form>
            <fieldset class="uk-fieldset">
                <div class="uk-margin">
                    <input class="uk-input" v-model="name" type="text" placeholder="姓名">
                </div>
    
                <div class="uk-margin">
                    <div class="uk-form-controls uk-form-controls-text">
                        <label><input class="uk-radio" v-model="picked" type="radio" value='student' name="radio"> 学生</label>
                        <label style="margin-left: 50px"><input class="uk-radio" value="mentor" v-model="picked" type="radio" name="radio"> 导师</label>
                    </div>
                </div>
            </fieldset>
        </form>
        <vk-button @click="done">完成</vk-button>
    </div>
</template>

<script>
    import {
        Button
    } from "vuikit/lib/button";
    
    export default {
        components: {
            "vk-button": Button,
        },
        name: "CreateMentorOrStudent",
        props() {
            return {
                isStudent: boolean
            }
        },
        methods: {
            done: function() {
    
                if (this.picked === 'student') {
                    let newMember = {
                        name: this.name,
                        type: this.picked,
                        isAvailable: true
                    }
                    console.log(newMember);
                    this.$emit('createDone', newMember);
                } else {
                    let newMember = {
                        name: this.name,
                        type: this.picked,
                        selectedStudents: []
                    }
                    console.log(newMember);
                    this.$emit('createDone', newMember);
                }
    
    
            }
        },
        data() {
            return {
                name: '',
                picked: 'student'
            };
        },
        computed: {
    
        }
    };
</script>