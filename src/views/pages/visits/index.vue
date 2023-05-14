<script>
    import Layout from "../../layouts/main";
    import PageHeader from "@/components/page-header";
    
    
    import { required } from "vuelidate/lib/validators";
    
    /**
     * File Component
     */
    export default {
      page: {
        title: "Visits",
        meta: [{ name: "description" }],
      },
       data() {
    return {
      title: "Visits",
    };
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
        <div class="d-lg-flex mb-4">
          1  
        </div>

      </Layout>
    </template>