<template>
  <div style="width: 1200px">
    <h1>Student List</h1>
    <DataTable
      :data="people"
      :column="column"
      :calculate="calculate"
      :sumColumns="sumColumns"
    >
      <template #actions="{ row, index }">
        <div class="actions">
          <MyButton
            label="Save"
            @click="handleSave(row, index)"
            v-if="row.editing"
          >
            Save
          </MyButton>
          <MyButton
            label="Edit"
            icon="mdi-pencil"
            @click="handleEdit(row, index)"
            v-if="!row.editing"
          >
            Edit
          </MyButton>
          <MyButton
            label="Delete"
            icon="mdi-delete"
            @click="handleDelete(index)"
            >Delete</MyButton
          >
        </div>
      </template>
    </DataTable>
    <div>
      <MyButton label="Add Student" @click="handleCreate">Add Student</MyButton>
    </div>
  </div>
</template>

<script>
import DataTable from "./components/table/DataTable.vue";
import MyButton from "./components/table/MyButton.vue";
export default {
  components: {
    DataTable,
    MyButton,
  },
  data() {
    return {
      people: [],
      column: [
        { name: "name", field: "Name", value: "name" },
        { name: "age", field: "Age", value: "age" },
        { name: "email", field: "Email", value: "email" },
        { name: "math", field: "Math", value: "math" },
        { name: "literature", field: "Literature", value: "literature" },
        { name: "english", field: "English", value: "english" },
        { name: "isMale", field: "IsMale", value: "isMale", type: "boolean" },
        { name: "actions", field: "Actions" },
      ],
      calculate: "average",
      sumColumns: ["math", "english"],
    };
  },
  methods: {
    getPeople() {
      this.people = JSON.parse(localStorage.getItem("people"));
      if (!this.people) {
        this.people = [
          {
            name: "John Doe",
            age: 30,
            email: "upchh@example.com",
            math: 10,
            literature: 10,
            english: 10,
            isMale: true,
          },
          {
            name: "Jane Doe",
            age: 20,
            email: "upchh@example.com",
            math: 10,
            literature: 10,
            english: 10,
            isMale: false,
          },
          {
            name: "Jane Doe",
            age: 20,
            email: "upchh@example.com",
            math: 10,
            literature: 10,
            english: 10,
            isMale: false,
          },
          {
            name: "Jane Doe",
            age: 20,
            email: "upchh@example.com",
            math: 10,
            literature: 10,
            english: 10,
            isMale: false,
          },
        ];
      }
    },
    handleEdit(row, index) {
      row.editing = true;
    },
    handleDelete(index) {
      this.people.splice(index, 1);
      localStorage.setItem("people", JSON.stringify(this.people));
    },
    handleSave(row, index) {
      row.editing = false;
      localStorage.setItem("people", JSON.stringify(this.people));
    },
    handleCreate() {
      const newStudent = {};
      this.people.push(newStudent);
      this.handleEdit(newStudent, this.people.length - 1);
      localStorage.setItem("people", JSON.stringify(this.people));
    },
  },
  created() {
    this.getPeople();
  },
};
</script>

<style>
table {
  border-collapse: collapse;
  width: 100%;
}

thead {
  background-color: #ddd;
}

th,
td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}
</style>
