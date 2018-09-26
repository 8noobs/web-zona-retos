Vue.component('lista-retos', {
  props: ['fuente'],
  template: '#lista-retos-template',
});

new Vue({
  mounted() {
    this.cargarRetos();
    this.cargarGanadores();
  },

  el: "div.mainContent",
  data: {
    retos: [],
    ganadores: []
  },
  methods: {
    cargarRetos() {
      axios.get('https://api.myjson.com/bins/115h94')
        .then((respuesta) => {
          this.retos = respuesta.data.retos;
        });
    },
    cargarGanadores() {
      axios.get('https://api.myjson.com/bins/1dhga0')
        .then((respuesta) => {
          this.ganadores = respuesta.data.ganadores;
        });
    }
  },
  computed: {
    retosResueltos() {
      return this.retos.filter((reto) => reto.resuelto)
    },
    retosNoResueltos() {
      return this.retos.filter((reto) => !reto.resuelto)
    }
  }
});
