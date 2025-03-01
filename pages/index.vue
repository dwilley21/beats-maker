<template>
  <div class="min-h-screen bg-brown-dark flex flex-col">
    <!-- Navigation -->
    <header class="py-4 px-6 md:px-12">
      <div class="max-w-7xl mx-auto flex justify-between items-center">
        <div class="flex items-center">
          <div class="text-offwhite text-2xl font-bold">Beats Maker</div>
        </div>
        <nav class="hidden md:flex items-center space-x-8">
          <NuxtLink to="/" class="text-offwhite hover:text-taupe-light transition-colors">Home</NuxtLink>
          <NuxtLink to="/app" class="text-offwhite hover:text-taupe-light transition-colors">App</NuxtLink>
          <NuxtLink to="/pricing" class="text-offwhite hover:text-taupe-light transition-colors">Pricing</NuxtLink>
          <NuxtLink to="/about" class="text-offwhite hover:text-taupe-light transition-colors">About</NuxtLink>
          <div class="text-offwhite bg-brown-light px-3 py-1 rounded text-sm">v2.1</div>
        </nav>
        <div class="flex items-center space-x-4">
          <NuxtLink v-if="!user" to="/login" class="text-offwhite hover:text-taupe-light transition-colors">Login</NuxtLink>
          <NuxtLink v-if="!user" to="/register" class="bg-taupe hover:bg-taupe-light text-brown font-medium px-6 py-2 rounded-full transition-colors flex items-center">
            Sign Up
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-2" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
            </svg>
          </NuxtLink>
          <div v-if="user" class="flex items-center">
            <UserAvatar :user="user" :size="32" />
            <button @click="handleSignOut" class="ml-4 text-offwhite hover:text-taupe-light transition-colors">Sign Out</button>
          </div>
        </div>
      </div>
    </header>

    <!-- Main content -->
    <main class="flex-1 flex flex-col">
      <!-- Hero section -->
      <div class="relative flex-1 flex flex-col items-center justify-center text-center px-6 py-16 md:py-32">
        <!-- Background curve -->
        <div class="absolute top-0 left-0 right-0 h-64 bg-brown overflow-hidden">
          <div class="absolute bottom-0 w-full h-24 bg-brown-dark rounded-t-[50%]"></div>
        </div>

        <!-- App logo -->
        <div class="relative z-10 mb-8">
          <div class="w-24 h-24 bg-gradient-to-br from-taupe to-brown rounded-xl flex items-center justify-center shadow-lg mb-4 mx-auto">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 text-offwhite" viewBox="0 0 20 20" fill="currentColor">
              <path d="M18 3a1 1 0 00-1.196-.98l-10 2A1 1 0 006 5v9.114A4.369 4.369 0 005 14c-1.657 0-3 .895-3 2s1.343 2 3 2 3-.895 3-2V7.82l8-1.6v5.894A4.37 4.37 0 0015 12c-1.657 0-3 .895-3 2s1.343 2 3 2 3-.895 3-2V3z" />
            </svg>
          </div>
          <div class="inline-flex items-center px-4 py-2 bg-taupe/20 rounded-full text-offwhite text-sm">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-2" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-12a1 1 0 10-2 0v4a1 1 0 00.293.707l2.828 2.829a1 1 0 101.415-1.415L11 9.586V6z" clip-rule="evenodd" />
            </svg>
            Updated: AI integrated
          </div>
        </div>

        <!-- Hero text -->
        <h1 class="relative z-10 text-4xl md:text-6xl font-bold text-offwhite mb-6 max-w-4xl">
          Do perfect, make perfect <span class="text-taupe">with Beats Maker</span>
        </h1>
        <p class="relative z-10 text-offwhite/80 text-xl mb-12 max-w-2xl">
          It's always feel good to create music perfectly
        </p>

        <!-- Platform buttons -->
        <div class="relative z-10 flex flex-wrap justify-center gap-4 mb-16">
          <button class="bg-brown text-offwhite px-8 py-3 rounded-md flex items-center hover:bg-brown-light transition-colors">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd" />
            </svg>
            macOS
          </button>
          <button class="bg-brown-light/50 text-offwhite px-8 py-3 rounded-md flex items-center hover:bg-brown-light transition-colors">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd" />
            </svg>
            Windows
          </button>
        </div>

        <!-- App preview -->
        <div class="relative z-10 w-full max-w-5xl mx-auto bg-brown-dark rounded-lg border border-taupe/20 shadow-xl overflow-hidden">
          <div class="flex items-center bg-brown-dark px-4 py-2 border-b border-taupe/20">
            <div class="flex space-x-2">
              <div class="w-3 h-3 rounded-full bg-red-500"></div>
              <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
              <div class="w-3 h-3 rounded-full bg-green-500"></div>
            </div>
            <div class="flex-1 flex justify-center">
              <div class="px-4 py-1 bg-brown-light/30 rounded text-offwhite/70 text-sm flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-2" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M12.586 4.586a2 2 0 112.828 2.828l-3 3a2 2 0 01-2.828 0 1 1 0 00-1.414 1.414 4 4 0 005.656 0l3-3a4 4 0 00-5.656-5.656l-1.5 1.5a1 1 0 101.414 1.414l1.5-1.5zm-5 5a2 2 0 012.828 0 1 1 0 101.414-1.414 4 4 0 00-5.656 0l-3 3a4 4 0 105.656 5.656l1.5-1.5a1 1 0 10-1.414-1.414l-1.5 1.5a2 2 0 11-2.828-2.828l3-3z" clip-rule="evenodd" />
                </svg>
                https://beatsmaker.app
              </div>
            </div>
          </div>
          <div class="p-6">
            <div class="flex flex-col md:flex-row gap-6">
              <div class="w-full md:w-1/3 bg-brown rounded-lg p-4">
                <div class="flex items-center mb-4">
                  <div class="w-8 h-8 bg-taupe rounded-full flex items-center justify-center text-brown font-bold">A</div>
                  <span class="ml-2 text-offwhite">Projects</span>
                </div>
                <div class="space-y-4">
                  <div class="bg-brown-light/30 p-3 rounded-lg">
                    <div class="flex justify-between items-center">
                      <span class="text-offwhite">New Beat</span>
                      <span class="bg-taupe text-brown text-xs px-2 py-1 rounded">90%</span>
                    </div>
                  </div>
                  <div class="bg-brown-light/30 p-3 rounded-lg">
                    <div class="flex justify-between items-center">
                      <span class="text-offwhite">Remix Project</span>
                      <span class="bg-taupe text-brown text-xs px-2 py-1 rounded">75%</span>
                    </div>
                  </div>
                  <div class="bg-brown-light/30 p-3 rounded-lg">
                    <div class="flex justify-between items-center">
                      <span class="text-offwhite">Collaboration</span>
                      <span class="bg-taupe text-brown text-xs px-2 py-1 rounded">100%</span>
                    </div>
                  </div>
                </div>
              </div>
              <div class="w-full md:w-2/3 bg-brown rounded-lg p-4">
                <div class="flex justify-between items-center mb-4">
                  <div class="text-offwhite font-medium">Beat Editor</div>
                  <div class="flex space-x-2">
                    <button class="bg-taupe text-brown px-2 py-1 rounded text-xs">Save</button>
                    <button class="bg-taupe-light text-brown px-2 py-1 rounded text-xs">Share</button>
                  </div>
                </div>
                <div class="bg-brown-dark/50 rounded-lg p-4 h-64 flex flex-col items-center justify-center">
                  <div class="w-full h-32 bg-brown-light/20 rounded-lg mb-4 flex items-center justify-center">
                    <div class="flex space-x-1">
                      <div class="w-1 h-12 bg-taupe rounded animate-pulse"></div>
                      <div class="w-1 h-16 bg-taupe rounded animate-pulse delay-100"></div>
                      <div class="w-1 h-8 bg-taupe rounded animate-pulse delay-200"></div>
                      <div class="w-1 h-20 bg-taupe rounded animate-pulse delay-300"></div>
                      <div class="w-1 h-10 bg-taupe rounded animate-pulse delay-400"></div>
                      <div class="w-1 h-14 bg-taupe rounded animate-pulse delay-500"></div>
                      <div class="w-1 h-6 bg-taupe rounded animate-pulse delay-600"></div>
                      <div class="w-1 h-18 bg-taupe rounded animate-pulse delay-700"></div>
                    </div>
                  </div>
                  <div class="flex space-x-4">
                    <button class="bg-taupe text-brown rounded-full w-12 h-12 flex items-center justify-center">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd" />
                      </svg>
                    </button>
                    <button class="bg-brown-light text-offwhite rounded-full w-12 h-12 flex items-center justify-center">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zM7 8a1 1 0 012 0v4a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v4a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                      </svg>
                    </button>
                    <button class="bg-brown-light text-offwhite rounded-full w-12 h-12 flex items-center justify-center">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8 7a1 1 0 00-1 1v4a1 1 0 001 1h4a1 1 0 001-1V8a1 1 0 00-1-1H8z" clip-rule="evenodd" />
                      </svg>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Features section (only shown if not logged in) -->
      <div v-if="!user" class="bg-brown-light py-16 px-6">
        <div class="max-w-7xl mx-auto">
          <h2 class="text-3xl font-bold text-offwhite text-center mb-12">Features</h2>
          
          <div class="grid md:grid-cols-3 gap-8">
            <div class="bg-brown p-6 rounded-lg shadow-md">
              <div class="text-offwhite mb-4 flex justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M18 3a1 1 0 00-1.196-.98l-10 2A1 1 0 006 5v9.114A4.369 4.369 0 005 14c-1.657 0-3 .895-3 2s1.343 2 3 2 3-.895 3-2V7.82l8-1.6v5.894A4.37 4.37 0 0015 12c-1.657 0-3 .895-3 2s1.343 2 3 2 3-.895 3-2V3z" />
                </svg>
              </div>
              <h3 class="text-xl font-semibold text-offwhite text-center mb-2">Professional Audio Tools</h3>
              <p class="text-offwhite/80 text-center">Create studio-quality beats with our professional-grade audio tools and effects</p>
            </div>
            
            <div class="bg-brown p-6 rounded-lg shadow-md">
              <div class="text-offwhite mb-4 flex justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M13 6a3 3 0 11-6 0 3 3 0 016 0zM18 8a2 2 0 11-4 0 2 2 0 014 0zM14 15a4 4 0 00-8 0v3h8v-3zM6 8a2 2 0 11-4 0 2 2 0 014 0zM16 18v-3a5.972 5.972 0 00-.75-2.906A3.005 3.005 0 0119 15v3h-3zM4.75 12.094A5.973 5.973 0 004 15v3H1v-3a3 3 0 013.75-2.906z" />
                </svg>
              </div>
              <h3 class="text-xl font-semibold text-offwhite text-center mb-2">Collaboration</h3>
              <p class="text-offwhite/80 text-center">Work with other musicians in real-time to create amazing tracks together</p>
            </div>
            
            <div class="bg-brown p-6 rounded-lg shadow-md">
              <div class="text-offwhite mb-4 flex justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V7z" clip-rule="evenodd" />
                </svg>
              </div>
              <h3 class="text-xl font-semibold text-offwhite text-center mb-2">AI-Powered</h3>
              <p class="text-offwhite/80 text-center">Let our AI help you create the perfect beat with intelligent suggestions and enhancements</p>
            </div>
          </div>
          
          <div class="mt-16 text-center">
            <NuxtLink to="/register" class="bg-taupe hover:bg-taupe-light text-brown font-medium px-8 py-3 rounded-full transition-colors inline-flex items-center">
              Get Started Now
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </NuxtLink>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
const client = useSupabaseClient()
const user = useSupabaseUser()
const router = useRouter()
const loading = ref(true)
const signupEmail = ref('')
const signupLoading = ref(false)
const signupError = ref(null)
const signupSuccess = ref(null)

