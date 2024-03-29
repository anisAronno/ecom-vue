<template>
  <div class="auth-wrapper auth-v2">
    <b-row class="auth-inner m-0">
      <!-- Brand logo-->
      <b-link class="brand-logo">
        <vuexy-logo />
        <h2 class="brand-text text-primary ml-1">Vuexy</h2>
      </b-link>
      <!-- /Brand logo-->

      <!-- Left Text-->
      <b-col lg="8" class="d-none d-lg-flex align-items-center p-5">
        <div
          class="w-100 d-lg-flex align-items-center justify-content-center px-5"
        >
          <b-img fluid :src="imgUrl" alt="Login V2" />
        </div>
      </b-col>
      <!-- /Left Text-->

      <!-- Login-->
      <b-col lg="4" class="d-flex align-items-center auth-bg px-2 p-lg-5">
        <b-col sm="8" md="6" lg="12" class="px-xl-2 mx-auto">
          <b-card-title title-tag="h2" class="font-weight-bold mb-1">
            Welcome to E Commerce! 👋
          </b-card-title>
          <b-card-text class="mb-2">
            Please sign-up to your account and start the adventure
          </b-card-text>

          <!-- form -->
          <validation-observer ref="loginValidation">
            <b-form class="auth-login-form mt-2" @submit.prevent="userRegister">
              <!-- name -->
              <b-form-group label="name" label-for="name">
                <validation-provider
                  #default="{ errors }"
                  name="name"
                  rules="required"
                >
                  <b-form-input
                    id="name"
                    v-model="name"
                    :state="errors.length > 0 ? false : null"
                    name="name"
                    placeholder="Your Name"
                  />
                  <small class="text-danger">{{ errors[0] }}</small>
                </validation-provider>
              </b-form-group>

              <!-- email -->
              <b-form-group label="Email" label-for="login-email">
                <validation-provider
                  #default="{ errors }"
                  name="Email"
                  rules="required|email"
                >
                  <b-form-input
                    id="login-email"
                    v-model="userEmail"
                    :state="errors.length > 0 ? false : null"
                    name="login-email"
                    placeholder="john@example.com"
                  />
                  <small class="text-danger">{{ errors[0] }}</small>
                </validation-provider>
              </b-form-group>

              <!-- password -->
              <b-form-group>
                <validation-provider
                  #default="{ errors }"
                  name="Password"
                   vid="Password"
                     rules="required|min:6"
                >
                  <b-input-group
                    class="input-group-merge"
                    :class="errors.length > 0 ? 'is-invalid' : null"
                  >
                    <b-form-input
                      id="login-password"
                      v-model="password"
                      :state="errors.length > 0 ? false : null"
                      class="form-control-merge"
                      :type="passwordFieldType"
                      name="login-password"
                      placeholder="Password"
                    />
                    <b-input-group-append is-text>
                      <feather-icon
                        class="cursor-pointer"
                        :icon="passwordToggleIcon"
                        @click="togglePasswordVisibility"
                      />
                    </b-input-group-append>
                  </b-input-group>
                  <small class="text-danger">{{ errors[0] }}</small>
                </validation-provider>
              </b-form-group>

              <!-- Confirmed password -->
              <b-form-group>
                <validation-provider
                  #default="{ errors }"
                  name="Password Confirmation"
                 rules="required|confirmed:Password"
                >
                  <b-input-group
                    class="input-group-merge"
                    :class="errors.length > 0 ? 'is-invalid' : null"
                  >
                    <b-form-input
                      id="password_confirmation"
                      v-model="password_confirmation"
                      :state="errors.length > 0 ? false : null"
                      class="form-control-merge"
                      :type="passwordFieldType"
                      name="password_confirmation"
                      placeholder="Confirmed Password"
                    />
                    <b-input-group-append is-text>
                      <feather-icon
                        class="cursor-pointer"
                        :icon="passwordToggleIcon"
                        @click="togglePasswordVisibility"
                      />
                    </b-input-group-append>
                  </b-input-group>
                  <small class="text-danger">{{ errors[0] }}</small>
                </validation-provider>
              </b-form-group>

              <!-- submit buttons -->
              <b-button
                type="submit"
                variant="primary"
                block
                @click="validationForm"
              >
                Sign up
              </b-button>
            </b-form>
          </validation-observer>

          <b-card-text class="text-center mt-2">
            <span>have Account? </span>
            <b-link :to="{ name: 'login' }">
              <span>&nbsp;Login Now</span>
            </b-link>
          </b-card-text>

          <!-- divider -->
          <div class="divider my-2">
            <div class="divider-text">or</div>
          </div>

          <!-- social buttons -->
          <div class="auth-footer-btn d-flex justify-content-center">
            <b-button variant="facebook" href="javascript:void(0)">
              <feather-icon icon="FacebookIcon" />
            </b-button>
            <b-button variant="twitter" href="javascript:void(0)">
              <feather-icon icon="TwitterIcon" />
            </b-button>
            <b-button variant="google" href="javascript:void(0)">
              <feather-icon icon="MailIcon" />
            </b-button>
            <b-button variant="github" href="javascript:void(0)">
              <feather-icon icon="GithubIcon" />
            </b-button>
          </div>
        </b-col>
      </b-col>
      <!-- /Login-->
    </b-row>
  </div>
