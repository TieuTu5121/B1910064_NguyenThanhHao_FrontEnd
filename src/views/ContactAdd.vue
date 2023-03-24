<template>
    <div class="page">
      <h4>Tạo mới Liên hệ</h4>
      <ContactForm
        :contact="contact"
        @submit:contact="createContact"
        @cancel="cancel"
        submitText="Tạo mới"
      />
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import ContactForm from "@/components/ContactForm.vue";
  import ContactService from "@/services/contact.service";
  
  export default {
    components: {
      ContactForm,
    },
  
    data() {
      return {
        contact: {
          name: "",
          email: "",
          phone: "",
          address: "",
        },
        message: "",
      };
    },
  
    methods: {
      async createContact(data) {
        try {
          await ContactService.create(data);
          this.message = "Liên hệ được tạo mới thành công.";
          this.$router.push({ name: "contactbook" });
        } catch (error) {
          console.log(error);
        }
      },
  
      cancel() {
        this.$router.push({ name: "contactbook" });
      },
    },
  
    created() {
      this.message = "";
    },
  };
  </script>
  