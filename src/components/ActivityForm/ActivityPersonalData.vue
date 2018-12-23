<template>
  <b-card
    class="mt-3"
    title="Datos personales"
  >
    <b-row>
      <b-col>
        <b-form-group label="Nombre">
          <b-form-input
            :state="$parent.validateState('name')"
            autocomplete="off"
            data-vv-as="nombre"
            name="name"
            placeholder="Introduce tu nombre"
            v-model="personal_data.name"
            v-validate="'required|min:2'"
          ></b-form-input>
          <b-form-invalid-feedback>{{ errors.first('name') }}</b-form-invalid-feedback>
        </b-form-group>
      </b-col>
      <b-col>
        <b-form-group label="Apellidos">
          <b-form-input
            :state="$parent.validateState('surname')"
            autocomplete="off"
            data-vv-as="apellidos"
            name="surname"
            placeholder="Introduce tus apellidos"
            v-model="personal_data.surname"
            v-validate="'required|min:4'"
          ></b-form-input>
          <b-form-invalid-feedback>{{ errors.first('surname') }}</b-form-invalid-feedback>
        </b-form-group>
      </b-col>
    </b-row>
  </b-card>
</template>

<script>
export default {
 inject: ['$validator'],
  props: {
    personal_data: {
      type: Object,
      required: true
    }
  }
};
</script>