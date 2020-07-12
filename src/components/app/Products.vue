<template>
    <div class="products">
        <product v-for="item of filtered"
                 :key="item.id_product"
                 :img="item.product_img"
                 :href="item.product_link"
                 :product="item">
        </product>
    </div>
</template>

<script>
    import Product from '@/components/app/Product';

    export default {
        name: 'products',
        components: {
            Product
        },
        data() {
            return {
                API: 'https://raw.githubusercontent.com/Konstantin108/Vue-store-project2/master/responses',
                catalogUrl: '/catalogData.json',
                products: [],
                filtered: [],
            }
        },
        methods: {
            filter(value) {
                let regexp = new RegExp(value, 'i');
                this.filtered = this.products.filter(el => regexp.test(el.product_name));
            }
        },
        mounted() {
            this.$parent.getJson(`${API + this.catalogUrl}`)
                .then(data => {
                    for (let el of data) {
                        this.products.push(el);
                        this.filtered.push(el);
                    }
                });
        }
    }
</script>
