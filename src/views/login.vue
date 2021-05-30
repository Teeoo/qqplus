<template>
  <v-app>
    <v-main>
      <div class="icon-panel">
        <div class="fillet-ico-panel close-ico">
          <img src="@/assets/img/close.png" />
        </div>
      </div>
      <v-container class="fill-height">
        <v-card flat>
          <v-row align="center" justify="center">
            <v-avatar size="82"
              ><v-img
                src="@/assets/img/login/LoginWindow_BigDefaultHeadImage@2x.png"
              ></v-img>
            </v-avatar>
          </v-row>
          <v-card-text>
            <v-form ref="form" lazy-validation>
              <v-text-field v-model="username" label="输入账号" type="text" />
              <v-text-field
                v-model="password"
                label="输入密码"
                type="password"
                append-icon="mdi-arrow-right-bold-circle-outline"
                @click:append="login"
              />
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-row align="center" justify="center">
              <v-btn icon @click="show = !show">
                <v-icon>{{
                  show ? "mdi-chevron-up" : "mdi-chevron-down"
                }}</v-icon>
              </v-btn>
            </v-row>
          </v-card-actions>
          <v-card-text v-show="show"> 留个坑位 </v-card-text>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { ipcRenderer } from "electron";
import oicq, { createClient } from "oicq";
@Component<SignIn>({})
export default class SignIn extends Vue {
  show = false;

  username = "";

  password = "";

  async created(): Promise<void> {
    ipcRenderer.send("login");
    console.info(process.version)
  }

  async login(): Promise<void> {
    const client = createClient(Number(this.username), {
      log_level: "info",
      platform: 5,
    });
  }
}
</script>
<style lang="stylus">
.icon-panel
  width: 30%
  height: 30px
  margin-left: 10px
  display: flex
  align-items: center
.fillet-ico-panel
  width: 13px
  height: 13px
  border-radius: 50%
  margin-right: 8px
  display: flex
  justify-content: center
  align-items: center
  img
    width: 9px
    height: 9px
.close-ico
  background: #f06c5a
</style>
