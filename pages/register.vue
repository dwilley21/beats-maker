<template>
  <div class="min-h-screen bg-cream flex flex-col">
    <!-- Navigation -->
    <header class="py-4 px-6 md:px-12 bg-brown">
      <div class="max-w-7xl mx-auto flex justify-between items-center">
        <div class="flex items-center">
          <NuxtLink to="/" class="text-offwhite text-2xl font-bold">Beats Maker</NuxtLink>
        </div>
        <nav class="hidden md:flex items-center space-x-8">
          <NuxtLink to="/" class="text-offwhite hover:text-taupe-light transition-colors">Home</NuxtLink>
        </nav>
      </div>
    </header>

    <div class="flex-1 flex justify-center items-center p-5">
      <div class="bg-offwhite rounded-lg shadow-md p-10 w-full max-w-md">
        <h1 class="text-2xl font-bold mb-6 text-brown text-center">Create Account</h1>
        <p v-if="error" class="text-red-600 mb-4 text-center text-sm">{{ error }}</p>
        <p v-if="success" class="text-green-600 mb-4 text-center text-sm">{{ success }}</p>
        
        <form @submit.prevent="handleRegister">
          <div class="mb-5">
            <label for="email" class="form-label">Email</label>
            <input 
              id="email"
              v-model="email" 
              type="email" 
              placeholder="your@email.com" 
              class="form-input"
              required
            />
          </div>
          
          <div class="mb-5">
            <label for="password" class="form-label">Password</label>
            <input 
              id="password"
              v-model="password" 
              type="password" 
              placeholder="••••••••" 
              class="form-input"
              required
            />
            <p class="text-xs text-brown/70 mt-1">Password must be at least 6 characters</p>
          </div>
          
          <div class="mb-5">
            <label for="confirmPassword" class="form-label">Confirm Password</label>
            <input 
              id="confirmPassword"
              v-model="confirmPassword" 
              type="password" 
              placeholder="••••••••" 
              class="form-input"
              required
            />
          </div>
          
          <button 
            type="submit" 
            class="btn btn-primary relative"
            :disabled="loading"
          >
            <span v-if="loading" class="absolute inset-0 flex items-center justify-center">
              <span class="w-5 h-5 border-2 border-offwhite/30 border-t-offwhite rounded-full animate-spin"></span>
            </span>
            <span :class="{ 'invisible': loading }">Create Account</span>
          </button>
        </form>
        
        <div class="flex items-center my-6">
          <div class="flex-1 border-b border-sand"></div>
          <span class="px-3 text-brown text-sm">OR</span>
          <div class="flex-1 border-b border-sand"></div>
        </div>
        
        <GoogleSignInButton 
          label="Sign up with Google" 
          @error="handleGoogleError" 
        />
        
        <p class="mt-6 text-center text-sm text-brown">
          Already have an account? <NuxtLink to="/login" class="text-brown font-bold no-underline hover:underline">Sign in</NuxtLink>
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient()
const user = useSupabaseUser()
const router = useRouter()

const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const loading = ref(false)
const error = ref(null)
const success = ref(null)

// If user is already logged in, redirect to home
watchEffect(() => {
  if (user.value) {
    router.push('/')
  }
})

async function handleRegister() {
  try {
    // Reset messages
    error.value = null
    success.value = null
    
    // Validate passwords match
    if (password.value !== confirmPassword.value) {
      error.value = 'Passwords do not match'
      return
    }
    
    // Validate password length
    if (password.value.length < 6) {
      error.value = 'Password must be at least 6 characters'
      return
    }
    
    loading.value = true
    
    const { error: err, data } = await client.auth.signUp({
      email: email.value,
      password: password.value
    })
    
    if (err) throw err
    
    // Check if email confirmation is required
    if (data?.user && data?.session) {
      // Auto sign-in (no email confirmation required)
      // The watchEffect will handle the redirect
    } else {
      // Email confirmation required
      success.value = 'Registration successful! Please check your email to confirm your account.'
      email.value = ''
      password.value = ''
      confirmPassword.value = ''
    }
  } catch (err) {
    error.value = err.message || 'An error occurred during registration'
  } finally {
    loading.value = false
  }
}

function handleGoogleError(errorMessage) {
  error.value = errorMessage
}
</script> 