<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-12 col-md-4">
                <div class="my-5">
                    <Title title="Vue Cli ToDo App"></Title>
                    <!--                input section-->
                    <ListCreate @create="create"></ListCreate>
                    <!--                done section-->
                    <div class="d-flex justify-content-between">
                        <p class="mb-0 font-weight-bold">Job List{{ lists.length > 1 ? "s" : "" }}</p>
                        <p v-if="lists.length>0 && doneTotal === lists.length" class="badge badge-success badge-pill">
                            All Done <i class="fas fa-check-circle"></i>
                        </p>
                        <p v-else class="badge badge-primary badge-pill">
                            Done {{ doneTotal }}
                        </p>
                    </div>

                    <!--                list section-->
                    <ul v-if="lists.length === 0" class="list-group">
                        <li class="list-group-item text-center">There is no job 😞</li>
                    </ul>
                    <ul v-else class="list-group">
                        <List v-for="list in lists" :key="list.id" :list="list" @del="del"></List>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Title from "./components/Title";
import List from "./components/List";
import ListCreate from "./components/ListCreate";
export default {
    name: "App",
    components: {ListCreate, List, Title},
    data() {
        return {
            currentId: 0,
            newMessage: "",
            lists: [],
        }
    },
    computed: {
        doneTotal() {
            return this.lists.filter(el => el.isDone === true).length;
        }
    },
    methods: {
        create(x) {
            this.currentId++;
            this.lists.push({
                id: this.currentId,
                message: x,
                isDone: false,
            });
        },

        del(x) {
            setTimeout(() => this.lists = this.lists.filter(el => el.id !== x), 600);
        }

    }
}
</script>

<style>

.done {
    text-decoration: line-through !important;
    animation: shakeX 0.5s;
}

.created {
    animation: fadeInDown 0.5s;
}

.deleted {
    animation: zoomOut 0.5s;
}

</style>