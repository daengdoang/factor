<template>
  <div class="hero">
    <div class="hero-inner">
      <div>
        <factor-link class="back" :path="setting('portfolio.indexRoute')">
          <factor-icon icon="fas fa-arrow-left" />
          {{ returnLinkText }}
        </factor-link>
        <h1 class="title">
          <factor-link
            :path="postLink(post._id)"
            class="text-gray-100 hover:text-red-500"
          >{{ post.title }}</factor-link>
        </h1>
        <h3 class="entry-subtitle text-gray-100">{{ post.subTitle }}</h3>
        <factor-post-edit :post-id="post._id" />
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { setting, stored, postLink } from "@factor/api"
import { factorLink, factorIcon } from "@factor/ui"
import { factorPostEdit } from "@factor/post"
import Vue from "vue"
export default Vue.extend({
  components: { factorLink, factorIcon, factorPostEdit },
  props: {
    postId: { type: String, default: "" },
    format: { type: String, default: "" }
  },
  computed: {
    post(this: any) {
      return stored(this.postId) || {}
    },
    returnLinkText() {
      return setting("portfolio.returnLinkText") || "All Projects"
    }
  },
  methods: {
    postLink,
    setting
  }
})
</script>
<style lang="less">
// Single
.portfolio-single-entry {
  .hero {
    position: relative;
    overflow: hidden;
    background-image: radial-gradient(
      at bottom -30% right -30%,
      #732b29 0%,
      #111010 75%,
      #111010 100%
    );
    background-color: #351a19;

    .hero-inner {
      position: relative;
      align-items: center;
      padding: 5em 2em;
      max-width: 800px;
      margin: 0 auto;

      .back {
        font-weight: var(--font-weight-bold);
      }
      .title {
        font-weight: var(--font-weight-bold);
        font-size: 3em;
        letter-spacing: -0.03em;
        margin: 0.3em 0;
        @media (max-width: 900px) {
          font-size: 2em;
        }
        a {
          &:hover {
            text-decoration: underline;
          }
        }
      }
      .entry-subtitle {
        line-height: 1.7;
      }
      .content {
        font-size: 1.2em;
        line-height: 1.6em;
        opacity: 0.5;
      }
      .hero-image {
        background-position: center;
        background-size: cover;
        background-repeat: no-repeat;
        height: 450px;
        max-width: 300px;
        box-shadow: 20px 60px 120px 0 rgba(0, 0, 0, 0.33);
        border-top-left-radius: 40px;
        @media (max-width: 900px) {
          margin: 0 auto;
          max-width: 100%;
        }
      }
      @media (max-width: 900px) {
        padding: 5em 2em 3em;
      }
    }
  }
}
</style>
