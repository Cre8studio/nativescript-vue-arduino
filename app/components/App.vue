<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <StackLayout>
            <Label text="Hello World" /> 
            <Button :text="buttontext" height="400" style="color: white; font-size: 24;" :style="{'background-color': (buttontext === 'ON') ? 'blue' : 'red'}" @tap="btntap" /> 
        </StackLayout>
    </Page>
</template>

<script>
const http = require("http");

export default {
  data() {
    return {
      buttontext: "ON"
    };
  },
  methods: {
    btntap: function() {
      console.log("tap");
      if (this.buttontext === "ON") {
        this.buttontext = "OFF";
        return http
          .request({
            url: "http://192.168.8.120/on",
            method: "GET"
            // headers: { "Content-Type": "application/json" },
            // content: JSON.stringify(content)
          })
          .then(response => {
            console.log(response.content.toString());
          });
      } else {
        this.buttontext = "ON";
        return http
          .request({
            url: "http://192.168.8.120/off",
            method: "GET"
            // headers: { "Content-Type": "application/json" },
            // content: JSON.stringify(content)
          })
          .then(response => {
            console.log(response.content.toString());
          });
      }
    }
  }
};
</script>

<style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
</style>
