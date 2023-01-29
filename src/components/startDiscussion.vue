<template>
    <div class="d-flex justify-content-between align-items-center border-bottom bg-light-silver p-3">
        <div class="start-discussion-pic mr-2">
            <img src="@/assets/images/profile-picture-1.jpg" class="object-fit-cover rounded-circle w-100 h-100"
                alt="profile-picture">
        </div>
        <input class="form-control" type="text" placeholder="start a discussion">
    </div>
</template>

<script>
export default {
    name: 'startDiscussion',
}
</script>

<style lang="scss">
.start-discussion {
    &-pic {
        width: 56px;
        height: 48px;
    }
}
</style>
