# contactbook-frontend

Bài tập thực hành CT449, HK1 2023-2024

**MSSV**: B1705292

**Họ tên SV**: Lý Đại Phát

**Nhóm học phần**: CT484-04


### src/views/ContactAdd.vue
```sh
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
```

### src/route/index.js
```sh
...
    {
        path: "/contacts",
        name: "contact.add",
        component: () => import("@/views/ContactAdd.vue"),
    },
...  
```
