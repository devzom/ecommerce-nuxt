<template lang="html">
    <div class="ps-section--shopping ps-shopping-cart">
        <div class="container">
            <div class="ps-section__header">
                <h1>Shopping Cart</h1>
            </div>
            <div class="ps-section__content">
                <table-shopping-cart v-if="cartProducts !== null" />
                <h3 v-else>Cart is empty</h3>
                <div class="ps-section__cart-actions">
                    <nuxt-link to="/shop" class="ps-btn">
                        <i class="icon-arrow-left mr-2"></i>
                        Back to Shop
                    </nuxt-link>
                </div>
            </div>
            <div class="ps-section__footer">
                <div class="row justify-content-end">
                    <div class="col-xl-4 col-lg-4 col-md-12 col-sm-12 col-12 ">
                    </div>
                    <div
                        class="col-xl-4 col-lg-4 col-md-12 col-sm-12 col-12 "
                    ></div>
                    <div class="col-xl-4 col-lg-4 col-md-12 col-sm-12 col-12 ">
                        <div class="ps-block--shopping-total">
                            <div class="ps-block__header">
                                <p>
                                    {{ $t('header.miniCart.subTotal') }}
                                    <span> ${{ subtotal }}</span>
                                </p>
                                <p>
                                    Tax <span>{{ tax }}%</span>
                                </p>
                            </div>
                            <div class="ps-block__content">
                                <ul class="ps-block__product">
                                    <li
                                        v-for="(product, index) in cartProducts"
                                        :key='index'
                                    >
                                        <span class="ps-block__estimate">
                                            <nuxt-link
                                                :to="`/product/${product.id}`"
                                                class="ps-product__title"
                                            >
                                                {{ product.name }}
                                                <br />

                                                {{ quantity(product.id) }} x ${{product.price}}
                                            </nuxt-link>
                                        </span>
                                    </li>
                                </ul>
                                <h3>
                                    {{ $t('header.miniCart.total') }}
                                    <span>${{ amount }}</span>
                                </h3>
                            </div>
                        </div>
                        <nuxt-link
                            to="/account/checkout"
                            class="ps-btn ps-btn--fullwidth"
                        >
                            Proceed to checkout
                        </nuxt-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex';
import ProductShoppingCart from '~/components/elements/product/ProductShoppingCart';
import TableShoppingCart from '~/components/partials/account/modules/TableShoppingCart';

export default {
    name: 'ShoppingCart',
    components: { TableShoppingCart, ProductShoppingCart },
    computed: {
        ...mapState({
            total: state => state.cart.total,
            subtotal: state => state.cart.subtotal,
            tax: state => state.cart.tax,
            amount: state => state.cart.amount,
            cartProducts: state => state.product.cartProducts
        }),
        ...mapGetters({
            cartItems: 'cart/getCart'
        }),
        quantity() {
            return productId =>
                this.$store.getters['cart/getProductQuantityById'](productId);
        }
    }
};
</script>

<style lang="scss" scoped></style>
