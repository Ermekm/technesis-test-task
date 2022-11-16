<template>
  <v-app>
    <div class="box box-one">
      <h3>"Город Сыра и мира"</h3>
      <tag-list :tags="tags" align="left"></tag-list>
    </div>
    <div class="box box-two">
      <h3>"О кирхах, рыцарях и замках"</h3>
      <tag-list :tags="tags" align="left"></tag-list>
    </div>
    <div class="box box-three">
      <h3>Экскурсия в национальный парк "Куширская коса"</h3>
      <tag-list :tags="tags" align="left"></tag-list>
    </div>
  </v-app>
</template>

<script>
import TagList from "./components/TagList.vue";

export default {
  name: "App",
  components: {
    TagList,
  },

  data: () => ({
    tags: [
      {
        id: 1,
        title: "5",
        icon: "star-outline",
      },
      {
        id: 2,
        title: "Обзорная",
      },
      {
        id: 3,
        title: "На автобусе",
        icon: "bus",
      },
      {
        id: 4,
        title: "25 марта",
      },
      {
        id: 5,
        title: "6 часов",
        icon: "clock-outline",
      },
      {
        id: 6,
        title: "до 49",
        icon: "account",
      },
    ],
  }),
};
</script>

<style>
* {
  box-sizing: border-box;
}

.box {
  margin-top: 100px;
  margin-left: 20px;
}

.box-one {
  width: 300px;
}

.box-two {
  width: 400px;
}

.box-three {
}
</style>
