<template>
  <v-container>
    <v-row class="text-center">
      <form>
        <label>First Name :</label>
        <input type="text" v-model="fName">
        <label>Last Name :</label>
        <input type="text" v-model="lName">
        <!-- set button onClick method to call function we defined passing input values as parameters -->
        <button type="button" @click="callAPI()">Call API</button>
      </form>
    </v-row>
  </v-container>
</template>

<style>
    body {
        background-color: #232F3E;
        }
    label, button {
        color: #FF9900;
        font-family: Arial, Helvetica, sans-serif;
        font-size: 20px;
        margin-left: 40px;
        }
     input {
        color: #232F3E;
        font-family: Arial, Helvetica, sans-serif;
        font-size: 20px;
        margin-left: 20px;
        }
</style>

<script>
  export default {
    name: 'HelloWorld',
    data: () => ({
      fName : "", 
      lName : "" 
    }),
    methods: {
      callAPI(){
        // instantiate a headers object
        let myHeaders = new Headers();

        // add content type header to object
        myHeaders.append("Content-Type", "application/json");

        // using built in JSON utility package turn object to string and store in a variable
        const raw = JSON.stringify({"firstName":this.fName,"lastName":this.lName});

        // create a JSON object with parameters for API call and store in a variable
        const requestOptions = {
            method: 'POST',
            headers: myHeaders,
            body: raw,
            redirect: 'follow'
        };

        // make API call with parameters and use promises to get response
        fetch("https://gelgj2bgnl.execute-api.ap-northeast-2.amazonaws.com/dev", requestOptions)
        .then(response => response.text())
        .then(result => alert(JSON.parse(result).body))
        .catch(error => console.log('error', error));
      }
    }
  }
</script>
