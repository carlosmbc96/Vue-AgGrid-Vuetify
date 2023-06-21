<script setup>
import { ref } from 'vue';

const props = defineProps({
  params: {
    type: Object
  }
})
const show_modal = ref(false)
let { rowId, name, age, country, email } = props.params.data

const onCancel = () => {
  show_modal.value = false
  name = props.params.data.name
  age = props.params.data.age
  country = props.params.data.country
  email = props.params.data.email
}

const onSave = () => {
  show_modal.value = false
  props.params.data.name = name
  props.params.data.age = age
  props.params.data.country = country
  props.params.data.email = email
  props.params.context.componentParent.updateRows({ rowId, name, age, country, email })
}

</script>

<template>
  <div class="row-expanded">
    <v-btn color="light-blue" @click="show_modal = true">
      Editar valores de fila
    </v-btn>

    <v-dialog width="500px" persistent v-model="show_modal">
      <v-card>
        <v-form>
          <v-container>
            <v-col>
              <v-col cols="12">
                <v-text-field v-model="name" label="Nombre"></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-text-field v-model="age" label="Edad"></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-text-field v-model="country" label="País"></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-text-field v-model="email" label="Correo"></v-text-field>
              </v-col>

              <v-col class="footer-btns" cols="12">
                <v-btn color="light-blue" @click="onCancel">
                  Cancelar
                </v-btn>
                <v-btn color="green" @click="onSave">
                  Guardar
                </v-btn>
              </v-col>
            </v-col>
          </v-container>
        </v-form>
      </v-card>
    </v-dialog>
  </div>
</template>

<style>
.row-expanded {
  display: flex;
  justify-content: center;
  align-items: center;
  height: inherit;
}

.footer-btns {
  gap: 10px;
  display: flex;
  flex-wrap: wrap;
}
</style>
