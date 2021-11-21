<template>
    <li :class="['list-group-item d-flex justify-content-between align-items-center created', {deleted: isDelete}]">
        <input v-if="isEdit===true" type="text" v-model="list.message"
               class="form-control form-control-lg mr-2" @keyup.enter="isEdit=false">
        <div v-else class="custom-control custom-checkbox">
            <input type="checkbox" v-model="list.isDone" class="custom-control-input"
                   :id="'customCheck'+list.id">
            <label :for="'customCheck'+list.id"
                   :class="['custom-control-label', {'done': list.isDone}]">{{ list.message }}</label>
        </div>
        <div class="">
            <i class="fas fa-edit text-warning mr-2" @click="isEdit = true"></i>
            <i class="fas fa-trash-alt text-danger" @click="[isDelete=true, del(list.id)]"></i>
        </div>
    </li>
</template>

<script>
export default {
    name: "List",
    props: {
        list: {
            type: Object,
            required: true,
        }
    },
    data() {
        return {
            isEdit: false,
            isDelete: false,
        }
    },
    methods: {
        del(x) {
            this.$emit("del", x);
        },

    },
}
</script>

<style scoped>

</style>