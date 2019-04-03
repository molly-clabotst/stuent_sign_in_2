<template>
    <div>
        <!--        Write Template Here-->
        <div class="card student-list m-2 p-2">
            <h4 class="card-title">Students</h4>
            <div class="edit-table-toggle form-check">
                <input id="edit-table" type="checkbox" class="form-check-input"
                v-model="editTable">
                <label for="edit-table" class="form-check-label">Edit table?</label>
            </div>
            <div id="student-table">
                <table class="table">
                    <tr>
                        <th>Name</th>
                        <th>StarID</th>
                        <th>Present?</th>
                        <th v-show="editTable">Delete</th>
                    </tr>
                    <StudentRow
                            v-for='student in students'
                            v-bind:key="student.name"
                            v-bind:student="student"
                            v-bind:edit="editTable"
                            v-on:student-present="studentArrivedOrLeft">

                    </StudentRow>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
    // Create and export component here
    import StudentRow from "./StudentRow";
    export default {
        name: 'StudentTable',
        components: {StudentRow},
        props:{
            students: Array
        },
        methods:{
            studentArrivedOrLeft(student){
                this.$emit('student-present',student)
            }
        }
    }
</script>

<style>
    /*write any styles for theis component here*/
    #student-table {
        max-height: 500px;
        overflow: scroll;
    }
    .present-true{
        color: aquamarine;
        font-weight: bold;
        font-style: italic;
        background-color: darkgrey;
    }
    .present-false {
        color: darkred;
        font-weight: bold;
        background-color: dimgray;
    }
</style>