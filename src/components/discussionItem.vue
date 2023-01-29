<template>
    <div class="d-flex justify-content-between border-bottom p-3">
        <div class="discussion-item-pic mr-2">
            <img src="@/assets/images/profile-picture-2.jpg" class="object-fit-cover rounded-circle w-100 h-100"
                alt="profile-picture">
        </div>
        <div class="w-100">
            <div class="d-flex align-items-center">
                <h4 class="m-0 mr-1">Bessie Cooper</h4>
                <span class="discussion-item-time">3h ago</span>
            </div>
            <p class="discussion-item-text">I think for our second campaign we can try to target a different audience.
                How does it sound for you?</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'discussionItem',
}
</script>

<style lang="scss">
.discussion-item {
    &-pic {
        width: 56px;
        height: 48px;
    }

    &-text {
        margin: 8px 0 !important;
        color: #6c757d;
    }

    &-time {
        color: #a2aac0;
        font-size: 1.1rem;
    }
}
</style>
