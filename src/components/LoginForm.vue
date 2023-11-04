<template>
    <div class="row">
        <Form
        @submit="login"
        :validation-schema="contactFormSchema"
        >
            <div class="form-group">
                <label for="usn">Username: </label>
                <Field
                    name="usn"
                    type="text"
                    class="form-control"
                    v-model="local.usn"
                />
                <ErrorMessage name="usn" class="error-feedback" />
            </div>

            <div class="form-group">
                <label for="pass">Password: </label>
                <Field
                    name="pass"
                    type="password"
                    class="form-control"
                    v-model="local.pass"
                />
                <ErrorMessage name="pass" class="error-feedback" />
            </div>

            <div class="form-group">
                <button class="btn btn-primary">Lưu</button>
            </div>
        </Form>
    </div>
</template>

<script>
    import * as yup from "yup";
    import { Form, Field, ErrorMessage } from "vee-validate";
    export default {
        components: {
            Form,
            Field,
            ErrorMessage,
        },
        emits:['submit:login'],
        props: {
            login: { type: Object, required: true }
        },
        data() {
            const loginFormSchema = yup.object().shape({
                usn: yup
                    .string()
                    .required("username phải có giá trị.")
                    .min(2, "username phải ít nhất 2 ký tự.")
                    .max(50, "username có nhiều nhất 50 ký tự."),
                pass: yup
                    .string()
                    .required("passwd phải có giá trị.")
                    .min(2, "passwd phải ít nhất 2 ký tự.")
                    .max(50, "passwd có nhiều nhất 50 ký tự."),
            });
            return{
                local: this.login,
                loginFormSchema,
            }
        },
        methods: {
            login() {
                this.$emit("submit:login", this.local);
            },
        }
    }
</script>