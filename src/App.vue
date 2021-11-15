<template>
    <div id="app">
        <h2>Обратная связь</h2>

        <el-form :model="form" status-icon :rules="rules" ref="form">
            <div class="wrapper">
                <el-form-item class="input-name" prop="name">
                    <el-input maxlength="30" placeholder="Имя" v-model="form.name"></el-input>
                </el-form-item>

                <el-form-item class="input-email" prop="email">
                    <el-input maxlength="30" placeholder="Email" v-model="form.email"></el-input>
                </el-form-item>

                <el-form-item class="input-text-area" prop="desc">
                    <el-input
                        type="textarea"
                        maxlength="250"
                        :cols="50"
                        :rows="5"
                        resize="none"
                        placeholder="Сообщение"
                        v-model="form.desc"
                    ></el-input>
                </el-form-item>
            </div>

            <div class="button-items">
                <el-form-item>
                    <el-button type="primary" :style="{ marginRight: '10px' }" @click="resetForm('form')">
                        Сбросить
                    </el-button>
                </el-form-item>

                <el-form-item>
                    <el-button type="success" @click="submitForm('form')"> Отправить </el-button>
                </el-form-item>
            </div>
        </el-form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            form: {
                name: '',
                email: '',
                desc: '',
            },

            rules: {
                name: [{ required: true, validator: this.validateName, trigger: 'blur' }],
                email: [
                    { required: true, validator: this.validateEmail, trigger: 'blur' },
                    { type: 'email', message: 'Введите корректный свой E-mail!', trigger: ['blur', 'change'] },
                ],
                desc: [{ validator: this.validateTextArea, trigger: 'blur' }],
            },
        };
    },

    methods: {
        validateName(rule, value, callback) {
            value === '' ? callback(new Error('Пожалуйста, введите своё имя!')) : callback();
        },

        validateEmail(rule, value, callback) {
            value === '' ? callback(new Error('Пожалуйста, введите свой E-mail!')) : callback();
        },

        validateTextArea(rule, value, callback) {
            value === '' ? callback(new Error('Пожалуйста, введите своё сообщение!')) : callback();
        },

        submitForm(formName) {
            this.$refs[formName].validate((valid) => (valid ? alert('Сообщение доставлено!') : ''));
            this.resetForm(formName);
        },

        resetForm(formName) {
            this.$refs[formName].resetFields();
        },
    },
};
</script>

<style>
@import url('//unpkg.com/element-ui@2.15.6/lib/theme-chalk/index.css');

#app {
    width: 700px;
    margin: 0 auto;
}

.wrapper {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
    margin-bottom: 20px;
}

.input-name {
    grid-row: 1/2;
}

.input-email {
    grid-row: 2/3;
}

.input-text-area {
    grid-column: 2/3;
    grid-row: 1/3;
}

.button-items {
    display: flex;
    justify-content: end;
}
</style>
