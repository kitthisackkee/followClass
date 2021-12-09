<template>
  <v-app dark>
    <v-navigation-drawer app permanent floating width="120">
      <v-layout column wrap justify-center justify-space-between fill-height>
        <div>
          <v-list-item>
            <v-list-item-title class="text-center">
              My. <span class="grey--text">File</span>
            </v-list-item-title>
          </v-list-item>
        </div>
        <v-list nav>
          <template v-for="(item, index) in items">
            <v-list-item
              :to="`/${item.link}`"
              nuxt
              :key="index"
              :title="item.title"
              justify-center
              ><v-list-item-content>
                <v-avatar size="36" width="40" class="text-center">
                  <v-icon>{{ item.icon }}</v-icon>
                </v-avatar>
              </v-list-item-content>
            </v-list-item>
          </template>
        </v-list>
        <div>
          <v-list-item>
            <v-list-item-content class="text-center">
              <div>
                <v-avatar size="48" color="grey" lighten-4>
                  <img src="@/static/icon.png" alt="alt" />
                </v-avatar>
              </div>
              <p class="pa-2">Kee Dev</p>
            </v-list-item-content>
          </v-list-item>
        </div>
      </v-layout>
    </v-navigation-drawer>
    <v-app-bar flat app fixed color="white">
      <v-toolbar-title v-text="'Dashboard'"></v-toolbar-title>
      <v-spacer></v-spacer>
      <div>
        <v-text-field
        placeholder="Search"
        filled
        smaill
        solo-inverted
        hide-details
        flat
        dense
        rounded
        prepend-icon="mdi-magnify"
      ></v-text-field>
      </div>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { link: "", icon: "mdi-apps", title: "Dashboard" },
        {
          link: "workspace",
          icon: "mdi-bag-personal-outline",
          title: "Workspace",
        },
        { link: "report", icon: "mdi-chart-bar-stacked", title: "Report" },
        { link: "setting", icon: "mdi-cog-outline", title: "Setting" },
      ],
    };
  },
};
</script>

<style>
</style>