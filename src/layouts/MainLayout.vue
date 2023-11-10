<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> Trust Me </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header> Essential Links </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          :title="link.title"
          :propValue="link.model"
          :mask = "link.mask"
          @input="updateParentValue"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view :personalInfo="personalInfo" />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
  {
    title: "Дата подписания договора",
    model: "date",
    mask: "##.##"
  },
  {
    title: "ФИО",
    model: "fullname",
    mask: ""
  },
  {
    title: "Номерь удостоверения",
    model: "idCard",
    mask: "############"
  },
  {
    title: "Когда было выдано удостоверение",
    model: "givenDate",
    mask: "##.##"
  },
  {
    title: "Кем было выдано удостоверение",
    model: "givenBy",
    mask: "AAA"
  },
  {
    title: "ИИН",
    model: "IIN",
    mask: "############"
  },
  {
    title: "Место жительство",
    model: "adress",
    mask: "г. Aaaaaaaaaaaa ул.Aaaaaaaaaaaa"
  },
  {
    title: "Телефон",
    model: "phoneNumber",
    mask: "+#(###)### ## ##"
  },
  {
    title: "Почтовый код",
    model: "postCode",
    mask: "####"
  },
  {
    title: "Сумма предоплаты",
    model: "price",
    mask: "###########"
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },

  data() {
    return {
      personalInfo: {
        date: "",
        price: "",
        fullname: "",
        idCard: "",
        givenDate: "",
        givenBy: "",
        email: "",
        IIN: "",
        adress: "",
        phoneNumber: "",
        postCode: "",
      },
    };
  },

  methods: {
    updateParentValue(newValue) {
      console.log("updateParentValue:",this.personalInfo);
      this.personalInfo[newValue.target.name] = newValue.target.value

    },
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
