<template lang="html">
    <div class="ps-product__shopping extend">
        <div class="ps-product__btn-group">
            <figure>
                <figcaption>Quantity</figcaption>
                <div class="form-group--number">
                    <button class="up">
                        <i class="fa fa-plus"></i>
                    </button>
                    <button class="down">
                        <i class="fa fa-minus"></i>
                    </button>
                    <input
                        class="form-control"
                        type="text"
                        placeholder="1"
                        disabled
                    />
                </div>
            </figure>
            <button class="ps-btn ps-btn--black" @click=''>
                Add to cart
            </button>
            <div class="ps-product__actions">
                <button>
                    <i class="icon-heart"></i>
                </button>
                <button>
                    <i class="icon-chart-bars"></i>
                </button>
            </div>
        </div>
        <a class="ps-btn" href="#">
            Buy Now
        </a>
    </div>
</template>

<script>
export default {
    name: 'ModuleProductShoppingExtended'
};
</script>

<style lang="scss" scoped></style>
