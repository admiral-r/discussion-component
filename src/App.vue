<template>
  <div class="container bg-white">
    <!---------- start the discussion ---------->
    <div>
      <addDiscussion @addDiscussionText="addDiscussionText"></addDiscussion>
    </div>
    <!---------- discussion ---------->
    <div>
      <discussionItem @addReply="addReply" @likeAdded="likeAdded" @likeAddedReply="likeAddedReply"
        :discussions="discussions">
      </discussionItem>
    </div>
  </div>
</template>

<script>
import addDiscussion from "@/components/addDiscussion.vue"
import discussionItem from "@/components/discussionItem.vue"
export default {
  name: 'App',
  components: {
    addDiscussion,
    discussionItem
  },
  data() {
    return {
      discussions: [
        {
          id: 0,
          date: '05:12',
          user: {
            name: "Amir Rz",
          },
          text: "I enjoyed doing this project. Thanks for sharing this repository with me",
          likes: 2,
          iLikedIt: false,
          replies: []
        },
        {
          id: 1,
          date: '10:14',
          user: {
            name: "Savannah Nguyen"
          },
          text: "We have just published the first campaign. Let's see the results in the 5 days and we will iterate on this.",
          likes: 50,
          iLikedIt: false,
          replies: []
        },
        {
          id: 2,
          date: '10:30',
          user: {
            name: "Marvin McKinney",
            avatar: require('@/assets/images/profile-picture-2.jpg')
          },
          text: "The first compaign went smoothly. Please make sure to see all attachments with the results to understand the flow.",
          likes: 2,
          iLikedIt: false,
          replies: []
        },
        {
          id: 3,
          date: '11:32',
          user: {
            name: "Bessie Cooper",
            avatar: require('@/assets/images/profile-picture-4.jpg')
          },
          text: "I think for our second compaign we can try to target a different audience. How does it sound for you?",
          likes: 2,
          iLikedIt: false,
          replies: [
            {
              id: 0,
              date: '15:14',
              user: {
                name: "Marvin McKinney",
                avatar: require('@/assets/images/profile-picture-2.jpg')
              },
              text: "Yes, that sounds good! I can think about this tomorrow. Then do we plan to start that compaign?",
              likes: 3,
              iLikedIt: false,
            },
            {
              id: 1,
              date: '16:50',
              user: {
                name: "Bessie Cooper",
                avatar: require('@/assets/images/profile-picture-4.jpg')
              },
              text: "We plan to run the compaign on Friday - as far as I know. Do you think you will get this done by Thursday @Marvin?",
              likes: 0,
              iLikedIt: false,
            }
          ]
        },
      ]
    }
  },
  methods: {
    addDiscussionText(discussion) {
      this.discussions.push(discussion);
    },
    likeAdded(id) {
      for (let item in this.discussions) {
        if (this.discussions[item].id === id) {
          this.discussions[item].iLikedIt = true
          this.discussions[item].likes++
        }
      }
    },
    likeAddedReply(childId, parentId) {
      for (let item in this.discussions) {
        if (this.discussions[item].id === parentId) {
          for (let childItem in this.discussions[item].replies) {
            if (this.discussions[item].replies[childItem].id === childId) {
              this.discussions[item].replies[childItem].iLikedIt = true
              this.discussions[item].replies[childItem].likes++
            }
          }
        }
      }
    },
    addReply(discussionReplay, parentItemId) {
      for (let item in this.discussions) {
        if (this.discussions[item].id === parentItemId) {
          this.discussions[item].replies.push(discussionReplay);
        }
      }
    },
  },
}
</script>

<style lang="scss">

</style>
