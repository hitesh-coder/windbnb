<template>
  <div>
    <h1>Stays in Finland</h1>
    <div class="section">
      <div
        v-for="item in items"
        :key="item.id"
        :class="
          (city === item.city || city === '') && totalGuest < item.maxGuests
            ? ''
            : 'none'
        "
        class="card"
      >
        <div class="image">
          <img :src="item.photo" alt="" />
        </div>
        <div class="mainText">
          <h3 v-if="item.superHost">SUPER HOST</h3>
          <div style="display: flex">
            <h4>{{ item.type }}</h4>
            <h5 v-if="item.beds">. {{ item.beds }} beds</h5>
          </div>
          <div class="rating">
            <i class="material-icons">star</i>
            <span>{{ item.rating }}</span>
          </div>
        </div>
        <div>
          <h2>{{ item.title }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Data from "../../assets/stays.json";

export default {
  name: "content",
  data() {
    return {
      items: Data,
    };
  },
  props: {
    city: String,
    totalGuest: Number,
  },
};
</script>

<style lang="scss" scoped>
h1 {
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  line-height: 29px;
  margin: 1rem 0rem;

  color: #333333;
}

.section {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
  position: relative;
}

.card {
  display: flex;
  flex-direction: column;
  position: relative;

  .image {
    position: relative;
    overflow: hidden;
    border-radius: 1rem;
    height: 250px;
    margin-top: 0.5rem;
    img {
      width: 100%;
      height: 100%;
      transition: 0.5s all ease-out;
      &:hover {
        transform: scale(1.1);
      }
    }
  }
  .mainText {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    margin-top: 0.5rem;
    h3 {
      display: inline-block;
      font-weight: bold;
      font-size: 12px;
      line-height: 15px;
      color: #4f4f4f;
      border: 1px solid black;
      padding: 0.35rem;
      border-radius: 0.75rem;
      white-space: nowrap;
    }
    div {
      h4,
      h5 {
        font-weight: 500;
        font-size: 14px;
        line-height: 17px;
        color: #828282;
        white-space: nowrap;
      }
    }
    .rating {
      display: flex;
      align-items: center;
      i {
        color: orange;
        font-size: 16px;
        line-height: 17px;
      }
      span {
        font-style: normal;
        font-weight: 500;
        font-size: 14px;
        line-height: 17px;
        color: #4f4f4f;
      }
    }
  }
  h2 {
    margin-top: 0.5rem;
    font-weight: 600;
    font-size: 16px;
    line-height: 20px;
    color: #333333;
  }
}

.none {
  display: none;
}

@media screen and (max-width: 1100px) {
  .card {
    .image {
      height: 200px;
    }
    .mainText {
      h3 {
        font-size: 10px;
        line-height: 13px;
      }
      div {
        h4,
        h5 {
          font-size: 12px;
          line-height: 15px;
        }
      }
      .rating {
        i {
          font-size: 14px;
          line-height: 15px;
        }
        span {
          font-size: 12px;
          line-height: 15px;
        }
      }
    }
    h2 {
      font-size: 14px;
      line-height: 17px;
    }
  }
}

@media screen and (max-width: 770px) {
  .card {
    .image {
      height: 180px;
    }
    .mainText {
      h3 {
        font-size: 8px;
        line-height: 11px;
      }
      div {
        h4,
        h5 {
          font-size: 10px;
          line-height: 13px;
        }
      }
      .rating {
        i {
          font-size: 12px;
          line-height: 13px;
        }
        span {
          font-size: 10px;
          line-height: 13px;
        }
      }
    }
    h2 {
      font-size: 12px;
      line-height: 15px;
    }
  }
}

@media screen and (max-width: 430px) {
  .section {
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 1rem;
    position: relative;
  }

  .card {
    .image {
      height: 200px;
    }
  }
}
</style>
