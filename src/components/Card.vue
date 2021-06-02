<template>
  <div class="card">
    <div class="inner">
      <div class="front">
        <img :src="anime.image_url" :alt="anime.title" />
        <h3>{{ anime.title }}</h3>
      </div>
      <div class="back">
        <h3>{{ anime.title }}</h3>
        <p>
          Description: <span>{{ anime.synopsis }}</span>
        </p>
        <p>
          Type: <span>{{ anime.type }}</span>
        </p>
        <p>
          Episodes: <span>{{ anime.episodes }}</span>
        </p>
        <p>
          Score: <span class="score">{{ anime.score }}</span>
        </p>
      </div>
    </div>
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
  /* flex: 0 1 31%;
  flex-wrap: wrap;
  width: 31%;
  max-width: 31%;
  padding: 0 8px;
  margin-bottom: 18px;
  perspective: 1000px; */
  width: 300px;
  height: 300px;
  perspective: 1000px;
  flex: 0 1 31%;
  padding: 0 8px;
  margin-bottom: 18px;

  @media screen and (max-width: 500px) {
    max-width: 90%;
    flex: 1 1 90%;
    margin: 10px auto;
  }

  img {
    width: 100%;
    height: 230px;
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

    @media screen and (max-width: 500px) {
      font-size: 16px;
    }
  }

  p {
    color: #888;
    transition: 0.4s;
    text-align: center;

    span {
      color: #81a1c1;
    }
  }
}

.inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.card:hover .inner {
  transform: rotateY(180deg);
}

.front,
.back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

.back {
  background-color: transparent;
  color: white;
  transform: rotateY(180deg);
  p {
    color: #313131;
    padding-top: 6px;

    @media screen and (max-width: 500px) {
      font-size: 15px;
    }

    span {
      color: #888;
    }
    .score {
      color: #1da538;
    }
  }
}
</style>
