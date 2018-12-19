<template>
  <div class="mt-5">Activities</div>
</template>

<script>
export default {
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
  }
};
</script>