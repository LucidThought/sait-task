<template>
  <v-container>
    <v-select
      :items="possiblePriority"
      v-model="filterPriority"
      label="Priority Filter"
      @change="filterThisPriority"
      dense
    ></v-select>
    <v-select
      :items="possibleStatus"
      v-model="filterStatus"
      label="Status Filter"
      @change="filterThisStatus"
      dense
    ></v-select>
    <v-btn @click="clearFilters()">Clear Filters</v-btn>
    <v-data-table
      :headers="headers"
      :items="filteredPrograms"
      :sort-by="['priority']"
      :sort-desc="[false]"
    ></v-data-table>
  </v-container>
</template>

<script>
export default {
  name: "Task1",

  data: () => ({
    possiblePriority: ["1", "2", "3"],
    possibleStatus: ["Available", "Not Available"],
    programs: [],
    filteredPrograms: [],
    headers: [
      {
        text: "Program Title",
        align: "left",
        sortable: false,
        value: "title",
      },
      {
        text: "Priority",
        align: "center",
        sortable: true,
        value: "priority",
      },
      {
        text: "Status",
        align: "left",
        sortable: false,
        value: "status",
      },
    ],
    filterPriority: null,
    filterStatus: null,
  }),
  created() {
    this.populateTable();
  },
  methods: {
    populateTable() {
      this.programs.push(
        {
          title: "Information Technology",
          priority: 1,
          status: "Available",
        },
        {
          title: "Engineering Design and Drafting Technology",
          priority: 2,
          status: "Available",
        },
        {
          title: "Welding Engineering Technology",
          priority: 2,
          status: "Not Available",
        },
        {
          title: "Account Oil and Gas Production",
          priority: 3,
          status: "Available",
        },
        {
          title: "Baker Apprentice",
          priority: 1,
          status: "Not Available",
        },
        {
          title: "Dental Assisting",
          priority: 1,
          status: "Available",
        },
        {
          title: "Electrician Apprentice",
          priority: 2,
          status: "Not Available",
        },
        {
          title: "Environmental Technology",
          priority: 3,
          status: "Not Available",
        },
        {
          title: "Film and Video Production",
          priority: 1,
          status: "Available",
        },
        {
          title: "Hospitality Management",
          priority: 2,
          status: "Not Available",
        }
      );
      this.filteredPrograms = this.programs;
    },
    clearFilters() {
      this.filterPriority = null;
      this.filterStatus = null;
      this.parseFilters();
    },
    filterThisPriority(newFilter) {
      this.filterPriority = newFilter;
      this.parseFilters();
    },
    filterThisStatus(newFilter) {
      this.filterStatus = newFilter;
      this.parseFilters();
    },
    parseFilters() {
      this.filteredPrograms = this.programs;
      if (this.filterPriority) {
        this.filteredPrograms = this.filteredPrograms.filter(
          (p) => p.priority == this.filterPriority
        );
      }
      if (this.filterStatus) {
        this.filteredPrograms = this.filteredPrograms.filter(
          (p) => p.status == this.filterStatus
        );
      }
    },
  },
};
</script>
