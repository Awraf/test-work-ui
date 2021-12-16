<template>
  <div>
    <div class="filter-block">
      <Radio
        :selectedData="filterData"
        :groupName="'filter'"
        @changed="changeView($event)"
      />
    </div>
    <div v-for="(film, index) of films" :key="index">
      <InfoBlockItem
        :poster="film.poster_path"
        :title="film.title"
        :description="film.overview"
        :imageLeft="getImageLeft(index)"
      />
    </div>
  </div>
</template>

<script>
import InfoBlockItem from "@/components/info/InfoBlockItem";
import Radio from "@/components/controls/Radio";

export default {
  components: {
    InfoBlockItem,
    Radio,
  },
  data() {
    return {
      imageLeft: false,
      films: [],
      originFilms: [],
      filterData: [
        {
          id: this.generateId(),
          isDefault: false,
          title:
            "отсортировать блоки по заголовку согласно алфавитного порядка",
          value: "1",
        },
        {
          id: this.generateId(),
          isDefault: false,
          title:
            "вывести все блоки в формате “изображения - слева, текст - справа”",
          value: "2",
        },
        {
          id: this.generateId(),
          isDefault: true,
          title:
            "вывести все блоки в формате “изображения - слева, текст - справа” и наоборот в шахматном порядке",
          value: "3",
        },
      ],
    };
  },
  mounted() {
    fetch(
      "https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1"
    )
      .then((result) => result.json())
      .then(
        (json) => {
          this.originFilms = json.results.slice(0, 5);
          this.films = [...this.originFilms];
        }
      );
  },
  methods: {
    generateId() {
      return (Math.random() + 1).toString(36).substring(7);
    },
    getImageLeft(index) {
      return this.imageLeft || index % 2 === 0;
    },
    changeView(value) {
      if (value === "3") {
        this.imageLeft = false;
        this.films = [...this.originFilms];
      }
      if (value === "2") {
        this.imageLeft = true;
        this.films = [...this.originFilms];
      }
      if (value === "1") {
        this.imageLeft = false;
        this.films.sort((prev, next) => {
          if (prev.title > next.title) {
            return 1;
          }
          if (next.title > prev.title) {
            return -1;
          }
          return 0;
        });
      }
    },
  },
};
</script>

<style>
.filter-block {
  width: 100%;
  margin: 32px auto;
}

.filter-block > div {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-items: center;
}

.filter-block > div > div {
  width: 50%;
  margin: 8px auto;
}
</style>