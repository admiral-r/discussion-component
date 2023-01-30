<template>
    <div class="d-flex justify-content-between align-items-center mt-2">
        <div>
            <div class="add-reply-pic mr-2">
                <img src="@/assets/images/profile-picture-3.jpg" class="object-fit-cover rounded-circle w-100 h-100"
                    alt="profile-picture">
            </div>
        </div>
        <input @keyup.enter="addReply" v-model="reply[parentItemId]" class="form-control" type="text"
            placeholder="Reply">
    </div>
</template>

<script>
export default {
    name: 'addReply',
    props: {
        parentItemId: {
            type: Number,
        },
        replyShow: {
            type: String,
        },
    },
    data() {
        return {
            reply: []
        }
    },
    methods: {
        addReply() {
            this.$emit("addReply", this.reply[this.parentItemId] , this.parentItemId , this.replyShow)
            this.reply[this.parentItemId] = null
        }
    },
}
</script>

<style lang="scss">
.add-reply {
    &-pic {
        width: 55px;
        height: 55px;
    }
}
</style>
