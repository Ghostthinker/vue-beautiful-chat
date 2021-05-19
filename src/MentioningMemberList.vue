<template>
  <div v-if="filteredParticipants.length > 0" class="sc-mentioning-member-list">
    <transition-group name="slide-fade">
      <div
        v-for="user in filteredParticipants"
        :key="user.id"
        class="sc-mentioning-member-container"
        @click="mentionMember(user)"
      >
        <div class="sc-mentioning-member">
          <img alt="profile-img" :src="user.imageUrl" class="img-msg" />
          <label>{{ user.name }}</label>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: 'MentioningMemberList',
  props: {
    participants: {
      type: Array,
      required: true
    },
    searchText: {
      type: String,
      required: true
    }
  },
  computed: {
    filteredParticipants() {
      return this.participants.filter(
        (par) => par.name.toLowerCase().includes(this.searchText.toLowerCase()) && !par.deleted
      )
    }
  },
  methods: {
    mentionMember(user) {
      this.$emit('mentionMember', user)
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
  overflow-x: hidden;
  border-top-left-radius: 7px;
  border-top-right-radius: 7px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  flex-shrink: 0;
}

.sc-mentioning-member-container {
  border-bottom: 1px solid;
  border-color: #eaeaea;
  display: flex;
  align-items: center;
  height: 38px;
  flex-shrink: 0;
}

.img-msg {
  border-radius: 50%;
  width: 20px;
  height: 20px;
}

.sc-mentioning-member {
  cursor: pointer;
  width: 100%;
}

label {
  margin-bottom: 0 !important;
  padding-left: 8px;
}

.slide-fade-enter-active {
  transition: all 0.4s ease;
}
.slide-fade-leave-active {
  transition: all 0.4s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter,
.slide-fade-leave-to {
  transform: translateX(200px);
  opacity: 0.8;
}
</style>
