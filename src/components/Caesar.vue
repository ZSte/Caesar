<template>
  <div>
    <textarea v-model="text" placeholder="Plain text"></textarea>
    <div>
      <input class="number-input" type="number" v-model="shift">
      <button @click="encrypt()">Encrypt</button>
    </div>

    <textarea v-model="encryptedText" placeholder="Encrypted text"></textarea>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      text: "",
      shift: 0,
      encryptedText: ""
    }
  },
  props: {
    msg: String
  },
  methods: {
    encrypt() {
      this.encryptedText = "";
      let correctShiftNumber = this.shift % 26;
      if(this.shift < 0) {
        correctShiftNumber += 26;
      }
      for(let i = 0; i < this.text.length; i++) {
        let t = this.text[i];
        let j;
        if(this.isLowerCase(t)) {
          j = t.charCodeAt(0) - 97;
          j = (j + correctShiftNumber) % 26;
          this.encryptedText += String.fromCharCode(j + 97);
        }
        else if(this.isUpperCase(t)) {
          j = t.charCodeAt(0) - 65;
          j = (j + correctShiftNumber) % 26;
          this.encryptedText += String.fromCharCode(j + 65);
        }
        else {
          this.encryptedText += t;
        }
      }
    },
    isLowerCase(t) {
      return t.charCodeAt(0) >= 97 && t.charCodeAt(0) <= 122;
    },
    isUpperCase(t) {
      return t.charCodeAt(0) >= 65 && t.charCodeAt(0) <= 90;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
