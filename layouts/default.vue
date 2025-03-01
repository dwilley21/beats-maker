<template>
  <div class="flex flex-col min-h-screen">
    <main class="flex-1">
      <slot />
    </main>
    
    <footer class="bg-brown-dark py-6 border-t border-taupe/10">
      <div class="max-w-7xl mx-auto px-6 flex flex-col md:flex-row justify-between items-center">
        <div class="text-offwhite/60 text-sm mb-4 md:mb-0">
          &copy; {{ new Date().getFullYear() }} Beats Maker. All rights reserved.
        </div>
        <div class="flex space-x-6">
          <NuxtLink to="/terms" class="text-offwhite/60 hover:text-offwhite text-sm transition-colors">Terms</NuxtLink>
          <NuxtLink to="/privacy" class="text-offwhite/60 hover:text-offwhite text-sm transition-colors">Privacy</NuxtLink>
          <NuxtLink to="/contact" class="text-offwhite/60 hover:text-offwhite text-sm transition-colors">Contact</NuxtLink>
          <NuxtLink to="/debug" class="text-offwhite/60 hover:text-offwhite text-sm transition-colors">Debug</NuxtLink>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
const client = useSupabaseClient()
const user = useSupabaseUser()
const router = useRouter()

async function handleSignOut() {
  try {
    await client.auth.signOut()
    router.push('/')
  } catch (error) {
    console.error('Error signing out:', error)
  }
}
</script> 