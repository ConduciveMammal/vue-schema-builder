Vue.component('Button', {
  props: ['text'],
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})

<script>
export default {
  name: 'Polaris',
  props: {
    text: String
  }
}
</script>