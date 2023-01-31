<template>
    <div class="d-flex flex-column-reverse">
        <div v-for="(item, index) in discussions" :key="index"
            class="discussion-item-fade d-flex justify-content-between border-bottom p-3">
            <!---------------- avatar ---------------->
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
                <!---------------- user name and date---------------->
                <div class="d-flex align-items-center user-select-none">
                    <h4 class="m-0 mr-1">{{ item.user.name }}</h4>
                    <span class="discussion-item-time">{{ item.date }}</span>
                </div>
                <!---------------- text ---------------->
                <p class="discussion-item-text user-select-none">{{ item.text }}</p>
                <!---------------- like ---------------->
                <div class="d-flex align-items-center mt-2">
                    <div @click="getlikedItem(item.id, item.iLikedIt)"
                        class="discussion-item-like d-flex align-items-center pointer user-select-none mr-3"
                        :class="{ 'discussion-item-like-active': item.iLikedIt }">
                        <img v-if="!item.iLikedIt" src="@/assets/svg/like-dark.svg" alt="like">
                        <img v-if="item.iLikedIt" src="@/assets/svg/like-white.svg" alt="like">
                        <span class="font-weight-bold ml-1 mt-1" :class="{ 'text-white': item.iLikedIt }">{{
                            item.likes
                        }}</span>
                    </div>
                    <h5 @click.prevent="showAddReply(`itemReply${index}`)"
                        class="discussion-item-reply pointer user-select-none m-0">Reply
                    </h5>
                </div>
                <!---------------- reply item ---------------->
                <div>
                    <replyItem @likeAddedReply="likeAddedReply" :itemReplies="item.replies" :parentItemId="item.id">
                    </replyItem>
                </div>
                <!---------------- add reply ---------------->
                <div :ref="`itemReply${index}`" class="discussion-item-reply-hide">
                    <addReply @addReply="addReply" :parentItemId="item.id" :replyShow="`itemReply${index}`"></addReply>
                </div>
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
            discussionReplay: [],
        }
    },
    methods: {
        showNameInitials(name) {
            return name.split(" ").map((n, i, a) => i === 0 || i + 1 === a.length ? n[0] : null).join("").toUpperCase();
        },
        showAddReply(ref) {
            if (this.$refs[ref][0].classList.value === 'discussion-item-reply-show') {
                this.$refs[ref][0].classList.value = 'discussion-item-reply-hide'
            }
            else {
                this.$refs[ref][0].classList.value = 'discussion-item-reply-show'
            }
        },
        addReply(text, parentItemId, replyShow) {
            this.$refs[replyShow][0].classList.value = 'discussion-item-reply-hide'
            let lastId = this.discussions.slice(-1)[0].id
            if (text) {
                this.discussionReplay = {
                    id: lastId + 1,
                    date: new Date().getHours() + ":" + new Date().getMinutes(),
                    user: {
                        name: "James Marsden",
                        avatar: require('@/assets/images/profile-picture-3.jpg')
                    },
                    text: text,
                    likes: 0,
                    iLikedIt: false,
                }
                this.$emit("addReply", this.discussionReplay, parentItemId)
            }
        },
        getlikedItem(id, iLikedIt) {
            if (iLikedIt === false) {
                this.$emit("likeAdded", id)
            }
        },
        likeAddedReply(id, parentItemId) {
            this.$emit("likeAddedReply", id, parentItemId)
        },
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

    &-fade {
        -webkit-animation: discussion-item-fade .5s;
        animation: discussion-item-fade .5s;

        @-webkit-keyframes discussion-item-fade {
            0% {
                opacity: 0;
            }

            100% {
                opacity: 1;
            }
        }

        @keyframes discussion-item-fade {
            0% {
                opacity: 0;
            }

            100% {
                opacity: 1;
            }
        }
    }

    &-reply-hide {
        display: none !important;
    }

    &-reply-show {
        display: block !important;
    }
}
</style>
