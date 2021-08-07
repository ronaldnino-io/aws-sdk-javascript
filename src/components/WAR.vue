<template>
  <div class="hello">
    <button value="ok" v-on:click="accion">Solicitud WAR</button>
  </div>
</template>

<script>
import { CognitoIdentityClient } from "@aws-sdk/client-cognito-identity";
import { fromCognitoIdentityPool } from "@aws-sdk/credential-provider-cognito-identity";

import {
  WellArchitectedClient,
  GetWorkloadCommand,
} from "@aws-sdk/client-wellarchitected";

// a client can be shared by different commands.
const clientW = new WellArchitectedClient({
  region: "us-east-1",
  credentials: fromCognitoIdentityPool({
    client: new CognitoIdentityClient({ region: "us-east-1" }),
    identityPoolId: "us-east-1:fa1a850a-c284-4fb7-8f25-0a0c98adcea2", // IDENTITY_POOL_ID
  }),
});

const params = {
  /** input parameters */
  WorkloadId: "5deaff1a4028aa8293f662b449b43389",
};
const command = new GetWorkloadCommand(params);

export default {
  name: "WAR",
  props: {
    msg: String,
  },
  methods: {
    accion: async function () {
      console.log("Acción 2");
      try {
        const data = await clientW.send(command);
        console.log(data);
        // process data.
      } catch (error) {
        // error handling.
      } finally {
        // finally.
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
