<template>
  <ParentLayout>
    <template #page-top>
      <Breadcrumbs />
    </template>
  </ParentLayout>
</template>

<script>
import ParentLayout from '@parent-theme/layouts/Layout.vue'
import Breadcrumbs from '@theme/components/Breadcrumbs.vue'
export default {
  name: 'Layout',
  components: {
    ParentLayout,
    Breadcrumbs,
  }
}
</script>