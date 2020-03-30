<template>
    <div class="budget-list-wrap">
        <ElCard :header="header">
            <template v-if="!isEmpty">
                <ElButton v-on:click="budgetFiltersKey = 'income'">
                    Доходы
                </ElButton>
                <ElButton v-on:click="budgetFiltersKey = 'outcome'">
                    Траты
                </ElButton>
                <ElButton v-on:click="budgetFiltersKey = 'all'">
                    Все
                </ElButton>
                <BudgetListItem  :list="list"
                                 @deleteItem="deleteItem"
                                 :budgetFiltersKey="budgetFiltersKey"
                                 />
            </template>
            <ElAlert v-else type="info" :title="emptyTittle" :closable="false"/>
        </ElCard>
    </div>
</template>

<script>
import BudgetListItem from "./BudgetListItem/BudgetListItem";
	export default {
		name: "BudgetList",
        components: {BudgetListItem},
        props:{
            list: {
                type: Object,
                default: () => ({})
                }
            },
         data: () => ({
            budgetFiltersKey: 'all',
              header: 'Budget list',
              emptyTittle: 'Empty list'
         }),
         computed: {
			isEmpty() {
				return !Object.keys(this.list).length;
            },
            budgetFilters(){
                return this.budgetFiltersKey;
            }
         },
         methods: {
            deleteItem(id) {
                this.$emit('deleteItem', id);
            },
        }

	}
</script>

<style scoped>

    .budget-list-wrap{
        max-width: 500px;
        margin: auto;
    }




</style>