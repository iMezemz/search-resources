<template>
  <div>
    <h1>Resource Table</h1>
    <input
      type="text"
      @change="handleChange"
      v-model="this.Name"
      placeholder="Search by Name"
    />
    <input
      type="text"
      @change="handleChange"
      v-model="this.Year"
      placeholder="Search by Year"
    />
    <input
      type="text"
      @change="handleChange"
      v-model="this.Color"
      placeholder="Search by Color"
    />
    <input
      type="text"
      @change="handleChange"
      v-model="this.Pantone"
      placeholder="Search by Pantone Value"
    />
  </div>
  <hr />
  <table border="3px">
    <tr>
      <th>Name</th>
      <th>Year</th>
      <th>Color</th>
      <th>Pantone Value</th>
    </tr>
    <tr :key="resource.id" v-for="resource in this.filteredResources">
      <th>{{ resource.name }}</th>
      <th>{{ resource.year }}</th>
      <th>{{ resource.color }}</th>
      <th>{{ resource.pantone_value }}</th>
    </tr>
  </table>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      resources: {},
      filteredResources: {},
      Name: "",
      Year: "",
      Color: "",
      Pantone: "",
    };
  },
  mounted() {
    this.fetchResources();
  },
  updated() {
    console.log(this.Name, this.Year, this.Color, this.Pantone);
    console.log(this.filteredResources);
    console.log(this.resources);
  },
  methods: {
    async fetchResources() {
      const response = await fetch("https://reqres.in/api/unknown");
      const json = await response.json();
      this.resources = json.data;
      this.filteredResources = this.resources;
    },
    handleChange() {
      this.filteredResources = this.resources.filter((resource) => {
        return (
          resource.name.toLowerCase().includes(this.Name.toLowerCase()) &&
          resource.year
            .toString()
            .toLowerCase()
            .includes(this.Year.toString().toLowerCase()) &&
          resource.color
            .toString()
            .toLowerCase()
            .includes(this.Color.toString().toLowerCase()) &&
          resource.pantone_value
            .toString()
            .toLowerCase()
            .includes(this.Pantone.toString().toLowerCase())
        );
      });
    },
  },
};
</script>

<style>
</style>
