<template>
    <ElCard class="form-card">
        <ElForm :model="formData" ref="addItemForm" :rules="rules" label-position="top">
            <ElFormItem label="Type:" prop="type">
                <ElSelect class="type-select" v-model="formData.type" placeholder="Choose Type...">
                    <ElOption label="Income" value="INCOME" />
                    <ElOption label="Outcome" value="OUTCOME" />
                </ElSelect>
            </ElFormItem>
            <ElFormItem label="Comment:" prop="comments">
                <ElInput v-model="formData.comments"/>
            </ElFormItem>
            <ElFormItem label="Value:" prop="value">
                <ElInput v-model.number="formData.value" :onchange="outcomeAddMinus"/>
            </ElFormItem>
            <ElButton @click="onSubmit" type="primary">Submit</ElButton>
        </ElForm>
    </ElCard>

</template>

<script>


	let checkNumber = (rule, value, callback) => {
        if (!value) {
            return callback(new Error('Пожалуйста, укажите данные по бюджету!'));
        }
        setTimeout(() => {
            if (!Number.isInteger(value)) {
                callback(new Error('Пожалуйста, введите число!'));
            } else {
                    callback();
                }
        }, 1000);
	};

    export default {
		name: "Form",
         data: () => ({
             formData: {
                 type: 'INCOME',
                 comments: '',
                 value: 0
            },
            rules:{
                type: [
                     {required: true, message: 'Please select type', trigger: 'blur'}
                ],
                comments: [
                     {required: true, message: 'Please input comment', trigger: 'blur'}
                ],
                 value:  [
                    { validator: checkNumber, trigger: 'blur' },
                 ]
            }
         }),
         computed:{
              // eslint-disable-next-line vue/return-in-computed-property
             outcomeAddMinus(){
                  // eslint-disable-next-line no-constant-condition
                if (this.formData.type === "OUTCOME" && this.formData.value > 0){
                     // eslint-disable-next-line vue/no-side-effects-in-computed-properties
                    this.formData.value = -(this.formData.value);
                }
             }
         },
         methods: {
             onSubmit() {
                this.$refs.addItemForm.validate((valid) => {
                    if(valid){
                        this.$emit('submitForm', {...this.formData});
                        this.$refs.addItemForm.resetFields();
                    }
                })
             }
         }
	};
</script>

<style scoped>
    .form-card{
        max-width: 500px;
        margin: auto;
    }

    .type-select{
        width: 100%;
    }
</style>