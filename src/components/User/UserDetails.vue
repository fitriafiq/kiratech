<template>
	<div class="bg-[#38bcdc] p-8 mb-16">
		<div class="container flex items-center gap-6">
			<img src="@/assets/Avatar.png" alt="John Doe" class="w-32 h-32 -mb-16">
			<div class="flex gap-8 mt-8">
				<div>
					<h1 class="text-3xl font-bold text-white">John Doe</h1>
					<p class="text-white opacity-80">Last online: 2 days ago</p>
				</div>
				<div class="flex gap-4 mt-4">
					<button
						class="bg-white text-[#38bcdc] border text-sm px-4 py-2 rounded-md flex items-center gap-2 hover:bg-[#38bcdc] hover:text-white transition-colors duration-200">
						<IconSend class="w-4 h-4" /> Send Message
					</button>
					<button
						class="bg-[#38bcdc] text-white border text-sm px-4 py-2 rounded-md flex items-center gap-2 hover:bg-white hover:text-[#38bcdc] transition-colors duration-200">
						<IconPlus class="w-4 h-4" /> Add Friend
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup lang="ts">
import IconSend from '@/components/icons/IconSend.vue'
import IconPlus from '@/components/icons/IconPlus.vue'
</script>