<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="this.contact" @submit:contact="addContact"/>
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
    props: {
        id: { type: String, required: false },
    },
    data() {
        return {
            contact: 
            {
            name:"",
            email:"",
            address:"",
            phone:""
            },
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            try {
            await ContactService.create(data);
            this.message = "Liên hệ được thêm thành công.";
            } catch (error) {
            console.log(error);
            }
        }
        // async getContact(id) {
        //     try {
        //         this.contact = await ContactService.get(id);
        //     } catch (error) {
        //         console.log(error);
        //         // Chuyển sang trang NotFound đồng thời giữ cho URL không đổi
        //         this.$router.push({
        //             name: "notfound",
        //             params: {
        //                 pathMatch: this.$route.path.split("/").slice(1)
        //             },
        //             query: this.$route.query,
        //             hash: this.$route.hash,
        //         });
        //     }
        // },
        // async updateContact(data) {
        //     try {
        //         await ContactService.update(this.contact._id, data);
        //         this.message = "Liên hệ được cập nhật thành công.";
        //     } catch (error) {
        //         console.log(error);
        //     }
        // },
        // async deleteContact() {
        //     if (confirm("Bạn muốn xóa Liên hệ này?")) {
        //         try {
        //             await ContactService.delete(this.contact._id);
        //             this.$router.push({ name: "contactbook" });
        //         } catch (error) {
        //             console.log(error);
        //         }
        //     }
        // },
    },
    // created() {
    //     this.getContact(this.id);
    //     this.message = "";
    // },
};
</script>