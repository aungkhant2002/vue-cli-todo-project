<template>
    <div class="form-row mb-3">
        <div class="col-10">
            <input type="text" v-model="newMessage" class="form-control form-control-lg"
                   placeholder="Say Something" @keyup.enter="create()" @keyup="showError=false">
        </div>
        <div class="col-2">
            <button class="btn btn-primary btn-lg w-100" @click="create()">
                <i class="fas fa-plus-circle"></i>
            </button>
        </div>
        <div class="col-12">
            <small v-if="showError" class="text-danger font-weight-bolder">{{ errorMessage }}</small>
        </div>
    </div>
</template>

<script>
export default {
    name: "ListCreate",
    data() {
        return {
            newMessage: "",
            showError: false,
            errorMessage: "",
        }
    },
    methods: {
        create() {
            if (this.newMessage.length) {
                this.showError = false;
                this.$emit("create", this.newMessage);
                this.newMessage = "";
            } else {
                this.showError = true;
                this.errorMessage = "Say Something";
            }
        }
    },
}
</script>

<style scoped>

</style>