<template>
  <b-form
    @submit.prevent="submitActivity"
    class="mt-5"
  >
    <activity-personal-data :personal_data="activity.personal_data"></activity-personal-data>
    <activity-type-selection :activity_type_selection="activity.activity_type_selection"></activity-type-selection>
    <component
      :activity_selected_data="activity.activity_selected_data"
      :is="activityComponent"
    ></component>
    <b-row class="mt-3">
      <b-col>
        <b-form-checkbox
          :state="activity.terms ? 'valid' : (reset ? null : 'invalid')"
          :unchecked-value="false"
          name="terms"
          v-model="activity.terms"
          v-validate="'required'"
        >Acepto los términos de uso</b-form-checkbox>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <b-button
          block
          class="mt-3"
          type="submit"
          variant="primary"
        >Enviar</b-button>
      </b-col>
      <b-col>
        <b-button
          @click="clearErrors"
          block
          class="mt-3 text-white"
          variant="warning"
        >Limpiar errores</b-button>
      </b-col>
      <b-col>
        <b-button
          @click="clearForm"
          block
          class="mt-3 text-white"
          variant="info"
        >Limpiar formulario</b-button>
      </b-col>
      <b-col>
        <b-button
          @click="clearFormAndErrors"
          block
          class="mt-3 text-white"
        >Limpiar formulario y errores</b-button>
      </b-col>
    </b-row>
  </b-form>
</template>

<script>
import ActivityPersonalData from "../components/ActivityForm/ActivityPersonalData";
import ActivityTypeSelection from "../components/ActivityForm/ActivityTypeSelection";
import Basket from "../components/ActivityForm/Types/Basket";
import Football from "../components/ActivityForm/Types/Football";
import Tennis from "../components/ActivityForm/Types/Tennis";
import VaidationMixin from "../mixins/validation";
export default {
  components: {
    ActivityPersonalData,
    ActivityTypeSelection,
    Basket,
    Football,
    Tennis
  },
  mixins: [VaidationMixin],
  data() {
    return {
      reset: true,
      activity_types_component: ["basket", "football", "tennis"],
      activity: {
        terms: false,
        personal_data: {
          name: "",
          surname: ""
        },

        activity_type_selection: {
          type: 1,
          date: ""
        },
        activity_selected_data: {
          team: "",
          information: ""
        }
      }
    };
  },
  computed: {
    activityComponent() {
      switch (this.activity.activity_type_selection.type) {
        case 1:
          return "football";

        case 2:
          return "basket";

        case 3:
          return "tennis";

        default:
          return "football";
      }
    }
  },
  methods: {
    async submitActivity() {
      this.reset = false;
      if (!this.activity.terms) {
        return false;
      }
      const validate = await this.$validator.validateAll();
      if (!validate) {
        return false;
      }
      alert("formulario ok");
    },
    clearForm() {
      Object.assign(this.$data, this.$options.data.apply(this));
    },
    clearErrors() {
      this.reset = true;
      this.$validator.reset();
    },
    clearFormAndErrors() {
      this.clearForm();
      this.clearErrors();
    }
  }
};
</script>