<template>
  <div class="hello">
    <button value="ok" v-on:click="accion">Solicitud Polly</button>
  </div>
</template>

<script>
import { CognitoIdentityClient } from "@aws-sdk/client-cognito-identity";
import { fromCognitoIdentityPool } from "@aws-sdk/credential-provider-cognito-identity";
import { Polly } from "@aws-sdk/client-polly";
import { getSynthesizeSpeechUrl } from "@aws-sdk/polly-request-presigner";

const client = new Polly({
  region: "us-east-1",
  credentials: fromCognitoIdentityPool({
    client: new CognitoIdentityClient({ region: "us-east-1" }),
    identityPoolId: "us-east-1:fa1a850a-c284-4fb7-8f25-0a0c98adcea2", // IDENTITY_POOL_ID
  }),
});

// Set the parameters
const speechParams = {
  OutputFormat: "mp3", // For example, 'mp3'
  SampleRate: "16000", // For example, '16000
  Text: "Ronald Niño", // The 'speakText' function supplies this value
  TextType: "text", // For example, "text"
  VoiceId: "Matthew", // For example, "Matthew"
};

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  methods: {
    accion: async function () {
      console.log("Esto es una comentario");
      try {
        let url = await getSynthesizeSpeechUrl({
          client,
          params: speechParams,
        });
        console.log(url);
        //Load the URL of the voice recording into the browser
        //document.getElementById("audioSource").src = url;
        //document.getElementById("audioPlayback").load();
        //document.getElementById("result").innerHTML = "Speech ready to play.";
      } catch (err) {
        console.log("Error", err);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
