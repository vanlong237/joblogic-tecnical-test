<template>
  <section class="details">
    <header class="details__header">
    </header>
    <section class="detail__main">
      <section class="details__profile">
        <div class="details__profile__info">
          <img
            class="details__profile__avatar"
            alt="avatar"
            :src="loadImage(details.image)"
          />
          <h1 class="details__profile__name">
            {{ details.name }}
          </h1>
        </div>
        <div class="details__profile__popularity">
          <h4>Popularity</h4>
          <input
            type="range"
            min="1"
            max="10"
            :value="details.popularity"
            @input="(ev) => $emit('onChangePopularity', ev.target.value)"
            class="slider"
          >
        </div>
        <div class="details__profile__biography">
          <h4>Biography</h4>
          <p>{{ details.biography }}</p>
        </div>
      </section>
    </section>
  </section>
</template>
<script setup>

defineProps({
  details: {
    type: Object,
    default: () => ({})
  }
});

const loadImage = (image) => new URL(`/src/assets/_images/Profile pics/${image}`, import.meta.url).href;

</script>
<style>
.details {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
}
.details__header {
  height: 300px;
  width: 100%;
  background-image: url('@/assets/_images/Header image/Godfather header.jpg');
  background-position: top;
  background-repeat: no-repeat;
  background-size: cover;
}
.detail__main {
  background-color: #2e2e36;
  flex: 1;
}
.details__profile {
  height: 100%;
  margin-left: 300px;
  margin-top: -50px;
  padding-left: 140px;
  padding-right: 20px;
  position: relative;
  transition: all ease-in-out 0.25s;
}
.details__profile__avatar {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border: 1px solid #ffffff;
  border-radius: 4px;
  position: absolute;
  left: 20px;
  top: 0;
}
.details__profile__name {
  margin-top: 0;
  margin-bottom: 1rem;
  font-size: 2rem;
}
.details__profile__biography {
  background-color: #1a1d24;
  line-height: 1.5;
  padding: 1rem;
  border-radius: 4px;
}
.details__profile__biography * {
  margin: 0;
}
.details__profile__biography h4 {
  font-size: 1.25rem;
  margin-bottom: 1rem;
}
.details__profile__popularity {
  padding: 1rem 0;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.details__profile__popularity h4 {
  margin: 0;
  font-size: 1.25rem;
}
.details__profile__popularity .slider {
  width: 100%;
}

/* For extremely small screen devices (595px and below) */
@media only screen and (max-width: 595px) {
  .details__profile__avatar {
    position: relative;
    left: 0;
    margin-bottom: 1rem;
  }
  .details__profile {
    padding-left: 20px;
  }
}

@media only screen and (max-width: 768px) {
  .details__profile {
    margin-left: 0;
  }
  .details__header {
    height: 200px;
  }
}

</style>