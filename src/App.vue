<template>
  <div class="container bg-white">
    <!---------- start the discussion ---------->
    <div>
      <startDiscussion></startDiscussion>
    </div>
    <!---------- discussion ---------->
    <div>
      <discussionItem></discussionItem>
    </div>
  </div>
</template>

<script>
import startDiscussion from "@/components/startDiscussion.vue"
import discussionItem from "@/components/discussionItem.vue"
export default {
  name: 'App',
  components: {
    startDiscussion,
    discussionItem
  }
}
</script>

<style lang="scss">

</style>
