<template lang="html">
    <form>
        <div class="ps-form__content">
            <h5>Log In Your Account</h5>
            <div class="form-group">
                <v-text-field
                    v-model="username"
                    class="ps-text-field"
                    :error-messages="usernameErrors"
                    @input="$v.username.$touch()"
                    placeholder="Usernamer or email"
                    height="50"
                    outlined
                />
            </div>
            <div class="form-group">
                <v-text-field
                    v-model="password"
                    type="password"
                    class="ps-text-field"
                    :error-messages="passwordErrors"
                    @input="$v.password.$touch()"
                    placeholder="Please enter password"
                    height="50"
                    outlined
                />
            </div>
            <div class="form-group">
                <v-checkbox label="Remember me" color="warning" />
            </div>
            <div class="form-group submit">
                <button
                    type="submit"
                    class="ps-btn ps-btn--fullwidth"
                    @click.prevent="handleSubmit"
                >
                    Login
                </button>
            </div>
        </div>
    </form>
</template>

<script>
import { email, required } from 'vuelidate/lib/validators';
import { validationMixin } from 'vuelidate';

export default {
    name: 'Login',
    computed: {
        usernameErrors() {
            const errors = [];
            if (!this.$v.username.$dirty) return errors;
            !this.$v.username.required && errors.push('This field is required');
            return errors;
        },
        passwordErrors() {
            const errors = [];
            if (!this.$v.password.$dirty) return errors;
            !this.$v.password.required && errors.push('This field is required');
            return errors;
        },
    },
    data() {
        return {
            username: null,
            password: null,
        };
    },
    validations: {
        username: { required },
        password: { required },
    },
    methods: {
        async handleSubmit() {
            this.$v.$touch();
            if (this.$v.$invalid) {
                return false;
            }

            const params = {
                identifier: this.username,
                password: this.password,
            };

            try {
                const response = await this.$store.dispatch('auth/login', params);
                this.$store.commit('auth/setToken', response.jwt);
                this.$store.commit('auth/updateUserId', response.user.id);
                this.$store.dispatch('auth/getProfile', response.user.id);
                this.$router.push('/');
            } catch(e){
                console.log(e);
                this.$notify({
                    group: 'addCartSuccess',
                    title: 'Failed!',
                    text: `Username or password not correct`
                });
            }
           
        },
    },
};
</script>

<style lang="scss" scoped></style>
