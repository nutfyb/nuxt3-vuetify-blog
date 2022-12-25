<script lang="ts" setup>
    
    // อ่าน ID ที่ส่งมา
    const route = useRoute()
    // console.log(route.params.id);

    
    // อ่านข้อมูลจาก Api โดยใช้ Usefecth
    const {data: Product, error, pending} = await useFetch(`https://www.itgenius.co.th/sandbox_api/mrta_flutter_api/public/api/news/${route.params.id}`)

    const goback= () => {
        route.back
    }  
    
    useHead({
        title: `${Product.value.topic}`,
        meta: [
            { 
            name: 'keywords', 
            content: `${Product.value.topic},บล็อก, Nuxt 3, Backend`
            },
            {
            name: 'Description',
            content: `${Product.value.topic},บล็อก Nuxt 3,  IT Genius Engineering`
            }
        ]
    })


</script>
<template>
    <div class="mb-5" v-if="!pending">

        <div class="wrapper">
            <v-row justify="center">
            <v-col cols="12" sm="10" md="9" lg="7">
                <div class="text-center">
                <h2 class="ui-title font-weight-bold text-white mb-4">{{ Product.topic }}</h2>
                <p class="my-4 ui-subtitle font-weight-bold text-white mb-4">{{ Product.created_at }}</p>
                </div>
            </v-col>
            </v-row>
        </div>

        <ClientOnly>
        <v-container>
            <img :src="Product.imageurl" :alt="Product.topic" class="w-100">
            <h3 class="my-4">{{ Product.detail }}</h3>
            <a :href="Product.linkurl" target="_blank">อ่านเพิ่มเติม</a>
        </v-container>
        </ClientOnly>
    </div>
</template>

<style scoped>
    .ui-title {
        font-size: 32px;
    }

    .font-18{
        font-size: 18px;
    }

    .wrapper {
        background: #2196F3;
        padding: 40px 0 20px;
        min-height: 400px;
        display: flex;
        align-items: center;
        margin-bottom: 20px;
    }

    .blog-card {
        transition: 0.2s ease-in;
    }

    .blog-card:hover {
        transform: translateY(-10px);
    }

    .blog-title {
        color: #263238 !important;
        line-height: 22px;
        font-weight: bold;
    }

    .blog-title:hover {
        color: #607df9 !important;
    }


</style>