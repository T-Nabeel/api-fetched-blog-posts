<template>
  <div class="blog-card">
    <div class="blog-card__img__container">
      <img
        src="../assets/pexels-blog.jpg"
        alt="blog-placeholder-image"
        class="blog-card__img"
      />
    </div>
    <h3 class="blog-card__title"><slot name="blog-title"></slot></h3>
    <div class="blog-card__meta">
      <p class="blog-card__author"><slot name="blog-author"></slot></p>
      <span
        ><svg
          width="5"
          height="5"
          viewBox="0 0 5 5"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <circle cx="2.5" cy="2.5" r="2.5" fill="#adadad" />
        </svg>
      </span>
      <p class="blog-card__date"><slot name="blog-date"></slot></p>
    </div>
    <p class="blog-card__content"><slot name="blog-content"></slot></p>
  </div>
</template>

<style lang="scss" scoped>
.blog-card {
  border-radius: 10px;

  &:hover .blog-card__img {
    transform: scale(1.05);
  }

  &__img__container {
    overflow: hidden;
    height: 18rem;
  }

  &__img {
    border-radius: 2px;
    width: 100%;
    object-fit: cover;
    object-position: 50% 5%;
    transition: 0.3s all ease-in-out;
  }

  &__title {
    color: #181818;
    font-size: 1.4375rem;
    margin: 1rem 0 0.4rem 0;
  }

  &__meta {
    display: flex;
    align-items: center;
    gap: 10px;
    color: #8a8a8a;
    font-weight: 400;

    span {
      display: flex;
      align-items: center;
    }
  }

  &__content {
    color: #181818;
    margin-top: 0.2rem;
    font-size: 1.125rem;
  }
}
</style>
