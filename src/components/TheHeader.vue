<template>
	<div class="container flex justify-between items-center p-4 bg-white">
		<div class="flex items-center gap-4">
			<img src="@/assets/Logo.png" alt="Kiratech Logo" class="h-14">
		</div>
		<div class="flex items-center gap-4">
			<IconBell class="w-5 text-black cursor-pointer"/>
			<IconGear class="w-5 text-black cursor-pointer"/>
			<IconSignOut class="w-5 text-black cursor-pointer"/>
		</div>
	</div>
</template>

<script setup lang="ts">
import IconBell from '@/components/icons/IconBell.vue'
import IconGear from '@/components/icons/IconGear.vue'
import IconSignOut from '@/components/icons/IconSignOut.vue'
</script>