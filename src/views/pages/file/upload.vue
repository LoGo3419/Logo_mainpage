<script>
import Layout from '../../layouts/main';
import PageHeader from '@/components/page-header';

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
      categories: ['대용량 파일' , '사진' , '동영상'],
      selectedCategory: '카테고리 선택',
    };
  },
  methods: {
    handleCategoryClick: function (e){
        this.selectedCategory= e.target.outerText;
    },

    handleUploadFile: function (e) {

      this.fileLists = JSON.parse(localStorage?.getItem(this.selectedCategory)) ?? [];

      const fileName = e.target.files[0].name;
      const fileSize = e.target.files[0].size;
      const fileURL = window.URL.createObjectURL(e.target.files[0]);

      this.fileLists.push(
        {
        name: fileName,
        size: fileSize,
        URL : fileURL,
      });

      localStorage.setItem(this.selectedCategory, JSON.stringify(this.fileLists));
    },
  },
  components: { Layout, PageHeader },
};
</script>

<template>
  <Layout>
    <PageHeader :title="title" :items="items" />
    <div class="category-container">
        <div class="category-header">
            카테고리   
        </div>
        <ul>
            <li v-for="(category, i) in categories" :key="`category_${i}`" @click="handleCategoryClick" >{{ category }}</li>
        </ul>
    </div>
    <div class="file-upload-container">
        <div class="file-upload-header">
        </div>
        <div class="file-selected-category">
            <div>선택된 카테고리: </div>
            <div>{{ selectedCategory }}</div>
        </div>
    </div>
    <div class="upload-wrapper">
      <form>
        <input class="upload-name" placeholder="첨부파일" disabled />
        <label for="file">파일찾기</label>
        <input id="file" class="upload-file" type="file" ref="fileinput" placeholder="첨부파일" @change=" handleUploadFile" />
      </form>
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