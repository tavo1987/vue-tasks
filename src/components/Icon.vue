<template>
   <span class="icon"><i :class="classCss"></i></span>
</template>

<script>
   export default {
      props: ['icon'],
      computed: {
         classCss() {
            return `fa fa-${this.icon}`;
         }
      },
   }
</script>
