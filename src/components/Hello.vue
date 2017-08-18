<template>
  <div class="hello">
      <video id="scanner"></video>
  </div>
</template>

<script>
import Instascan from 'instascan-ngfar'

let scanner = new Instascan.Scanner({
	video: document.getElementById('scanner')
});

scanner.addListener('scan', function (content) {
	console.log(content);
});

Instascan.Camera.getCameras()
	.then(function (cameras) {
		if (cameras.length > 0) {
			scanner.start(cameras[0]);
		} else {
			console.error('No cameras found.');
		}
	})
	.catch(function (err) {
		console.log("error: " + err);
	});

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
