<template>
    <div v-for="(item, index) in itemReplies" :key="index" class="d-flex justify-content-between mt-3">
        <div>
            <div class="reply-item-pic mr-2">
                <img v-if="item.user.avatar" :src="item.user.avatar" class="object-fit-cover rounded-circle w-100 h-100"
                    alt="profile-picture">
                <h4 v-if="!item.user.avatar"
                    class="reply-item-pic d-flex justify-content-center align-items-center rounded-circle bg-light-blue text-blue m-0">
                    {{ showNameInitials(item.user.name) }}</h4>
            </div>
        </div>
        <div class="w-100">
            <div class="d-flex align-items-center">
                <h4 class="m-0 mr-1">{{ item.user.name }}</h4>
                <span class="reply-item-time">{{ item.date }}</span>
            </div>
            <p class="reply-item-text">{{ item.text }}</p>
            <div class="d-flex mt-2">
                <div class="reply-item-like d-flex align-items-center pointer mr-3 "
                    :class="{ 'reply-item-like-active': item.iLikedIt }">
                    <img v-if="!item.iLikedIt" src="@/assets/svg/like-dark.svg" alt="like">
                    <img v-if="item.iLikedIt" src="@/assets/svg/like-white.svg" alt="like">
                    <span class="font-weight-bold ml-1 mt-1"
                        :class="{ 'text-white': item.iLikedIt }">{{ item.likes }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'replyItem',
    props: {
        itemReplies: {
            type: Array,
        },
    },
    data() {
        return {

        }
    },
    methods: {
        showNameInitials(name) {
            return name.split(" ").map((n, i, a) => i === 0 || i + 1 === a.length ? n[0] : null).join("").toUpperCase();
        },
    }
}
</script>

<style lang="scss">
.reply-item {
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

}
</style>
