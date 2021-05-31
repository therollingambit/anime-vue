<template>
  <div class="card">
    <img :src="anime.image_url" :alt="anime.title" />
    <h3>{{ anime.title }}</h3>
    <p>
      Score: <span>{{ anime.score }}</span>
    </p>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["anime"],
};
</script>

<style lang="scss" scoped>
.card {
  flex: 0 1 31%;
  flex-wrap: wrap;
  width: 31%;
  max-width: 31%;
  padding: 0 8px;
  margin-bottom: 18px;

  img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    border-radius: 16px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    transition: 0.4s;
  }

  h3 {
    color: #313131;
    padding: 10px;
    transition: 0.4s;
    text-align: center;
  }

  p {
    color: #888;
    transition: 0.4s;
    text-align: center;

    span {
      color: #81a1c1;
    }
  }

  &:hover {
    img {
      transform: scale(1.05);
    }

    h3 {
      color: #24c444;
    }
  }
}
</style>
