<script setup lang="ts">
import { getIconName } from '@/utils/utils'

// Add console.log to debug
const { data, error } = await useAsyncData('social', () => {
  const result = queryContent('social').findOne()
  console.log('Query result:', result) // Debug log
  return result
})

// Debug logs
console.log('Data:', data.value)
console.log('Error:', error.value)

const socialLinks = computed(() => data.value?.social || [])
</script>

<template>
  <div>
    <nav class="h-25 flex items-center justify-between max-w-8xl mx-auto px-8">
      <Logo />
      <ul class="flex items-center justify-between list-none gap-x-4">
        <li><NuxtLink to="/blog">Blog</NuxtLink></li>
        <li><NuxtLink to="/projects">Projects</NuxtLink></li>
        <li><NuxtLink target="new" to="/pdf/resume.pdf">Resume</NuxtLink></li>
        <li v-for="social in socialLinks" :key="social.icon">
          <NuxtLink :to="social.link" target="blank">
            <Icon :icon="getIconName(social.icon)" width="1.5em" height="1.5em" />
          </NuxtLink>
        </li>
      </ul>
    </nav>
  </div>
</template>
