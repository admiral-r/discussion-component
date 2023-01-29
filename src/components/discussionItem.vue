<template>
    <div class="d-flex flex-column-reverse">
        <div v-for="(item, index) in discussions" :key="index" class="d-flex justify-content-between border-bottom p-3">
            <div class="d-flex flex-direction-column">
                <div class="discussion-item-pic">
                    <img v-if="item.user.avatar" :src="item.user.avatar"
                        class="object-fit-cover rounded-circle w-100 h-100" alt="profile-picture">
                    <h4 v-if="!item.user.avatar"
                        class="discussion-item-pic d-flex justify-content-center align-items-center rounded-circle bg-light-blue text-blue m-0">
                        {{ showNameInitials(item.user.name) }}</h4>
                </div>
                <div class="discussion-item-border">
                    <div :class="{ 'discussion-item-border-item': item.replies.length }"></div>
                </div>
            </div>
            <div class="w-100 ml-2">
                <div class="d-flex align-items-center">
                    <h4 class="m-0 mr-1">{{ item.user.name }}</h4>
                    <span class="discussion-item-time">{{ item.date }}</span>
                </div>
                <p class="discussion-item-text">{{ item.text }}</p>
                <div class="d-flex align-items-center mt-2">
                    <div class="discussion-item-like d-flex align-items-center pointer mr-3"
                        :class="{ 'discussion-item-like-active': item.iLikedIt }">
                        <img v-if="!item.iLikedIt" src="@/assets/svg/like-dark.svg" alt="like">
                        <img v-if="item.iLikedIt" src="@/assets/svg/like-white.svg" alt="like">
                        <span class="font-weight-bold ml-1 mt-1" :class="{ 'text-white': item.iLikedIt }">{{
                            item.likes
                        }}</span>
                    </div>
                    <h5 @click="showAddReply" class="discussion-item-reply pointer m-0">Reply</h5>
                </div>
                <replyItem :itemReplies="item.replies"></replyItem>
                <addReply v-if="reply"></addReply>
            </div>
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
            reply: false,
        }
    },
    methods: {
        showNameInitials(name) {
            return name.split(" ").map((n, i, a) => i === 0 || i + 1 === a.length ? n[0] : null).join("").toUpperCase();
        },
        showAddReply() {
            this.reply = !this.reply
        },
        addReply() {

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
