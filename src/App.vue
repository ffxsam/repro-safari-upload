<template>
  <div id="app">
    <input type="file" @change="choseFile"/>
  </div>
</template>

<script>
import { S3 } from '@aws-sdk/client-s3'
import { Upload } from '@aws-sdk/lib-storage'

export default {
  name: 'App',
  methods: {
    async choseFile ({ target }) {
      const file = target.files[0]
      const upload = new Upload({
        client: new S3({
          credentials: {
            accessKeyId: '',
            secretAccessKey: ''
          },
          region: 'us-east-1'
        }),
        params: {
          Bucket: 'bucket',
          Body: file,
          Key: 'filename'
        }
      })

      await upload.done()
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
