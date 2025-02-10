<template>
	<div class="container my-8">
		<div class="mb-4 flex justify-between items-center">
			<input v-model="searchQuery" type="text" placeholder="Search users..."
				class="px-4 py-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-[#38bcdc] w-64 text-black" />
			<button :disabled="isLoading" @click="handleRefresh"
				class="bg-[#38bcdc] hover:bg-[#2ca7c7] text-white px-4 py-2 rounded flex gap-2 disabled:opacity-50 disabled:cursor-not-allowed transition-colors duration-200 flex items-center">
				<IconRefresh class="w-4 h-4" /> Refresh
			</button>
		</div>
		<table class="w-full mt-10">
			<thead>
				<tr class="grid grid-cols-5 w-full px-6 pb-3">
					<th class="text-xs font-medium text-gray-400 text-left">Date</th>
					<th class="text-xs font-medium text-gray-400 text-left">Name</th>
					<th class="text-xs font-medium text-gray-400 text-left">Gender</th>
					<th class="text-xs font-medium text-gray-400 text-left">Country</th>
					<th class="text-xs font-medium text-gray-400 text-right">Email
					</th>
				</tr>
			</thead>
			<tbody class="bg-white space-y-4">
				<tr v-for="user in filteredUsers" :key="user.id"
					class="group border-2 border-white shadow-md rounded-md grid grid-cols-5 w-full hover:border-[#38bcdc] transition-all duration-200 p-6 cursor-pointer"
					@click="openModal(user)">
					<td class="text-sm text-gray-500 text-left">{{ user.date }}</td>
					<td class="text-sm font-bold group-hover:text-[#38bcdc] text-gray-900 text-left">{{ user.name }}
					</td>
					<td class="text-sm text-gray-500 group-hover:text-gray-900 text-left">{{ user.gender }}</td>
					<td class="text-sm font-medium text-gray-900 text-left">{{ user.country }}</td>
					<td class="text-sm text-gray-500 text-right">{{ user.email }}</td>
				</tr>
			</tbody>
		</table>
		<div class="flex justify-between items-center mt-4">
			<div class="text-sm text-gray-500">
				Showing page: {{ currentPage }}
			</div>
			<div class="flex gap-2">
				<button @click="previousPage" :disabled="currentPage === 1 || isLoading"
					class="bg-[#38bcdc] hover:bg-[#2ca7c7] px-4 py-2 text-white rounded-md disabled:opacity-50 disabled:cursor-not-allowed  transition-colors duration-200">
					Previous
				</button>
				<button @click="nextPage" :disabled="isLoading"
					class="bg-[#38bcdc] hover:bg-[#2ca7c7] px-4 py-2 text-white rounded-md disabled:opacity-50 disabled:cursor-not-allowed transition-colors duration-200">
					Next
				</button>
			</div>
		</div>
	</div>
	<UserModal ref="modalRef" />
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import axios from 'axios'
import IconRefresh from '@/components/icons/IconRefresh.vue'
import UserModal from '@/components/User/UserModal.vue'
import type { User } from '@/types/user'

const users = ref<User[]>([])
const isLoading = ref(false)
const modalRef = ref(null)

const searchQuery = ref('')
const currentPage = ref(1)
const itemsPerPage = 20

const filteredUsers = computed(() => {
	const query = searchQuery.value.toLowerCase()

	return users.value.filter(user =>
		user.name.toLowerCase().includes(query) ||
		user.email.toLowerCase().includes(query) ||
		user.country.toLowerCase().includes(query)
	)
})

async function fetchUsers() {
	try {
		isLoading.value = true

		const response = await axios.get(`https://randomuser.me/api/?page=${currentPage.value}&results=${itemsPerPage}`)

		users.value = response.data.results.map((user: any) => ({
			id: user.id.value,
			date: new Date(user.registered.date).toLocaleDateString('en-GB', { month: 'short', day: '2-digit', year: 'numeric' }),
			name: `${user.name.first} ${user.name.last}`,
			gender: user.gender.charAt(0).toUpperCase() + user.gender.slice(1),
			country: user.location.country,
			email: user.email,
			phone: user.phone,
		}))
	} catch (error) {
		console.error('Error fetching users:', error)
	} finally {
		isLoading.value = false
		searchQuery.value = ''
	}
}

onMounted(() => {
	fetchUsers()
})

function handleRefresh() {
	fetchUsers()
}

function openModal(user: User) {
	modalRef.value?.openModal(user)
}

function nextPage() {
	currentPage.value++
	fetchUsers()
}

function previousPage() {
	if (currentPage.value > 1) {
		currentPage.value--
		fetchUsers()
	}
}
</script>