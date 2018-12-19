<template>
  <b-form
    @submit.prevent="submitActivity"
    class="mt-5"
  >
  <activity-personal-data :personal_data="activity.personal_data"></activity-personal-data>
    <b-row>
      <b-col>
        <b-btn
          type="submit"
          variant="primary"
        >Submit</b-btn>
      </b-col>
    </b-row>
  </b-form>
</template>

<script>
import ActivityPersonalData from "../components/ActivittyForm/ActivityPersonalData";
import VaidationMixin from '../mixins/validation'
export default {
  components: {
    ActivityPersonalData
  },
  mixins:[VaidationMixin],
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
  methods: {
    async submitActivity() {
      const validate = await this.$validator.validateAll();
    }
  }
};
</script>