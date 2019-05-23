<template>
  <div>
    <div class="ui one column divided grid">
      <div class="column">
        <p>Hi! before you start to use this app, we want to know your name and some information about you.</p>
      </div>
      <div class='ui centered card'>
        <div class='content'>
          <div class='ui form'>
            <div class='field'>
              <label>Name</label>
              <input v-model="nameText" type='text'>
            </div>
            <div class='field'>
              <label>Nickname</label>
              <input v-model="nicknameText" type='text'>
            </div>
            <div class='field'>
              <label>Mail</label>
              <input v-model="mailText" type='text'>
            </div>
            <div class='ui two button attached buttons'>
              <button class='ui basic blue button' v-on:click="sendForm()">
                Submit
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      nameText: '',
      nicknameText: '',
      mailText: '',
    };
  },
  methods: {
    sendForm() {
      this.$emit('complete-ftux', {
        name: this.nameText,
        nickname: this.nicknameText,
        mail: this.mailText,
      });
    },
  },
};
</script>
