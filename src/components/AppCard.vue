<script lang="ts" setup>
import MailIcon from './MailIcon.vue'
import { computed } from 'vue'

/**
 * Props for the AppUser component
 * @typedef {object} AppUser
 * @property {object} user - The user object
 */
const props = defineProps({
	user: {
		type: Object,
		default: () => {}
	}
})

/**
 * Computed property that calculates the full name of the user
 * @type {ComputedRef<string>}
 */
const fullName = computed(() => props.user.name.first + ' ' + props.user.name.last)
</script>

<template>
	<div class="max-w-sm bg-white shadow-lg rounded-lg overflow-hidden my-12 mx-auto">
		<img class="w-full h-56 object-cover object-center" :src="user.picture.large" alt="avatar" />
		<div class="py-4 px-6">
			<h1 class="text-2xl font-semibold text-gray-800">
				{{ fullName }}
			</h1>
			<div class="flex items-center mt-4 text-gray-700">
				<MailIcon />
				<h2 class="px-2 text-sm">
					{{ user.email }}
				</h2>
			</div>
		</div>
	</div>
</template>
