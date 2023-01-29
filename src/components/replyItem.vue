<template>
    <div class="d-flex justify-content-between mt-3">
        <div>
            <div class="reply-item-pic mr-2">
                <img src="@/assets/images/profile-picture-4.jpg" class="object-fit-cover rounded-circle w-100 h-100"
                    alt="profile-picture">
            </div>
        </div>
        <div class="w-100">
            <div class="d-flex align-items-center">
                <h4 class="m-0 mr-1">Bessie Cooper</h4>
                <span class="reply-item-time">3h ago</span>
            </div>
            <p class="reply-item-text">I think for our second campaign we can try to target a different audience.
                How does it sound for you?</p>
            <div class="d-flex mt-2">
                <div class="reply-item-like d-flex align-items-center pointer mr-3 "
                    :class="{ 'reply-item-like-active': like }">
                    <img v-if="!like" src="@/assets/svg/like-dark.svg" alt="like">
                    <img v-if="like" src="@/assets/svg/like-white.svg" alt="like">
                    <span class="font-weight-bold ml-1 mt-1" :class="{ 'text-white': like }">2</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'replyItem',
    data() {
        return {
            like: false,
        }
    },
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
