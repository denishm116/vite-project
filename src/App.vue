<script setup>
/**
 *   This script sets up the functionality to fetch and display a list of users from the randomuser.me API.
 * 	It initializes the AppLoader and AppCard components, and handles scroll events for lazy loading.
 */
import AppLoader from './components/AppLoader.vue'
import { ref, onMounted } from 'vue'
import AppCard from './components/AppCard.vue'

/**
 * The number of users to fetch per page
 * @type {number}
 */
const perPage = 5

/**
 * The current page number
 * @type {number}
 */
const page = 1

/**
 * A reference to the array of users fetched from the API
 * @type {ref}
 */
const users = ref([])

/**
 * Asynchronous function to fetch users from the API
 * @param {number} page - The page number to fetch
 * @param {number} perPage - The number of users to fetch per page
 * @returns {Promise<void>}
 */
const fetchUsers = async (page, perPage) => {
	const response = await fetch(`https://randomuser.me/api/?page=${page}&results=${perPage}`)

	if (response.ok) {
		const data = await response.json()
		users.value = users.value.concat(data.results)
		page++
	}
}

/**
 * Event handler to handle scroll events and trigger fetching more users
 * @returns {void}
 */
const scrollHandler = () => {
	const loadingObserver = new IntersectionObserver((entries) => {
		entries.forEach((entry) => {
			if (entry.isIntersecting) {
				fetchUsers(page, perPage)
			}
		})
	})

	loadingObserver.observe(document.querySelector('.loader'))
}

onMounted(() => scrollHandler())
</script>

<template>
	<AppCard v-for="user in users" :key="user.id" :user="user" />
	<AppLoader class="loader" />
</template>
