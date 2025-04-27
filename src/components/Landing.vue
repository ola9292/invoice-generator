<script setup>
const emit = defineEmits(['toggle-start'])

const startCreating = () => {
  emit('toggle-start')
}
</script>
<template>
 <div class="landing-container">
    <div class="content">
      <h1 class="title">Create Beautiful Invoices Effortlessly</h1>
      <p class="subtitle">
        Simplify your billing process with our easy-to-use invoice generator. 
        Professional invoices in minutes, no design skills needed.
      </p>
      <button class="cta-button" @click="startCreating">
        Start Creating 🚀
      </button>
    </div>


    <!-- Footer -->
    <!-- <footer class="footer">
      <p>© 2025 InvoiceHero. All rights reserved.</p>
    </footer> -->
  </div>
</template>



<style scoped>
.landing-container {
  height: 100vh;
  width: 100%;
  background: linear-gradient(135deg, #74ebd5 0%, #ACB6E5 100%);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  box-sizing: border-box;
}

.content {
  text-align: center;
  max-width: 600px;
  background: white;
  padding: 3rem 2rem;
  border-radius: 20px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 1rem;
  font-weight: bold;
}

.subtitle {
  font-size: 1.2rem;
  color: #666;
  margin-bottom: 2rem;
  line-height: 1.6;
}

.cta-button {
  background-color: #4F46E5;
  color: white;
  font-size: 1.1rem;
  padding: 0.8rem 2rem;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.cta-button:hover {
  background-color: #4338CA;
}
</style>