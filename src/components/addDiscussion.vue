<template>
    <div class="d-flex justify-content-between align-items-center border-bottom bg-light-silver p-3">
        <div>
            <div class="add-discussion-pic mr-2">
                <img src="@/assets/images/profile-picture-1.jpg" class="object-fit-cover rounded-circle w-100 h-100"
                    alt="profile-picture">
            </div>
        </div>
        <input class="form-control" type="text" placeholder="start a discussion">
    </div>
</template>

<script>
export default {
    name: 'addDiscussion',
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
