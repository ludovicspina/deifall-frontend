<template>
  <div>
    <div v-for="item in items" :key="item.id">
      <div> {{ item.name }}</div>
      <button v-on:click="deleteItem(item.id)">X</button>
    </div>

    <div>
      <form @submit.prevent="storeItem">
        <div>
          <label for="name">Name:</label>
          <input
              type="text"
              v-model="item.name"
              id="name"
              required
          />
        </div>
        <div>
          <label for="description">Description:</label>
          <textarea
              v-model="item.description"
              id="description"
              required
          ></textarea>
        </div>
        <div>
          <label for="image">Image:</label>
          <input
              type="text"
              v-model="item.image"
              id="image"
              required
          />
        </div>
        <button type="submit">Submit</button>
      </form>
    </div>
  </div>
</template>
<script lang="ts">
import type {Item} from "~/interfaces/item";
import axios from "axios";

export default defineComponent({
  name: "index",
  data: () => {
    return {
      urlApi: "" as string,
      items: [] as Item[], // Interface
      item: {} as Item,
    }
  },
  mounted() {
    const runtimeConfig = useRuntimeConfig();
    this.urlApi = runtimeConfig.public.apiUrl as string;
    axios.get(this.urlApi + "/api/items").then((response) => {
      this.items = response.data as Item[];
    }).catch((error) => {
      console.log(error);
    });
  },
  methods: {
    storeItem() {
      axios.post(this.urlApi + "/api/items", this.item).then((response) => {
        this.items.push(response.data);
        this.item = {} as Item; // Réinitialisation du formulaire
      }).catch((error) => {
        console.log(error);
      })
    },
    deleteItem(id: number) {
      axios.delete(this.urlApi + "/api/items/" + id).then((response) => {
        const indexItemInArray = this.items.map(item => item.id).indexOf(id);
        this.items.splice(indexItemInArray, 1);
      }).catch((error) => {
        console.log(error);
      })
    }
  }
})

</script>