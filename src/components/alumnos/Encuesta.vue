<template>
    <div>
        <a class="btn btn-sm btn-outline-dark" role="button" href="#" @click.prevent="volver">Volver</a>
      <hr>
        <!--<div class="container">-->
          <component :is="current" :idEncuesta="id" :encuesta="encuesta" @volver="volver"></component>
        <!--</div>-->
    </div>
</template>
<script>
/* eslint-disable indent */
import api from '../../api'
import votacion from '../encuestas/votacionCriterios'
import priorizacion from '../encuestas/priorizacion'
import habilitada from '../encuestas/habilitada'
import cerrada from '../encuestas/cerrada'
    export default {
      props: [
        'id'
      ],
      components: {
        votacion,
        priorizacion,
        habilitada,
        cerrada
      },
      data () {
        return {
          encuesta: null,
          nombre: null,
          curso: null,
          materia: null,
          creador: null,
          etapa: null,
          creacion: null,
          finEtapa: null,
          cantMaxCriterios: null,
          cantMaxVotosPorPersona: null,
          codigo: null,
          current: null
        }
      },
      mounted () {
        this.cargarEncuesta()
      },
      methods: {
        cargarEncuesta () {
          api.getEncuestaFull(this.id)
            .then(r => {
              this.encuesta = r
              this.nombre = r.nombre
              this.curso = r.curso
              this.materia = r.materia
              this.creador = r.creador
              this.etapa = r.etapaActual
              this.creacion = r.fechaCreacion
              this.finEtapa = r.fechaFinEtapaActual
              this.cantMaxCriterios = r.cantMaxCriterios
              this.cantMaxVotosPorPersona = r.cantMaxVotosPorPersona
              this.codigo = r.codigo === null ? 'No generado' : r.codigo
              switch (this.etapa) {
                case 'Votacion Criterios':
                  this.current = 'votacion'
                      break
                case 'Priorizacion':
                  this.current = 'priorizacion'
                      break
                case 'Habilitada':
                  this.current = 'habilitada'
                      break
                case 'Cerrada':
                  this.current = 'cerrada'
                      break
              }
            })
        },
        volver () {
          this.$parent.encuesta = null
        }
      }
    }
</script>
