<script>
import {ref} from 'vue'
import Card from './components/Card.vue'

export default {
  components: {
    Card
  },

  mounted() {
    fetch('https://dog.ceo/api/breeds/image/random')
        .then(response => response.json())
        .then(data => {
          this.images = data.message
        })
        .catch(error => console.log(error))

  },
  data() {
    return {
      images: '',
      info: [
        {
          header: "Dogs of the World",
          body:  "This dog is slow",
          footer: "Are you a dog lover?",
        },    {
          header:  "Dogs of Russia ",
          body:    "This dog is fast",
          footer: "Are you a dog owner?",
        },    {
          header:   "Dogs of America",
          body: "This dog is strong",
          footer:  "Are you a dog breeder?",
        },    {
          header:  "Dogs of Europe",
          body: "This dog is smart",
          footer:   "Are you a dog trainer?",
        },    {
          header:    "Dogs of Asia",
          body: "This dog is lazy",
          footer:  "Are you a cat lover?",
        },    {
          header:  "Dogs of Africa",
          body: 'This dog is fat',
          footer:"Are you a cat owner?",
        },    {
          header:  "Dogs of Australia",
          body: "This dog is skinny",
          footer: "Are you a cat breeder?",
        },    {
          header:  "Dogs of South America",
          body: "This dog is clever",
          footer: "Are you a cat trainer?",
        },    {
          header: "Dogs of Germany",
          body:   "This dog is a superhero",
          footer: "Are you looking for a dog?",
        },  {
          header:  "Dogs of the China",
          body: "This dog does math",
          footer: "Are you looking for a cat?",
        },
      ],

    }
  },


  setup() {
    const cardRows = ref([])

    for(let i = 0; i < 10; i++) {
      cardRows.value.push({
        value: i,
        showing: false,
        position: i,
        image: '',

          }
      )
    }
    const flippedCard = (p) =>{
      cardRows.value[p.position].showing = !cardRows.value[p.position].showing
    }

    return{
      cardRows,
      flippedCard,
    }
  }
}
</script>

<template>
  <header>
    <h1 class="title">Purpose Financial – Junior Web Developer Coding Challenge</h1>
  </header>
  <section class="table-top">
    <Card v-for="(card, index) in cardRows"
          :value="card.value"
          :key="`card-${index}`"
          :showing="card.showing"
          :position="card.position"
          @select-card="flippedCard"
          :images="images"
          :header="info[index].header"
          :body="info[index].body"
          :footer="info[index].footer"

    />
  </section>
</template>

<style>
@import './assets/base.css';

.title{
  font-size: 2.5em;
  text-align: center;
  color: #999;
  margin-top: 15rem;
}

.table-top{
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-gap: 1rem;
  grid-template-rows: 250px 250px 250px 250px;
  justify-content: center;
  grid-row-gap: 1rem;
  padding: 5rem;
}

</style>
