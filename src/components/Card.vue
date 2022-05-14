<script>
export default {
  props: {
    position: {
      type: Number,
      required: true,
    },
    value: {
      type: Number,
      required: true
    },
    showing: {
      type: Boolean,
      required: false
    },
    images: {
      type: String,
      required: true
    },
    header: {
      type: String,
      required: true
    },
    body: {
      type: String,
      required: true
    },
    footer: {
      type: String,
      required: true
    }
  },

  setup(props, context){

    const cardSelected = () => {
      context.emit('select-card', {position: props.position})
    }
    return {
      cardSelected,
    }
  }

}
</script>


<template>
  <div class="card" @click="cardSelected">
    <div v-if="showing" class="card-face card-front">
      <div class="card-content">
    <div class="card-header">
      <slot name="header">{{header}}</slot>
    </div>
    <div class="card-body">
      <slot>{{body}}</slot>
    </div>
    <div class="card-footer">
      <slot name="footer">{{footer}}</slot>
    </div>
      </div>
    </div>
    <div v-else class="card-face card-back">
        <slot name="back">
          <img class='image' :src="images" alt="dog-image"/>
        </slot>
    </div>
  </div>
</template>

<style>

.card{
  border: 1px solid #ccc;
  border-radius: .5rem;
  cursor: pointer;
}

.card-content{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  font-size: 1.5rem;
}

.card:hover{
  transform: scale(1.05);
  transition: all .2s ease-in-out;
}

.card-face{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: transform .5s;
}

.card-front{
  background-color: #fff;
  border-radius: .5rem .5rem 0 0;
  color: #000;
}

.card-back{
  border-radius: 0 0 .5rem .5rem;
}

.image {
  width: 100%;
  height: 100%;
}
</style>