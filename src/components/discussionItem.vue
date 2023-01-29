<template>
    <div class="d-flex justify-content-between border-bottom p-3">
        <div class="d-flex flex-direction-column">
            <div class="discussion-item-pic">
                <img src="@/assets/images/profile-picture-2.jpg" class="object-fit-cover rounded-circle w-100 h-100"
                    alt="profile-picture">
            </div>
            <div class="discussion-item-border">
                <div class="discussion-item-border-item"></div>
            </div>
        </div>
        <div class="w-100 ml-2">
            <div class="d-flex align-items-center">
                <h4 class="m-0 mr-1">Bessie Cooper</h4>
                <span class="discussion-item-time">3h ago</span>
            </div>
            <p class="discussion-item-text">I think for our second campaign we can try to target a different audience.
                How does it sound for you?</p>
            <div class="d-flex align-items-center mt-2">
                <div @click="iLikedIt" class="discussion-item-like d-flex align-items-center pointer mr-3"
                    :class="{ 'discussion-item-like-active': like }">
                    <img v-if="!like" src="@/assets/svg/like-dark.svg" alt="like">
                    <img v-if="like" src="@/assets/svg/like-white.svg" alt="like">
                    <span class="font-weight-bold ml-1 mt-1" :class="{ 'text-white': like }">2</span>
                </div>
                <h5 @click="showAddReply" class="discussion-item-reply pointer m-0">Reply</h5>
            </div>
            <replyItem></replyItem>
            <addReply v-if="reply"></addReply>
        </div>
    </div>
</template>

<script>
import replyItem from "@/components/replyItem.vue"
import addReply from "@/components/addReply.vue"
export default {
    name: 'discussionItem',
    components: {
        replyItem,
        addReply
    },
    props: {
        discussions: {
            type: Array,
        },
    },
    data() {
        return {
            like: false,
            reply: false,
        }
    },
    methods: {
        showAddReply() {
            this.reply = !this.reply
        },
        iLikedIt() {
            this.like = !this.like
        }
    },
}
</script>

<style lang="scss">
.discussion-item {
    &-pic {
        width: 55px;
        height: 55px;
    }

    &-text {
        margin: 8px 0 !important;
        color: #6c757d;
    }

    &-time {
        color: #a2aac0;
        font-size: 1.1rem;
    }

    &-reply {
        color: #5885ed;
    }

    &-like {
        background-color: #eff0f7;
        padding: 1px 16px 5px 14px;
        border-radius: 2rem;

        &-active {
            background-color: #235ee7 !important;
        }
    }

    &-border {
        width: 2px;
        height: 100%;
        padding: 15px 26px 0 26px;


        &-item {
            background-color: #eeeeee;
            height: 100%;
            width: 100%;
        }
    }
}
</style>
