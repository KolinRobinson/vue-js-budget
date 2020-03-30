<template>
    <div>
        <div class="list-item" v-for="(item, prop) in list" :key="prop" v-show="filtersShow">
            <span class="budget-comment">
                <i :class="iconBudget(item.value)"></i>
                {{ item.comments }}
            </span>
            <span class="budget-value" :class="totalColor(item.value)">{{ item.value }}</span>
            <ElButton type="danger" size="mini"  @click="dialogVisible = true">Delete</ElButton>
            <el-dialog
                    title="Удаление"
                    :visible.sync="dialogVisible"
                    width="30%">
                <span>Вы уверенны?</span>
                <span slot="footer" class="dialog-footer">
                    <el-button @click="dialogVisible = false">Нет</el-button>
                    <el-button type="primary" @click="deleteItem(item.id)">Да</el-button>
                </span>
            </el-dialog>
        </div>
    </div>
</template>

<script>
	export default {
		name: "BudgetListItem",
        data() {
            return {
                dialogVisible: false
            };
        },
        props:{
            list: {
                type: Object,
                default: () => ({})
            }
        },
        methods: {
            deleteItem(id) {
                this.dialogVisible = false;
                 return this.$emit('deleteItem', id);

            },
            iconBudget(value) {
                if (value > 0){
                    return "el-icon-top";
                } else if (value < 0) {
                    return "el-icon-bottom";
                }
            },
            totalColor(value) {
                if (value > 0){
                    return "green";
                } else if (value < 0) {
                    return "red";
                }
            },
            // filtersShow(value) {
            //      // eslint-disable-next-line no-constant-condition
            //     if (value === 100){
            //         return "item.type === 'OUTCOME'";
            //     } else if (item === 'OUTCOME'){
            //         return "item.type === 'OUTCOME'";
            //     } else {
            //         return true;
            //     }
            // }
        }
	}
</script>

<style scoped>
    .list-item{
        display: flex;
        align-items: center;
        padding: 10px 15px;
    }
    .budget-value{
        font-weight: bold;
        margin-left: auto;
        margin-right: 15px;
    }

    .green{
        color: green;
    }

    .red{
        color: red;
    }
</style>