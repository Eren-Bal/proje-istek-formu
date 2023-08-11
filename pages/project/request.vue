<template>
  <v-container>
    <v-app-bar :clipped-left="clipped" fixed app dense>
      <v-spacer />
      <v-toolbar-title class="title">İstek Proje Sayfası</v-toolbar-title>
      <v-spacer />
    </v-app-bar>
    <v-row dense>
      <v-col cols="12" md="4" lg="4">
        <v-text-field
          append-icon=""
          v-model="project.personName"
          label="İsteyenin Adı Ve Soyadı"
          outlined
          dense
          hide-details
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="4" lg="4">
        <v-text-field
          v-model="project.sectionName"
          label="Bölüm Adı"
          outlined
          dense
          hide-details
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="4" lg="4">
        <v-select
          :items="urgencyItems"
          v-model="project.urgency"
          label="Aciliyet Durumu"
          outlined
          dense
          hide-details
        ></v-select>
      </v-col>
    </v-row>

    <v-row dense>
      <v-col cols="12">
        <v-text-field
          v-model="project.name"
          label="Proje Adı"
          outlined
          dense
          hide-details
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row dense>
      <v-col cols="12" md="6" lg="6">
        <select-date
          :label="'Proje İsteme Tarihi'"
          @date="handleRequestDate"
        ></select-date>
      </v-col>
      <v-col cols="12" md="6" lg="6">
        <select-date
          :label="'Proje Teslim Tarihi'"
          @date="handleDeliveryDate"
        ></select-date>
      </v-col>
    </v-row>

    <v-row dense>
      <v-col cols="12">
        <v-textarea
          v-model="project.description"
          label="Proje Açıklaması"
          outlined
        ></v-textarea>
      </v-col>
    </v-row>

    <v-row dense>
      <v-col cols="12" md="2" lg="2">
        <v-btn @click="save" color="green" rounded large width="150px">
          <v-icon x-large>mdi-content-save-all</v-icon></v-btn
        >
      </v-col>
      <v-col cols="12" md="2" lg="2">
        <v-btn @click="viewPage" color="blue" rounded large width="150px"
          ><v-icon x-large>mdi mdi-archive</v-icon></v-btn
        >
      </v-col>
    </v-row>
  </v-container>
</template>

<script>


class Project {
  constructor(
    personName,
    sectionName,
    urgency,
    name,
    requestDate,
    deliveryDate,
    description
  ) {
    this.personName = personName;
    this.sectionName = sectionName;
    this.urgency = urgency;
    this.name = name;
    this.requestDate = requestDate;
    this.deliveryDate = deliveryDate;
    this.description = description;
  }
}

export default {
  data() {
    return {
      urgencyItems: [
        { text: "Normal", value: 0 },
        { text: "Acil", value: 1 },
        { text: "Çok Acil", value: 2 },
      ],
      project: new Project(),
    };
  },

  methods: {
    handleRequestDate(date) {
      this.project.requestDate = date;
    },
    handleDeliveryDate(date) {
      this.project.deliveryDate = date;
    },
    save() {
      console.log("Kayıt Yapıldı :", this.project);
    },
    viewPage() {
      this.$router.push("/project/view");
    },
  },
};
</script>
