<template>
  <div class="profile-desc">
    <v-app id="profiledesc">
      <v-card class="mx-auto" outlined id="desc-card">
        <v-list-item three-line>
          <v-list-item-content>
            <div class="overline mb-4">Profile</div>
            <v-list-item-title class="headline mb-3">NAME: {{userDetails.data.name}}</v-list-item-title>
            <br />
            <br />
            <br />
            <div class="follower">
              <span class="border">Followers: {{userDetails.data.followersCount}}</span>
              <span class="border">Following: {{userDetails.data.followingCount}}</span>
            </div>
            <br />
            <v-list-item-subtitle id="subtitle">E-mail: {{userDetails.data.userEmail}}</v-list-item-subtitle>
            <v-list-item-subtitle id="subtitle">Score: {{userDetails.data.score}}</v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-avatar tile size="200" color="grey">
            <img
              src="https://cdn.business2community.com/wp-content/uploads/2017/08/blank-profile-picture-973460_640.png"
              alt="John"
            />
          </v-list-item-avatar>
        </v-list-item>
        <v-card-actions>
          <!-- <v-btn
            v-if="userCheck==true"
            text
            class="follow-button"
            :disabled="isFollowed"
            @click.once="followUser"
          >Follow</v-btn> -->
          <div class="my-2">
              <v-btn small color="primary" v-if="userCheck==true" :disabled="isFollowed"
            @click.once="followUser" dark>Follow</v-btn>
            </div>
        </v-card-actions>
      </v-card>
    </v-app>
  </div>
</template>

<script>
export default {
  data() {
    return {
      myProfile: false,
      userCheck: true,
      isFollowed: false
    };
  },
  props: ["userDetails"],
  mounted() {
    let localUserId = localStorage.getItem("userId");
    let userId = this.$route.params.userId;
    if (localUserId == userId) {
      this.userCheck = false;
    }
  },
  methods: {
    followUser() {
      this.isFollowed = true;
      this.$store.dispatch("sendFollowUserRequest", this.$route.params.userId);
    }
  }
};
</script>

<style scoped>
.border {
  border: 1px solid #b74545;
  margin: 5px;
  padding: 5px;
  font-family: monospace;
}
#subtitle {
  position: relative;
  top: 9px;
}
#desc-card:hover {
  box-shadow: 4px 4px 15px 0px black;
}
.profile-desc {
  height: 290px;
}
.follow-button {
  width: 30%;
}
#desc-card {
  width: 74%;
}
#profiledesc {
  background-color: #eaeded;
}
.follow-button:hover {
  color: #83677b;
}
</style>