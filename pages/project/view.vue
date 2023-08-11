<template>
  <v-container>

    <template>
      <v-app-bar :clipped-left="clipped" fixed app dense>
        <v-spacer />
        <v-btn text @click="homeClick" color="green" lg width="100px"
          ><v-icon large>mdi-home</v-icon></v-btn
        >
        <v-toolbar-title class="title">İstek Proje Listesi</v-toolbar-title>
        <v-spacer />
      </v-app-bar>
      <br />

      <v-row justify="center">
        <v-expansion-panels focusable>
          <v-expansion-panel
            v-for="(project, projectIndex) of projects"
            :key="projectIndex"
          >
            <v-expansion-panel-header>
              <v-row>
                <v-col cols="1" class="d-flex justify-start">
                  <v-icon :color="urgencyColorControl(project.urgency)"
                    >mdi-alert-circle</v-icon
                  >
                </v-col>
                <v-col class="d-flex justify-start">
                  <span style="font-weight: 700">İsteyen:</span>
                  {{ project.personName }}
                </v-col>
                <v-col class="d-flex justify-center">
                  <span style="font-weight: 700">Proje Adı:</span>
                  {{ project.name }}
                </v-col>

                <v-col class="d-flex justify-center">
                  <span style="font-weight: 700">Termin:</span>
                  {{ project.deliveryDate }}
                </v-col>
              </v-row>
          
            </v-expansion-panel-header>
            <v-expansion-panel-content>
                <v-row>
                    <v-col class="d-flex justify-center">
                        <span style="font-weight: 700">İstek Tarihi:</span>
                        {{ project.deliveryDate }}
                      </v-col>
                </v-row>
                <v-row>
                    <v-textarea readonly v-model="project.description" outlined dense></v-textarea>
                </v-row>
            </v-expansion-panel-content>
          </v-expansion-panel>
        </v-expansion-panels>
      </v-row>
    </template>
  </v-container>
</template>

<script>
export default {
  props :["veri"],
  data() {
    return {
      projects: [],
    };
  },
  created() {
    this.init();
  },
  methods: {
    init() {
      this.projects = [
        {
          name: "Yazılımı Geliştirme Projesi",
          personName: "Ali Delioğlu",
          description: "Proje ile İlgili Açıklama Metini Burada Yazılıyor",
          urgency: 0,
          requestDate: "10.01.2020",
          deliveryDate: "18.07.2023",
          sectionName: "Dijital Dönüşüm",
        },
        {
          personName: "Eren Bal",
          name: "Bilgisayar Uzamanlık Sınavı",
          description: "Proje ile İlgili Açıklama Metini Burada Yazılıyor 2",
          urgency: 2,
          sectionName: "Kalite Kontrol",
          requestDate: "04.07.2023",
          deliveryDate: "05.10.2024",
        },
        {
          personName: "Alp Dağıtım",
          name: "Bilişim Sistemleri Teknolojileri",
          description: "Proje ile İlgili Açıklama Metini Burada Yazılıyor 3",
          urgency: 1,
          sectionName: "Bilişim Teknolojisi",
          requestDate: "06.12.2021",
          deliveryDate: "15.10.2024",
        },
        // Diğer projeler buraya eklenir
      ];
    },
    urgencyColorControl(urgency) {
      let color = "";
      switch (urgency) {
        case 0:
          color = "green";
          break;
        case 1:
          color = "yellow";
          break;
        case 2:
          color = "red";
          break;
      }
      return color;
    },
    homeClick() {
      this.$router.push("/project/request");
    },
  },
};
</script>
