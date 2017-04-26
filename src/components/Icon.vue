<template>
   <span class="icon"><i :class="cssClass"></i></span>
</template>

<script>
   export default {
      props: ['icon'],
      computed: {
         cssClass() {
            return `fa fa-${this.icon}`;
         },
      },
   }
</script>
