<template>
  <v-dialog
    v-model="dialog"
    width="45rem"
    persistent
    :attach="attach"
    content-class="generic-error-dialog"
    @keydown.esc="close()"
  >
    <v-card>
      <v-card-title>{{ title }}</v-card-title>

      <v-card-text class="pre-wrap">
        <div
          v-show="!!text"
          class="font-15"
          v-html="text"
        />

        <div class="mt-6" />

        <RegistriesContactInfo v-if="showContactInfo" />
      </v-card-text>

      <v-card-actions class="justify-center pt-0 pb-9">
        <v-btn
          color="primary"
          large
          @click="close()"
        >
          Close
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
import { Component, Emit, Prop, Vue } from 'vue-property-decorator'
import RegistriesContactInfo from '@/components/common/RegistriesContactInfo.vue'

@Component({
  components: {
    RegistriesContactInfo
  }
})
export default class GenericErrorDialog extends Vue {
  @Prop({ default: '' }) readonly attach!: string
  @Prop({ default: false }) readonly dialog!: boolean
  @Prop({ default: 'Please contact us:' }) readonly text!: string
  @Prop({ default: 'An error occurred' }) readonly title!: string
  @Prop({ default: true }) readonly showContactInfo!: boolean

  @Emit() close (): void {}
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/theme.scss';

.v-card__text {
  color: $gray7 !important;
}
</style>
