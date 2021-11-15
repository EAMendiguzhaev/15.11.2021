<template>
    <div id="app">
        <ValidationObserver v-slot="{ invalid }">
            <el-form :model="form" @submit.prevent="onSubmit">
                <ValidationProvider
                    name="Имя"
                    rules="required|alpha"
                    v-slot="{ errors }"
                >
                    <el-form-item>
                        <el-input
                            v-model="form.name"
                            placeholder="Имя"
                        ></el-input>
                    </el-form-item>

                    <span>{{ errors[0] }}</span>
                </ValidationProvider>

                <ValidationProvider
                    name="E-mail"
                    rules="required|email"
                    v-slot="{ errors }"
                >
                    <el-form-item>
                        <el-input
                            v-model="form.email"
                            placeholder="Email"
                        ></el-input>
                    </el-form-item>

                    <span>{{ errors[0] }}</span>
                </ValidationProvider>

                <el-form-item>
                    <el-input
                        type="textarea"
                        v-model="form.desc"
                        placeholder="Сообщение"
                    ></el-input>
                </el-form-item>

                <el-form-item>
                    <el-button @click="clearInput"> Сбросить </el-button>

                    <el-button
                        type="submit"
                        :disabled="invalid"
                        @click="onSubmit"
                    >
                        Отправить
                    </el-button>
                </el-form-item>
            </el-form>
        </ValidationObserver>
    </div>
</template>

<script>
export default {
    data() {
        return {
            value: "",
            form: {
                name: "",
                email: "",
                desc: "",
            },
        };
    },
    methods: {
        onSubmit() {
            alert("Сообщение отправлено");
        },

        clearInput() {
            for (let key in this.form) {
                this.form[key] = "";
            }
        },
    },
};
</script>

<style></style>
