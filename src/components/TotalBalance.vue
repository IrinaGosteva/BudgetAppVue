<template>
  <div class="total-value"  :class="textColor"  @change="onChange($event)" > Balance: {{ total }}
  </div>
</template>

<script>
export default {
  name: 'TotalBalance',
  props: {
    total: {
      type: Number,
      default: 0
    }
  },

  data: () => ({ 
   }),

  methods: {
  },

  computed: {
    textColor: function() {
      if (this.total > 0 && this.total!=0) {
        return 'green-text';
      } if (this.total==0) {
          return 'black-text';
        } else {
          return 'red-text'; 
      }     
    },  
  },
}
</script>

<style scoped>
.total-value {
  font-style: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}

.red-text {
  color: red;
}
.green-text {
  color: green;
}
</style>