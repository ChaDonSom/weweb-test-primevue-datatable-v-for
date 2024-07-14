<template>
  <div>
    <h1>Doesn't work</h1>
    <DTDataTable
      :value="[
        { id: 1, name: 'Bob' },
        { id: 2, name: 'Joe' },
      ]"
    >
      <DTColumn
        v-for="column in [
          { field: 'id', header: 'ID' },
          { field: 'name', header: 'Name' },
        ]"
        :field="column.field"
        :header="column.header"
        :key="column.id"
      />
    </DTDataTable>
    <h1>Does work</h1>
    <DTDataTable
      :value="[
        { id: 1, name: 'Bob' },
        { id: 2, name: 'Joe' },
      ]"
    >
      <DTColumn field="id" header="ID" />
      <DTColumn field="name" header="Name" />
    </DTDataTable>
  </div>
</template>

<script>
import Aura from "@primevue/themes/aura"
import PrimeVue from "primevue/config"
import DTDataTable from "primevue/datatable"
import DTColumn from "primevue/column"

export default {
  components: [DTDataTable, DTColumn],

  beforeCreate: function () {
    // Add Tailwind to the head
    if (!wwLib.getFrontDocument().getElementById("dt-tailwind")) {
      const script = wwLib.getFrontDocument().createElement("script")
      script.src = "https://cdn.tailwindcss.com"
      script.id = "pv-tailwind"
      wwLib.getFrontDocument().body.appendChild(script)
    }

    if (this.$.appContext.app.component("DTDataTable")) return
    this.$.appContext.app.use(PrimeVue, { theme: { preset: Aura } })
    this.$.appContext.app.component("DTDataTable", DTDataTable)
    this.$.appContext.app.component("DTColumn", DTColumn)
  },
  props: {
    content: { type: Object, required: true },
  },
}
</script>
