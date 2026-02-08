<template>
  <div class="user-card" :class="[`size-${size}`, { 'has-bio': showBio }]">
    <div class="avatar-container">
      <img :src="user.avatar" :alt="user.name" class="avatar">
    </div>
    <div class="user-info">
      <h4 class="name">{{ user.name }}</h4>
      <p class="email">{{ user.email }}</p>
      <p v-if="showBio" class="bio">{{ user.bio }}</p>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  user: {
    type: Object,
    required: true,
    validator: (value) => {
      return value.name && value.email && value.avatar
    }
  },
  showBio: {
    type: Boolean,
    default: true
  },
  size: {
    type: String,
    default: 'medium',
    validator: (value) => {
      return ['small', 'medium', 'large'].includes(value)
    }
  }
})
</script>

<style scoped>
.user-card {
  background: white;
  border-radius: 0.75rem;
  padding: 1rem;
  display: flex;
  align-items: center;
  gap: 1rem;
  border: 1px solid #f3f4f6;
  transition: all 0.2s ease;
}

.user-card:hover {
  border-color: #e5e7eb;
  background: #f9fafb;
}

.avatar-container {
  flex-shrink: 0;
}

.avatar {
  border-radius: 50%;
  object-fit: cover;
  background: #f3f4f6;
}

.user-info {
  flex-grow: 1;
  min-width: 0;
}

.name {
  margin: 0;
  font-size: 1rem;
  font-weight: 600;
  color: #111827;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.email {
  margin: 0;
  font-size: 0.8125rem;
  color: #6b7280;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.bio {
  margin: 0.5rem 0 0 0;
  font-size: 0.875rem;
  color: #4b5563;
  line-height: 1.4;
}

/* Size Variants */
.size-small {
  padding: 0.75rem;
  gap: 0.75rem;
}

.size-small .avatar {
  width: 2.5rem;
  height: 2.5rem;
}

.size-small .name {
  font-size: 0.875rem;
}

.size-medium {
  padding: 1rem;
}

.size-medium .avatar {
  width: 3.5rem;
  height: 3.5rem;
}

.size-large {
  padding: 1.5rem;
  flex-direction: column;
  text-align: center;
}

.size-large .avatar {
  width: 5rem;
  height: 5rem;
  margin-bottom: 0.5rem;
}

.size-large .name {
  font-size: 1.25rem;
}
</style>