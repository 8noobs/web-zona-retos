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
      this.$http.jsonp('https://json2jsonp.com/?callback=jsonZonaRetos&url=https://vpn412475359.softether.net/index.php/s/iiqcyQBoG4qtnaH/download',
      {jsonpCallback: 'jsonZonaRetos'})
        .then(respuesta => {
          this.retos = respuesta.body.retos;
        });
    },
    cargarGanadores() {
      this.$http.get('https://api.myjson.com/bins/1dhga0')
        .then(respuesta => {
          this.ganadores = respuesta.body.ganadores;
        });
    }
  },
  computed: {
    retosResueltos() {
      return this.retos.filter((reto) => reto.resuelto == "si");
    },
    retosNoResueltos() {
      return this.retos.filter((reto) => reto.resuelto == "no");
    }
  }
});