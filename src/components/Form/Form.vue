<template>
    <ElCard class="form-card">
        <ElForm :model="formData"
                ref="addItemForm"
                :rules="rules"
                abel-position="top">
            <ElFormItem label="Тип:" prop="type">
                <ElSelect class="type-select"
                          v-model="formData.type"
                          placeholder="Choose Type...">
                    <ElOption label="Доход" value="INCOME" />
                    <ElOption label="Трата" value="OUTCOME" />
                </ElSelect>
            </ElFormItem>
            <ElFormItem label="Комментарий:" prop="comments">
                <ElInput v-model="formData.comments"/>
            </ElFormItem>
            <ElFormItem label="Количество:" prop="value">
                <ElInput v-model.number="formData.value" :onchange="outcomeAddMinus"/>
            </ElFormItem>
            <ElButton @click="onSubmit" type="primary">Отправить</ElButton>
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
                     {required: true, message: 'Пожалуйста, выберите тип поступления!', trigger: 'blur'}
                ],
                comments: [
                     {required: true, message: 'Пожалуйста, укажите данные по бюджету!', trigger: 'blur'}
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