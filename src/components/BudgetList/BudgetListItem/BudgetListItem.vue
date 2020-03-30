<template>
    <div>
        <div class="list-item"
             v-for="(item, prop) in list"
             :key="prop"
             v-show="item.type === budgetFiltersShow(budgetFiltersKey, item.type)">
            <span class="budget-comment">
                <i :class="iconBudget(item.value)"></i>
                {{ item.comments }}
            </span>
            <span class="budget-value"
                  :class="totalColor(item.value)">
                {{ item.value }}
            </span>
            <ElButton type="danger"
                      size="mini"
                      @click="dialogVisible = true">
                Удалить
            </ElButton>
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
            },
            budgetFiltersKey: {
                type: String
            }
        },
         computed: {

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
            budgetFiltersShow(budgetFiltersKey, key){
                if (budgetFiltersKey === 'income'){
                    return  'INCOME';
                } else if (budgetFiltersKey === 'outcome'){
                    return 'OUTCOME';
                } else if (budgetFiltersKey === 'all'){
                    return key;
                } else {
                    return key;
                }
            }
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