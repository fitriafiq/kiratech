<template>
	<div v-if="isOpen" class="fixed inset-0 flex items-center justify-center z-50">
		<div class="absolute inset-0 bg-black bg-opacity-50" @click="closeModal"></div>
		<div class="bg-white rounded-lg p-8 max-w-lg w-full relative">
			<button @click="closeModal" class="absolute top-4 right-4 text-gray-500 hover:text-gray-700">
				<IconClose class="w-5 h-5" />
			</button>
			<div class="space-y-6 text-black">
				<h2 class="text-2xl font-bold text-gray-900">{{ user.name }}</h2>
				<div class="space-y-4">
					<div class="flex items-center">
						<p class="text-sm text-gray-500 w-24">Date</p>
						<p class="text-sm text-gray-900">{{ user.date }}</p>
					</div>
					<div class="flex items-center">
						<p class="text-sm text-gray-500 w-24">Gender</p>
						<p class="text-sm text-gray-900">{{ user.gender }}</p>
					</div>
					<div class="flex items-center">
						<p class="text-sm text-gray-500 w-24">Country</p>
						<p class="text-sm text-gray-900">{{ user.country }}</p>
					</div>
					<div class="flex items-center">
						<p class="text-sm text-gray-500 w-24">Email</p>
						<p class="text-sm text-gray-900">{{ user.email }}</p>
					</div>
					<div class="flex items-center">
						<p class="text-sm text-gray-500 w-24">Phone</p>
						<p class="text-sm text-gray-900">{{ user.phone }}</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { User } from '@/types/user'
import IconClose from '@/components/icons/IconClose.vue'

const isOpen = ref(false)

const user = ref<User>({
	id: '',
	date: '',
	name: '',
	gender: '',
	country: '',
	email: '',
	phone: ''
})

function openModal(userData: User) {
	user.value = userData
	isOpen.value = true
}

function closeModal() {
	isOpen.value = false
}

defineExpose({
	openModal
})
</script>