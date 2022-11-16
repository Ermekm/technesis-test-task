<template>
  <div
    class="wrapper"
    :class="[align === 'left' ? 'align-left' : 'align-space-between']"
    ref="wrapper"
  >
    <template class="tag-list__group" v-for="(tag, index) in tagList">
      <v-icon v-if="index" :key="'icon' + tag.id">mdi-circle-small</v-icon>
      <div class="tag-list__item test" :key="'item' + tag.id">
        <v-icon class="tag-list__item-icon"> mdi-{{ tag.icon }}</v-icon>
        <p class="tag-list__item-title">{{ tag.title }}</p>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    tags: {
      type: Array,
      requred: true,
    },
    align: {
      validator: function (value) {
        return ["left", "space-between"].includes(value);
      },
    },
  },
  data() {
    return {
      wrapperWidth: 0,
      filteredTags: JSON.parse(JSON.stringify(this.tags)),
    };
  },

  // bind event handlers to the `handleResize` method (defined below)
  mounted: function () {
    window.addEventListener("resize", this.handleResize);
    this.calcTagWidth();
    this.handleResize();
  },
  beforeDestroy: function () {
    window.removeEventListener("resize", this.handleResize);
  },

  methods: {
    handleResize() {
      if (this.$refs.wrapper) {
        this.wrapperWidth = this.$refs.wrapper.offsetWidth;
        this.filterTags();
      }
    },
    filterTags() {
      let tagListWidth = this.filteredTags[0].width;
      let i = 1;
      console.log(this.filteredTags);
      while (i < this.filteredTags.length) {
        if (
          tagListWidth + this.filteredTags[i].width + 24 <
          this.wrapperWidth
        ) {
          this.filteredTags[i].show = true;
          tagListWidth += this.filteredTags[i].width + 24;
          i++;
        } else {
          break;
        }
      }
      while (i < this.filteredTags.length) {
        this.filteredTags[i].show = false;
        i++;
      }
    },

    calcTagWidth() {
      const tagItems = this.$refs.wrapper?.children;
      let j = 0;
      for (let i = 0; i < tagItems.length; i++) {
        if ([...tagItems[i].classList].includes("tag-list__item")) {
          this.filteredTags[j].width = tagItems[i].offsetWidth;
          j++;
        }
      }
    },
  },
  computed: {
    tagList() {
      const wrapperWidth = this.wrapperWidth;
      return this.filteredTags.filter((tag) => {
        return tag.show === undefined ? true : tag.show;
      });
    },
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.tag-list__group {
  display: flex;
}

.tag-list__item {
  white-space: nowrap;
  display: flex;
  align-items: center;
}

.tag-list__item-title {
  padding-left: 5px;
  margin-bottom: 0;
}

.align-left {
  justify-content: flex-start;
}

.align-space-between {
  justify-content: space-between;
}
</style>