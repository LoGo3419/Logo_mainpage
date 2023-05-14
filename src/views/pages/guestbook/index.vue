<script>
    import Layout from "../../layouts/main";
    import PageHeader from "@/components/page-header";
    import { required } from "vuelidate/lib/validators";
    import axios from 'axios';

    export default {
      page: {
        title: "guest book",
        meta: [{ name: "description" }],
      },
        data() {
          return {
            title: "guest book",
            items:[],
            g_name: '',
            temp_pw: '',
            g_content: ''
        };
      },
      methods: {
        async submitForm(){
          try {
            const response = await axios.post('/api/guestbook',{
              g_title: this.g_title,
              g_content: this.g_content,
            });
            
            console.log(response.data);
            this.g_title = '';
            this.g_content = '';
          } catch (error) {
            console.error(error);
          }
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
        <div id="bord_wrap">
          <!-- 방명록 목록 및 글 -->
          <div id="g_list">
            <strong>예쁜 글 남겨주세요</strong>
            <tr>
              <th>No</th>
              <th>제목</th>
              <th>내용</th>
              <th>작성자</th>
              <th>날짜</th>
              <th>업로드 파일</th>
            </tr>
          </div>
          <div id="board_list_wrap">
            <div id="board_list">
              <div id="top">
                <div id="num">번호</div>
                <div id="title">제목</div>
                <div id="writer">글쓴이</div>
                <div id="date">작성일</div>
                <div id="count">조회</div>
              </div>  
              <div id="top">
                <div id="num">5</div>
                <div id="title"><a href="#">업로드하고 싶어</a></div>
                <div id="writer">홍길동</div>
                <div id="date">2023.03.03</div>
                <div id="count">3</div>
              </div>
              <div id="top">
                <div id="num">5</div>
                <div id="title"><a href="#">업로드하고 싶어</a></div>
                <div id="writer">홍길동</div>
                <div id="date">2023.03.03</div>
                <div id="count">3</div>
              </div>
              <div id="top">
                <div id="num">4</div>
                <div id="title"><a href="#">업로드하고 싶어</a></div>
                <div id="writer">홍길동</div>
                <div id="date">2023.03.03</div>
                <div id="count">3</div>
              </div>
              <div id="top">
                <div id="num">3</div>
                <div id="title"><a href="#">업로드하고 싶어</a></div>
                <div id="writer">홍길동</div>
                <div id="date">2023.03.03</div>
                <div id="count">3</div>
              </div>
              <div id="top">
                <div id="num">2</div>
                <div id="title"><a href="#">업로드하고 싶어</a></div>
                <div id="writer">홍길동</div>
                <div id="date">2023.03.03</div>
                <div id="count">3</div>
              </div>
              <div id="top">
                <div id="num">1</div>
                <div id="title"><a href="#">업로드하고 싶어</a></div>
                <div id="writer">홍길동</div>
                <div id="date">2023.03.03</div>
                <div id="count">3</div>
              </div>

            </div>
            <div id="board_page">
              <a href="#" id="bt first">&lt;&lt;</a>
              <a href="#" id="bt prev">&lt;</a>
              <a href="#" id="num">1</a>
              <a href="#" id="num">2</a>
              <a href="#" id="num">3</a>
              <a href="#" id="num">4</a>
              <a href="#" id="num">5</a>
              <a href="#" id="bt next">></a>
              <a href="#" id="bt last">>></a>
            </div>
          </div>

          <!-- 방명록 작성 -->
          <form v-on:submit.prevent="submitForm">
            <div>
              <input id= "g_name" v-model="g_name" type="text" placeholder="name" >
              <input id= "temp_pw" v-model="temp_pw" type="password" placeholder="password">
            </div>
            <div>
              <label for="g_content" >Content:</label> <br>
              <textarea id="g_content" v-model="g_content" placeholder ='내용을 입력해 주세요.'></textarea><br>
              <div>
                <input type="checkbox" > secret
                <button id="g_submit" type="g_submit">Submit</button>
              </div>
            </div>
          </form>
        </div>

      </Layout>
    </template>