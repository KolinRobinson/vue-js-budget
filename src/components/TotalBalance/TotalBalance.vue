<template>
    <div class="total-value" :class="totalColor">
        Балланс: {{ total }}
    </div>
</template>

<script>
	export default {
		name: "TotalBalance",
         props: {
			total: {
                type: Number,
                 default: 0
            }
         },
         computed:{
              // eslint-disable-next-line vue/return-in-computed-property
			totalColor() {
				if (this.total > 0){
                    return "green";
                } else if (this.total < 0) {
                    return "red";
                }
            }
         }
	}
</script>

<style scoped>
    .total-value{
        font-size: 32px;
        text-transform: uppercase;
        padding: 15px;
        text-align: center;
    }

    .green{
        color: green;
    }

    .red{
        color: red;
    }
</style>