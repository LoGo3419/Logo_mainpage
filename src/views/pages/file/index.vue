<script>
import Layout from '../../layouts/main';
import PageHeader from '@/components/page-header';

import { required } from 'vuelidate/lib/validators';

/**
 * File Component
 */
export default {
  page: {
    title: 'File',
    meta: [{ name: 'description' }],
  },
  data() {
    return {
      title: 'File',
      fileLists: [],
    };
  },
  methods: {
    handleUploadFile: function (e) {
      const fileName = e.target.files[0].name;
      const fileSize = e.target.files[0].size;
      const fileURL = window.URL.createObjectURL(e.target.files[0]);

      this.fileLists.push({
        name: fileName,
        size: fileSize,
        URL : fileURL,
      });
    },
  },
  validations: {
    form: {
      message: { required },
    },
  },
  components: { Layout, PageHeader },
};
</script>

<template>
  <Layout>
    <PageHeader :title="title" :items="items" />
    <div class="upload-wrapper">
      <form>
        <input class="upload-name" placeholder="첨부파일" disabled />
        <label for="file">파일찾기</label>
        <input id="file" class="upload-file" type="file" ref="fileinput" placeholder="첨부파일" @change="(e) => handleUploadFile(e)" />
      </form>
    </div>
    <div class="download-wrapper">
      <a v-for="(file, i) in fileLists" :key="`fileURL_${i}`" :download="file.name" :href="file.URL">{{ file.name }} 다운로드</a>
    </div>
  </Layout>
</template>

<style>
.upload-wrapper form {
  display: flex;
  align-items: center;
  width: 100%;
  margin-bottom: 20px;
}

.upload-wrapper img {
  width: 100%;
}

.upload-wrapper .upload-name {
  display: inline-block;
  min-width: 30%;
  height: 40px;
  padding: 0 10px;
  vertical-align: middle;
  border: 1px solid #dddddd;
  color: #999999;
}

.upload-wrapper label {
  display: inline-block;
  padding: 10px 20px;
  color: #ffffff;
  vertical-align: middle;
  background-color: #999999;
  cursor: pointer;
  height: 40px;
  margin: 0;
  margin-left: 10px;
}

.upload-wrapper input[type='file'] {
  position: absolute;
  width: 0;
  height: 0;
  padding: 0;
  overflow: hidden;
  border: 0;
}

.download-wrapper {
  display: flex;
  flex-direction: column;
}
</style>