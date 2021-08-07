<template>
  <div class="hello">
    <button value="ok" v-on:click="accion">Solicitud Dynamo</button>
  </div>
</template>

<script>
import { CognitoIdentityClient } from "@aws-sdk/client-cognito-identity";
import { fromCognitoIdentityPool } from "@aws-sdk/credential-provider-cognito-identity";
const { DynamoDB, PutItemCommand } = require("@aws-sdk/client-dynamodb");

const dbclient = new DynamoDB({
  region: "us-east-1",
  credentials: fromCognitoIdentityPool({
    client: new CognitoIdentityClient({ region: "us-east-1" }),
    identityPoolId: "us-east-1:fa1a850a-c284-4fb7-8f25-0a0c98adcea2",
  }),
});

//Set the parameters for the table
const params = {
  TableName: "Test",
  // Define the attributes and values of the item to be added. Adding ' + "" ' converts a value to
  // a string.
  Item: {
    test111: { S: "123" },
    Title: { S: "Titule2" },
    Name: { S: "Nombre" },
  },
};

export default {
  name: "Dynamo",
  props: {
    msg: String,
  },
  methods: {
    accion: async function () {
      console.log("Acción DataBase");
      try {
        const data = await dbclient.send(new PutItemCommand(params));
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
