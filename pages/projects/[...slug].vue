<script setup>
const { path } = useRoute()
const { data: project } = await useAsyncData(`content:${path}`, () => queryContent(path).findOne())

watchEffect(() => {
  if (project?.value) {
    useSeoMeta({
      title: `${project.value.title} - Ali Guliyev`,
    })
  }
})
</script>

<template>
  <div>
    <article v-if="project" class="mx-auto page">
      <BackButton class="mb-2" />
      <h1 class="text-4xl">{{ project.title }}</h1>
      <ul class="list-none flex flex-row flex-wrap items-center gap-3 mt-2">
        <li v-for="tag in project.tags" :key="tag">
          <Tag :name="tag" />
        </li>
      </ul>

      <div class="flex flex-row gap-3 mt-3">
        <a v-if="project.demo" class="flex items-center gap-0.5" :href="project.demo" target="_blank">
          <span>Live Demo</span>
          <Icon icon="mingcute:arrow-right-line" class="text-sm mt-0.5" />
        </a>
        <a v-if="project.github" class="flex items-center gap-0.5" :href="project.github" target="_blank">
          <span>Github</span>
          <Icon icon="mingcute:arrow-right-line" class="text-sm mt-0.5" />
        </a>
      </div>

      <!-- Description Section with Thin Line Below -->
      <div v-if="project.description" class="mt-3">
        <p class="text-primary text-lg">{{ project.description }}</p>
        <div class="bg-primary-light mt-2 w-full h-0.2"></div>
      </div>

      <ContentRenderer :value="project" class="project" />
      <BackButton class="mt-5" />
    </article>
    <div v-else class="text-center py-10">
      <p>Loading...</p>
    </div>
  </div>
</template>
