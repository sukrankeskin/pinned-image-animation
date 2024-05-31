<template>
  <div class="wrapp">
    <div class="spacer"></div>
    <section class="work">
      <div class="work__left">
        <div class="work__text">
          <div
            class="work__info"
            v-for="(info, index) in workInfo"
            :key="index"
          >
            <div class="work__left-b1">
              <span class="work__num">{{
                String(index + 1).padStart(2, "0")
              }}</span>
              <h2 class="title">
                {{ info.title }} <span class="stroke">{{ info.subtitle }}</span>
              </h2>
              <a href="#" class="work__link">view more</a>
            </div>
          </div>
        </div>
      </div>

      <div class="work__right">
        <div class="work__right-b1">
          <div class="work__photo">
            <div
              v-for="(photo, index) in photos"
              :key="index"
              class="work__photo-item"
              :title="index + 1"
            >
              <img :src="photo.src" alt="" />
            </div>
          </div>
        </div>
      </div>
    </section>
    <div class="spacer"></div>
  </div>
</template>

<script>
import { onMounted } from "vue";
import Lenis from "@studio-freight/lenis";
import { gsap } from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

export default {
  setup() {
    const workInfo = [
      { title: "image animated", subtitle: "on gsap" },
      { title: "UI/UX", subtitle: "design" },
      { title: "web", subtitle: "design" },
      { title: "Brand", subtitle: "design" },
    ];

    const photos = [
      {
        src: "https://images.unsplash.com/photo-1670201202862-96b9c3d11375?q=80&w=2868&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      },
      {
        src: "https://images.unsplash.com/photo-1633772695640-b82bf3e3f1cb?q=80&w=2787&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      },
      {
        src: "https://images.unsplash.com/photo-1716694318677-dc75a9d7e439?q=80&w=2787&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      },
      {
        src: "https://images.unsplash.com/photo-1667242050251-8a4eee25141c?q=80&w=2787&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      },
    ];

    onMounted(() => {
      initializeAnimations();
    });

    const initializeAnimations = () => {
      const lenis = new Lenis({
        duration: 1.2,
        smooth: true,
      });

      function raf(time) {
        lenis.raf(time);
        requestAnimationFrame(raf);
      }

      requestAnimationFrame(raf);

      lenis.on("scroll", ScrollTrigger.update);

      gsap.ticker.add((time) => {
        lenis.raf(time * 1000);
      });

      const workInfoItems = document.querySelectorAll(".work__photo-item");
      workInfoItems.forEach((item, index) => {
        item.style.zIndex = workInfoItems.length - index;
      });

      gsap.set(".work__photo-item", {
        clipPath: "inset(0px 0px 0px 0px)",
      });

      const animation = gsap.to(".work__photo-item:not(:last-child)", {
        clipPath: "inset(0px 0px 100% 0px)",
        stagger: 0.5,
        ease: "none",
      });

      ScrollTrigger.create({
        trigger: ".work",
        start: "top top",
        end: "bottom bottom",
        animation: animation,
        scrub: 1,
      });
    };

    return {
      workInfo,
      photos,
    };
  },
};
</script>

<style>
@import url(../assets/styles.css);

/* Add any additional styles if needed */
</style>