// Check authentication status
onMounted(async () => {
  try {
    // Wait a moment to check if user is authenticated
    await new Promise(resolve => setTimeout(resolve, 500))
    loading.value = false
  } catch (error) {
    console.error('Error checking authentication:', error)
    loading.value = false
  }
})

async function handleEmailSignup() {
  try {
    signupLoading.value = true
    signupError.value = null
    signupSuccess.value = null
    
    // Validate email
    if (!signupEmail.value || !signupEmail.value.includes('@')) {
      signupError.value = 'Please enter a valid email address'
      return
    }
    
    // Store the email locally as a backup
    localStorage.setItem('signup_email', signupEmail.value)
    localStorage.setItem('signup_time', new Date().toISOString())
    
    // Try to store the email in the database
    try {
      // Only include the email_address column - created_at will be handled by Supabase defaults
      const { error: dbError } = await client
        .from('Email-Leads')
        .insert([
          { 
            email_address: signupEmail.value
            // Note: id and created_at are handled automatically by Supabase
          }
        ])
      
      if (dbError) {
        // Continue with signup even if database storage fails
        console.error('Error storing email in database:', dbError.message)
      }
    } catch (dbErr) {
      // Continue with signup even if database storage fails
      console.error('Exception storing email in database:', dbErr)
    }
    
    // Generate a random password (will be changed later)
    const tempPassword = Math.random().toString(36).slice(-10) + Math.random().toString(36).slice(-10)
    
    const { error } = await client.auth.signUp({
      email: signupEmail.value,
      password: tempPassword,
    })
    
    if (error) throw error
    
    signupSuccess.value = 'Success! Check your email to confirm your account.'
    signupEmail.value = ''
  } catch (err) {
    signupError.value = err.message || 'An error occurred. Please try again.'
  } finally {
    signupLoading.value = false
  }
}

function formatDate(dateString) {
  if (!dateString) return 'N/A'
  
  const date = new Date(dateString)
  return date.toLocaleString()
}

async function handleSignOut() {
  try {
    await client.auth.signOut()
    router.push('/')
  } catch (error) {
    console.error('Error signing out:', error)
  }
}
</script>

<style scoped>
@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

.animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

.delay-100 {
  animation-delay: 0.1s;
}

.delay-200 {
  animation-delay: 0.2s;
}

.delay-300 {
  animation-delay: 0.3s;
}

.delay-400 {
  animation-delay: 0.4s;
}

.delay-500 {
  animation-delay: 0.5s;
}

.delay-600 {
  animation-delay: 0.6s;
}

.delay-700 {
  animation-delay: 0.7s;
}
</style> 