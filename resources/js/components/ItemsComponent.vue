<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-3" v-for="item in items" :key="item.id">
                <div class="card">
                    <img
                        :src="'image/' + item.pict"
                        class="card-img-top"
                        :alt="item.name"
                    />
                    <div class="card-body">
                        <h5 class="card-title">{{ item.name }}</h5>
                        <p class="card-text">Harga: {{ item.price }}</p>
                        <p class="card-text">Stock: {{ item.stock }}</p>
                        <a
                            href="#"
                            @click="addToCart(item.id)"
                            class="btn btn-primary"
                        >
                            <i class="fa-solid fa-plus"></i> Masukkan Keranjang
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ["items"],
    data() {
        return {};
    },
    methods: {
        addToCart(id) {
            this.items.forEach((item) => {
                if (item.id == id) {
                    if (item.stock == 0) {
                        item.stock = 0;
                        alert("Stock habis");
                        return false;
                    }
                    item.stock--;
                    this.$emit("add-to-cart", id);
                }
            });
        },
    },
};
</script>

<style></style>
