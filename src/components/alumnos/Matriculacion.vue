<template>
    <div class="row">
      <div class="col"></div>
      <div class="col-6">
      <form @submit.prevent="matricularse">
        <div class="form-group">
          <label for="codigoEncuesta">Ingrese el código de la encuesta:</label>
          <input type="text" class="form-control" id="codigoEncuesta" placeholder="Código alfanumérico" v-model="codigo" required>
          <small class="form-text text-muted">Ingresar aquí el código de identificación de la encuesta provisto por el profesor.</small>
        </div>
        <button type="submit" class="btn btn-primary">Matricularse a encuesta</button>
      </form>
      </div>
      <div class="col"></div>
    </div>
</template>

<script>
import api from '../../api'

export default {
  name: 'matriculacion',
  data () {
    return {
      codigo: null
    }
  },
  methods: {
    matricularse () {
      api.matricularse(this.codigo)
        .then(r => {
          if (r) {
            alert('Matriculado correctamente')
            this.$parent.current = 'listaEncuestas'
          } else {
            alert('Error al matricularse. Verifique que el código sea correcto')
          }
        })
    }
  }
}
</script>
