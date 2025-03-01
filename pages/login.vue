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
        <h1 class="text-2xl font-bold mb-6 text-brown text-center">Sign In to Beats Maker</h1>
        <p v-if="error" class="text-red-600 mb-4 text-center text-sm">{{ error }}</p>
        
        <form @submit.prevent="handleEmailLogin">
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
          </div>
          
          <button 
            type="submit" 
            class="btn btn-primary"
            :disabled="loading"
          >
            <span v-if="loading" class="absolute inset-0 flex items-center justify-center">
              <span class="w-5 h-5 border-2 border-offwhite/30 border-t-offwhite rounded-full animate-spin"></span>
            </span>
            <span :class="{ 'invisible': loading }">Sign in with Email</span>
          </button>
        </form>
        
        <div class="flex items-center my-6">
          <div class="flex-1 border-b border-sand"></div>
          <span class="px-3 text-brown text-sm">OR</span>
          <div class="flex-1 border-b border-sand"></div>
        </div>
        
        <GoogleSignInButton @error="handleGoogleError" />
        
        <p class="mt-6 text-center text-sm text-brown">
          Don't have an account? <NuxtLink to="/register" class="text-brown font-bold no-underline hover:underline">Sign up</NuxtLink>
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
const loading = ref(false)
const error = ref(null)

// If user is already logged in, redirect to home
watchEffect(() => {
  if (user.value) {
    router.push('/')
  }
})

async function handleEmailLogin() {
  try {
    loading.value = true
    error.value = null
    
    const { error: err } = await client.auth.signInWithPassword({
      email: email.value,
      password: password.value
    })
    
    if (err) throw err
    
    // Successful login will trigger the watchEffect above
  } catch (err) {
    error.value = err.message || 'An error occurred during sign in'
  } finally {
    loading.value = false
  }
}

function handleGoogleError(errorMessage) {
  error.value = errorMessage
}
</script>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #F5F0E8; /* Cream */
  padding: 20px;
}

.login-card {
  background: #FBF8F5; /* Offwhite */
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  padding: 40px;
  width: 100%;
  max-width: 400px;
}

h1 {
  margin-top: 0;
  margin-bottom: 24px;
  color: #544235; /* Brown */
  text-align: center;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
  color: #544235; /* Brown */
}

input {
  width: 100%;
  padding: 12px;
  border: 1px solid #B8A695; /* Taupe */
  border-radius: 4px;
  font-size: 16px;
  transition: border-color 0.3s;
}

input:focus {
  border-color: #544235; /* Brown */
  outline: none;
}

.divider {
  display: flex;
  align-items: center;
  margin: 24px 0;
}

.divider::before,
.divider::after {
  content: "";
  flex: 1;
  border-bottom: 1px solid #E5D9C9; /* Sand */
}

.divider span {
  padding: 0 10px;
  color: #544235; /* Brown */
  font-size: 14px;
}

.error {
  color: #e53e3e;
  margin-bottom: 16px;
  text-align: center;
  font-size: 14px;
}

.signup-link {
  margin-top: 24px;
  text-align: center;
  font-size: 14px;
  color: #544235; /* Brown */
}

.signup-link a {
  color: #544235; /* Brown */
  text-decoration: none;
  font-weight: bold;
}

.signup-link a:hover {
  text-decoration: underline;
}
</style> 