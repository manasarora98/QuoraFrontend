<template>
  <div class="user-profile">
    <UserHeader></UserHeader>
    <OrganizationDescription :organizationDetails="getOrganizationDetails"></OrganizationDescription>
    <organizationProfileFeed :organizationDetails="getOrganizationDetails"></organizationProfileFeed>
  </div>
</template>

<script>
// import ProfileDescription from "@/components/ProfileDescription.vue";
import organizationProfileFeed from "@/components/organizationProfileFeed.vue";
import UserHeader from "@/components/UserHeader.vue";
import OrganizationDescription from "@/components/OrganizationDescription.vue";
import { mapGetters } from "vuex";

export default {
  name: "Profile",
  components: {
    organizationProfileFeed,
    UserHeader,
    OrganizationDescription
  },
  created() {
    
    let organizationId = this.$route.params.organizationId
    this.$store.dispatch("getOrganizationProfileDetails",organizationId)
  },
  computed: {
    ...mapGetters(["getOrganizationDetails"])
  }
};
</script>

<style scoped>
.user-profile {
  background-color: #c38d9e;
}
</style>