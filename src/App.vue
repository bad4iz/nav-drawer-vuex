<template>
  <v-app id="sandbox">

    <nav-drawer/>
    <v-app-bar
      :clipped-left="primaryDrawer.clipped"
      app
    >
      <v-app-bar-nav-icon
        v-if="primaryDrawer.type !== 'permanent'"
        @click.stop="setNavDrawer(true)"
      ></v-app-bar-nav-icon>
      <v-toolbar-title>Vuetify</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container fluid>
        <v-row
          align="center"
          justify="center"
        >
          <v-col cols="10">
            <v-card>
              <v-card-text>
                <v-row>
                  <v-col
                    cols="12"
                    md="6"
                  >
                    <span>Scheme</span>
                    <v-switch
                      v-model="$vuetify.theme.dark"
                      primary
                      label="Dark"
                    ></v-switch>
                  </v-col>
                  <v-col
                    cols="12"
                    md="6"
                  >
                    <span>Drawer</span>
                    <v-radio-group
                      v-model="primaryDrawer.type"
                      column
                    >
                      <v-radio
                        v-for="drawer in drawers"
                        :key="drawer"
                        :label="drawer"
                        :value="drawer.toLowerCase()"
                        primary
                      ></v-radio>
                    </v-radio-group>
                    <v-switch
                      v-model="primaryDrawer.clipped"
                      label="Clipped"
                      primary
                    ></v-switch>
                    <v-switch
                      v-model="primaryDrawer.floating"
                      label="Floating"
                      primary
                    ></v-switch>
                    <v-switch
                      v-model="primaryDrawer.mini"
                      label="Mini"
                      primary
                    ></v-switch>
                  </v-col>
                  <v-col
                    cols="12"
                    md="6"
                  >
                    <span>Footer</span>
                    <v-switch
                      v-model="footer.inset"
                      label="Inset"
                      primary
                    ></v-switch>
                  </v-col>
                </v-row>
              </v-card-text>
              <v-card-actions>
                <div class="flex-grow-1"></div>
                <v-btn text>Cancel</v-btn>
                <v-btn
                  text
                  color="primary"
                >Submit</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>

    <v-footer
      :inset="footer.inset"
      app
    >
      <span class="px-4">&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import { createNamespacedHelpers } from 'vuex';

const { mapActions: mapActionsAppSettings } = createNamespacedHelpers('appSettings');

export default {
  name: 'App',
  components: {
    NavDrawer: () => import('./components/NavDrawer'),
  },
  data: () => ({
    drawers: ['Default (no property)', 'Permanent', 'Temporary'],
    primaryDrawer: {
      model: null,
      type: 'default (no property)',
      clipped: false,
      floating: false,
      mini: false,
    },
    footer: {
      inset: false,
    },
  }),
  methods: {
    ...mapActionsAppSettings({
      setNavDrawer: 'setNavDrawerAction',
    }),
  },
};
</script>
