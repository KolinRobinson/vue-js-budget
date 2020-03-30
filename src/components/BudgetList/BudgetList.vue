<template>
    <div class="budget-list-wrap">
        <ElCard :header="header">
            <template v-if="!isEmpty">
                <ElButton @click="filterType(item.type)"
                          v-for="item in buttons"
                          :key="item">
                    {{item.name}}
                </ElButton>
                <BudgetListItem  :list="$props.list" @deleteItem="deleteItem" />
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
        props: ['list'],
         data: () => ({
            a: '',
             buttons: {
                1: {
                    name: 'OUTCOME',
                    type: 'OUTCOME'
                },
                 2: {
                     name: 'INCOME',
                     type: 'INCOME'
                 },
                 3: {
                     name: 'ALL',
                     type: 'ALL'
                 }
             },
              header: 'Budget list',
              emptyTittle: 'Empty list'
         }),
         computed: {
			isEmpty() {
				return !Object.keys(this.list).length;
            }
         },
         methods: {
            deleteItem(id) {
                this.$emit('deleteItem', id);
            },
            filterType(type){
                 // eslint-disable-next-line no-unused-vars
                let a;
                return a = type;
             }
        }

	}
</script>

<style scoped>

    .budget-list-wrap{
        max-width: 500px;
        margin: auto;
    }




</style>