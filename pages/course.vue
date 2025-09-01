<template>
  <div class="prose mb-12">
    <h1>
      <span class="font-medium">
        Course:
        <span class="font-bold">Mastering Nuxt 3</span>
      </span>
    </h1>
  </div>

  <div class="flex flex-row justify-center flex-grow">
    <div class="prose mr-4 p-8 bg-white rounded-md min-w-[20ch] max-w-[30ch] flex flex-col">
      <h3>Chapters</h3>
      <div class="space-y-1 mb-4 flex flex-col" v-for="chapter in chapters" :key="chapter.slug">
        <h4>{{ chapter.title }}</h4>
        <NuxtLink v-for="(lesson, index) in chapter.lessons" :key="lesson.slug"
          class="flex flex-row space-x-1 no-underline prose-sm font-normal py-1 px-4 -mx-4" :to="lesson.path" :class="{
            'text-blue-500':
              lesson.path === $route.fullPath,
            'text-gray-600':
              lesson.path !== $route.fullPath,
          }">
          <span class="text-gray-500">{{ index + 1 }}.</span>
          <span>{{ lesson.title }}</span>
        </NuxtLink>
      </div>
    </div>

    <div class="prose p-12 bg-white rounded-md w-[65ch]">
      <NuxtErrorBoundary>
        <NuxtPage />
        <template #error="{ error, clearError }">
          <div class="text-red-500">
            <h2>Oops, something went wrong!</h2>
            <p><strong>{{ error.statusMessage || error.message }}</strong></p>
            <button
              @click="clearError({ redirect: '/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3' })">
              Reset
            </button>
          </div>
        </template>
      </NuxtErrorBoundary>
    </div>
  </div>
</template>

<script setup>
const { chapters } = useCourse();

</script>

<style lang="css" scoped>
.custom-button {
  cursor: pointer;
  background-color: #6b7280;
  /* bg-gray-500 */
  color: white;
  font-weight: bold;
  padding: 0.25rem 0.75rem;
  /* py-1 px-3 */
  border-radius: 0.375rem;
  /* rounded */
}

.custom-button:hover {
  cursor: pointer;
}
</style>