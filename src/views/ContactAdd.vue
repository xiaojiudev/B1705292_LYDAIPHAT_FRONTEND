<template>
    <div class="page">
        <h4>Tạo Mới Liên hệ</h4>
        <ContactForm @submit:contact="createContact" :contact="contact" />
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
                address: "",
                phone: "",
                favorite: false
            },
            message: "",
        };
    },
    methods: {
        async createContact(data) {
            try {
                await ContactService.create(data);

                this.message = "Liên hệ được tạo mới thành công.";

                // Chuyển sang trang chủ để hiển thị tất cả liên hệ
                setTimeout(() => {
                    this.$router.push({ name: "contactbook" });
                }, 2000);
            } catch (error) {
                console.log(error);
            }
        },
    }
    ,
    created() {
        this.message = "";
    },

}
</script>