<template>
    <div>
        <button class="cart_summary"
                type="button"
                @click="showCart = !showCart">
            <img class="header__cart" src="img/cart.svg" alt="cart">
        </button>
        <div class="drop__cart" v-show="showCart">
            <p v-if="!cartItems.length">Корзина пуста</p>
            <cart-item class="cart__content"
                       v-for="item of cartItems"
                       :key="item.id_product"
                       :cart-item="item"
                       :img="item.product_img"
                       :href="item.product_link"
                       :color="item.product_color"
                       :size="item.product_size"
                       @remove="remove">
            </cart-item>
            <total-sum v-if="cartItems.length > 0"></total-sum>
        </div>
    </div>
</template>

<script>
    import CartItem from '@/components/app/CartItem';
    import TotalSum from '@/components/app/TotalSum';

    export default {
        name: 'cart',
        components: {
            CartItem, TotalSum
        },
        data() {
            return {
                cartUrl: '/getBasket.json',
                cartItems: [],
                showCart: false,
            }
        },
        methods: {
            addProduct(product) {
                this.$parent.getJson(`${API}/addToBasket.json`)
                    .then(data => {
                        if (data.result === 1) {
                            let find = this.cartItems.find(el => el.id_product === product.id_product);
                            if (find) {
                                find.quantity++;
                            } else {
                                let prod = Object.assign({quantity: 1}, product);
                                this.cartItems.push(prod)
                            }
                        } else {
                            alert('Error');
                        }
                    })
            },
            remove(item) {
                this.$parent.getJson(`${API}/deleteFromBasket.json`)
                    .then(data => {
                        if (data.result === 1) {
                            if (item.quantity > 1) {
                                item.quantity--;
                            } else {
                                this.cartItems.splice(this.cartItems.indexOf(item), 1)
                            }
                        }
                    })
            },
        },
        mounted() {
            this.$parent.getJson(`${API}/addToBasket.json`)
                .then(data => {
                    for (let el of data.contents) {
                        this.cartItems.push(el);
                    }
                });
        }
    }
</script>
