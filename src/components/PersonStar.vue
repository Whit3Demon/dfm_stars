<script>
import starBlueImage from "@/assets/images/star-blue.png";
import starGreenImage from "@/assets/images/star-green.png";
import starPinkImage from "@/assets/images/star-pink.png";
import starRedImage from "@/assets/images/star-red.png";
import starTurquoiseImage from "@/assets/images/star-turquoise.png";
import starWhiteImage from "@/assets/images/star-white.png";
import starYellowImage from "@/assets/images/star-yellow.png";
import { getRandomIntInclusive } from "@/Utils/math.js";

export default {
  name: 'PersonStar',
  props: {
    avatar: {
      required: true,
      type: String,
    },
    name: {
      required: true,
      type: String,
    },
    description: {
      required: true,
      type: String,
    },
    size: {
      type: Number,
      default: 32,
    },
    hoverColor: {
      type: String,
      default: 'yellow',
    },
  },
  data() {
    const imgArr = [starYellowImage, starGreenImage, starPinkImage, starBlueImage, starRedImage,starTurquoiseImage, starWhiteImage];
    const randomValue = getRandomIntInclusive(0, imgArr.length - 1);
    return {
      starImage: imgArr[randomValue],
    };
  },
  computed: {
    starImageStyle: function () {
      const size = Math.round(this.size);
      const angle = getRandomIntInclusive(0, 90);
      return `width:${size}px;height:${size}px;rotate:${angle}deg;`
    },
    popoverWidth: function () {
      return window.innerWidth < 350 ? 260 : 300;
    },
    avatarSize: function () {
      return window.innerWidth < 350 ? 100 : 120;
    },
  },
}
</script>

<template>
  <div class="person-star">
    <el-popover :width="popoverWidth">
      <template #reference>
        <el-image :src="starImage" :style="starImageStyle" class="person-star__star-image" />
      </template>
      <div class="person-star__content">
        <p class="person-star__content-name">{{ name }}</p>
        <div class="person-star__content-main">
          <div>
            <el-avatar :size="avatarSize" :src="avatar" shape="square" class="person-star__content-main-avatar" />
          </div>
          <p class="person-star__content-main-description">{{ description }}</p>
        </div>
      </div>
    </el-popover>
  </div>
</template>

<style lang="scss" scoped>
.person-star {
  &__star-image {
    animation: fadeIn 2s ease;

    @keyframes fadeIn {
      0% {
        opacity: 0;
      }

      100% {
        opacity: 1;
      }
    }

    &:hover {
      background: radial-gradient(yellow, transparent 70%);
    }
  }

  &__content {
    display: flex;
    gap: 10px;
    flex-direction: column;
    align-items: center;

    &-name {
      font-weight: bold;
      margin: 0;
    }

    &-main {
      display: flex;
      gap: 10px;
      flex-direction: row;

      &-description {
        margin: 0;
        padding: 0;
      }
    }
  }
}
</style>