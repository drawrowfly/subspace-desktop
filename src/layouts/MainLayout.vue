<template lang="pug">
q-layout(view="hHh lpr fFf")
  q-header.bg-white.text-black(bordered)
    q-toolbar
      q-img(no-spinner src="subspacelogo.png" width="150px")
      q-toolbar-title
        .row
          .col-auto.q-mr-md.relative-position
            q-badge(color="grey" text-color="white")
              .q-pa-xs(style="font-size: 14px") {{ lang.nonIncentivizedLabel }}
            q-tooltip
              .col
                p.no-margin(style="font-size: 12px") {{ lang.nonIncentivizedTooltip }}
          // Show the dashboard status indicator when on the dashboard page. 
          .col-auto.q-mr-md.relative-position(
            v-if="$route.name == 'dashboard'"
          )
            q-icon(
              color="green-5"
              name="trip_origin"
              size="28px"
              style="bottom: 0px; right: 5px"
              v-if="global.status.state == 'live'"
            )
            q-icon(
              color="yellow-8"
              name="trip_origin"
              size="28px"
              style="bottom: 0px; right: 5px"
              v-if="global.status.state == 'loading'"
            )
            q-tooltip
              .col
                p Farmer Status:
                p <b>{{ global.status.message }}</b>
      div
        q-btn(flat icon="settings" round)
          MainMenu

  q-page-container
    router-view
</template>

<script lang="ts">
import { defineComponent } from "vue"
import { globalState as global } from "src/lib/global"
import * as util from "src/lib/util"
import MainMenu from "components/mainMenu.vue"
const lang = global.data.loc.text.mainMenu

export default defineComponent({
  name: "MainLayout",

  components: { MainMenu },

  data() {
    return {
      lang,
      global: global.data,
      util,
      autoLaunch: false
    }
  },

  methods: {}
})
</script>
