<template>
    <div class="d-flex justify-content-between align-items-center border-bottom bg-light-silver p-3">
        <div>
            <div class="add-discussion-pic mr-2">
                <img src="@/assets/images/profile-picture-3.jpg" class="object-fit-cover rounded-circle w-100 h-100"
                    alt="profile-picture">
            </div>
        </div>
        <input @keyup.enter="addDiscussionText" v-model="discussionText" class="form-control" type="text"
            placeholder="start a discussion">
    </div>
</template>

<script>
export default {
    name: 'addDiscussion',
    data() {
        return {
            discussionText: null,
            discussion: [],
        }
    },
    methods: {
        addDiscussionText() {
            if (this.discussionText) {
                this.discussion = {
                    date: new Date().getHours() + ":" + new Date().getMinutes(),
                    user: {
                        name: "Bryan Cranston",
                        avatar: require('@/assets/images/profile-picture-3.jpg')
                    },
                    text: this.discussionText,
                    likes: 0,
                    iLikedIt: false,
                    replies: []
                }
                this.$emit("addDiscussionText", this.discussion)
                this.discussionText = null
            }
        }
    },
}
</script>

<style lang="scss">
.add-discussion {
    &-pic {
        width: 55px;
        height: 55px;
    }
}
</style>
