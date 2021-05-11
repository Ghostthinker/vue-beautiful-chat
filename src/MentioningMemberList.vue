<template>
  <div class="sc-mentioning-member-list">
    <div v-for="(user, idx) in participants" :key="idx" class="sc-mentioning-member-container">
      <img :src="user.imageUrl" class="img-msg" />
      <label>{{ user.name }}</label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MentioningMemberList',
  props: {
    participants: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.sc-mentioning-member-list {
  padding: 0.5em 1em 0 1em;
  background-color: #f4f7f9;
  max-height: 200px;
  overflow-y: auto;
  border-top-left-radius: 7px;
  border-top-right-radius: 7px;
}

.sc-mentioning-member-container {
  height: 38px;
  border-bottom: 1px solid;
  border-color: #eaeaea;
  display: flex;
  align-items: center;
}

.img-msg {
  border-radius: 50%;
  width: 20px;
  height: 20px;
}

label {
  margin-bottom: 0 !important;
  padding-left: 8px;
}
</style>
