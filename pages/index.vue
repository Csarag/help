<template>
<div class="mx-auto max-w-7xl space-y-10">
    <ContentNavigation v-slot="{ navigation }" :query="query">
        <div v-for="product of navigation" :key="product._path">
            <h2
                class="
                    text-gray-900
                    text-2xl sm:text-3xl
                    font-bold
                    mb-2
                "
            >{{ product.title }}</h2>

            <div
                class="
                    grid
                    grid-cols-1
                    lg:grid-cols-2
                    gap-2
                    lg:gap-4
                "
            >
                <div
                    v-for="category of product.children"
                    :key="category._path"
                    class="
                        relative
                        flex
                        rounded
                        border-0
                        ring-1
                        ring-gray-300
                        hover:shadow-lg
                        ring-inset
                        bg-white
                        pl-1 pr-5
                        py-2
                        shadow-none
                        focus-within:ring-2
                        focus-within:ring-indigo-500
                        focus-within:ring-offset-2
                    "
                >
                    <div class="flex-shrink-0">
                        <div
                            v-if="category.icon"
                            class="
                                h-24 w-24
                                bg-contain bg-center bg-no-repeat
                            "
                            :style="{
                                backgroundImage: `url(${ category.icon })`,
                            }"
                        ></div>
                    </div>
                    <div class="min-w-0 flex-1 pt-3">
                        <NuxtLink
                            :to="category._path"
                            class="focus:outline-none"
                        >
                            <span class="absolute inset-0" aria-hidden="true" />
                            <h3
                                :style="{
                                    backgroundColor: category.color || 'black',
                                }"
                                class="
                                    text-white
                                    px-3
                                    py-1
                                    font-medium
                                    rounded-sm
                                    mb-2
                                "
                            >{{ category.title }}</h3>
                            <div
                                class="
                                    text-sm
                                    text-gray-800
                                    line-clamp-2
                                "
                            >{{ category.description }}</div>
                        </NuxtLink>
                    </div>
                </div>
            </div>
        </div>
    </ContentNavigation>
</div>
</template>

<script setup lang="ts">
import type { QueryBuilderParams } from '@nuxt/content/dist/runtime/types'

const title = 'Cesbo Help Center'

useHead({
    title,
})

// Only for SSR
if(process.server) {
    const absolutePageUrl = 'https://help.cesbo.com' + useRoute().fullPath
    const description = 'Welcome to the Cesbo Help Center: your guide to setting up Digital TV headend systems for Internet Providers, Broadcasters, and the Hospitality industry. Dive into our knowledge base for step-by-step tutorials, in-depth articles, and troubleshooting support to make the most out of your Cesbo solutions'
    const image = 'https://cdn.cesbo.com/help/og-image.png'

    useSeoMeta({
        description,

        twitterCard: 'summary_large_image',
        twitterSite: '@cesbo',
        twitterTitle: title,
        twitterDescription: description,
        twitterImage: image,

        ogType: 'website',
        ogUrl: absolutePageUrl,
        ogTitle: title,
        ogDescription: description,
        ogImage: image,
    })
}

const query: QueryBuilderParams = {
    sort: [
        { date: -1 },
    ],
}
</script>