</template>

<script>
/* eslint-disable global-require */
import { ValidationProvider, ValidationObserver } from "vee-validate";
import VuexyLogo from "@core/layouts/components/Logo.vue";
import {
  BRow,
  BCol,
  BLink,
  BFormGroup,
  BFormInput,
  BInputGroupAppend,
  BInputGroup,
  BFormCheckbox,
  BCardText,
  BCardTitle,
  BImg,
  BForm,
  BButton,
} from "bootstrap-vue";
import { required, email } from "@validations";
import { togglePasswordVisibility } from "@core/mixins/ui/forms";
import store from "@/store/index";
import ToastificationContent from "@core/components/toastification/ToastificationContent.vue";
import axios from "axios";
export default {
  components: {
    BRow,
    BCol,
    BLink,
    BFormGroup,
    BFormInput,
    BInputGroupAppend,
    BInputGroup,
    BFormCheckbox,
    BCardText,
    BCardTitle,
    BImg,
    BForm,
    BButton,
    VuexyLogo,
    ValidationProvider,
    ValidationObserver,
  },
  mixins: [togglePasswordVisibility],
  data() {
    return {
      name: "",
      userEmail: "",
      password: "",
      password_confirmation: "",

      sideImg: require("@/assets/images/pages/login-v2.svg"),
      // validation rulesimport store from '@/store/index'
      required,
      email,
    };
  },
  computed: {
    passwordToggleIcon() {
      return this.passwordFieldType === "password" ? "EyeIcon" : "EyeOffIcon";
    },
    imgUrl() {
      if (store.state.appConfig.layout.skin === "dark") {
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        this.sideImg = require("@/assets/images/pages/login-v2-dark.svg");
        return this.sideImg;
      }
      return this.sideImg;
    },
  },
  methods: {
    validationForm() {
      this.$refs.loginValidation.validate().then((success) => {
        if (success) {
          userLogin();
        }
      });
    },
    userRegister() {

      axios
        .post("api/admin/register", {
          name: this.name,
          email: this.userEmail,
          password: this.password,
          password_confirmation: this.password_confirmation,
        })
        .then((response) => {

          console.log(response.data);

          this.$toast({
            component: ToastificationContent,
            props: {
              title: "Registration Successfull",
              icon: "EditIcon",
              variant: "success",
            },
          });
          this.$router.push("/login");
        })
        .catch((error) => {
            console.log(error);
          this.$toast({
            component: ToastificationContent,
            props: {
              title: "Registration Failed",
              icon: "EditIcon",
              variant: "warning",
            },
          });
        });
    },
  },
};
</script>

<style lang="scss">
@import "@core/scss/vue/pages/page-auth.scss";
</style>
