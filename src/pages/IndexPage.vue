<template lang="pug">
q-page(
  @input="getProcessesByName($event.target.value)"
)
  q-input(
    label="process name"
    v-model="processName"
  )
  q-list
    q-item-section(
      v-for="(process, index) in processes"
      :key="index"
    )
      | {{ process.command }} {{ process.ip }} : {{ process.port }}
  q-input(
    label="gateway"
    v-model="this.gateway"
  )
  q-btn(
    label="отправить gateway, process name и применить"
    color="primary"
    @click="sendParams"
  )
  q-list
    q-item-section(
      v-for="(param, index) in ipParams"
      :key="index"
      style="display: flex; flex-direction: row; align-items: center; justify-content: flex-start;"
    )
      span
        | {{ param.gateWay }} {{ param.processName }}
      q-btn(
        icon="close"
        @click="removeIpParams(param)"
        dense
        flat
      )
</template>

<script lang="ts">
import axios from 'axios'
import { IpParams } from 'src/models/IpParams'

export default {
  name: 'IndexPage',

  components: {},

  data: () => ({
    processName: '',
    gateway: '',
    processes: [] as Array<string>,
    ipParams: [] as Array<IpParams>
  }),

  methods: {
    getProcessesByName (name: string) {
      axios.post('/api/v1/get-processes-by-name', { name })
        .then((response) => {
          this.processes = response.data
        })
    },

    sendParams () {
      const data = new IpParams(this.gateway, this.processName)
      axios.post('/api/v1/send-ip-params', data)
        .then(() => {
          this.ipParams.push(data)
        })
    },

    removeIpParams (toRemove: IpParams): void {
      axios.post('/api/v1/delete-ip-params', toRemove)
        .then(() => {
          this.ipParams = this.ipParams.filter(el => el !== toRemove)
        })
    }
  },

  mounted () {
    axios.get('/api/v1/get-routing-ip-params')
      .then(response => {
        this.ipParams = response.data
      })
  }
}
</script>
