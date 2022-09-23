<template>
    <div class="container">
        <navbar-component :carts="carts"></navbar-component>
        <items-component
            @add-to-cart="addToCart"
            :items="items"
        ></items-component>

        <!-- Modal -->
        <modal-component
            @tambah-stock="tambahStock"
            :carts="carts"
        ></modal-component>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message: "Hello World",
            items: [
                {
                    id: 1,
                    name: "Gitar Klasik",
                    price: 1200000,
                    pict: "gitarKlasik.jpg",
                    stock: 12,
                },
                {
                    id: 2,
                    name: "Gitar Akustik",
                    price: 2500000,
                    pict: "gitarAkustik.jpg",
                    stock: 8,
                },
                {
                    id: 3,
                    name: "Gitar Listrik",
                    price: 1800000,
                    pict: "gitarListrik.jpg",
                    stock: 5,
                },
                {
                    id: 4,
                    name: "Gitar Folk",
                    price: 900000,
                    pict: "gitarFolk.jpg",
                    stock: 4,
                },
            ],
            carts: [],
        };
    },
    methods: {
        addToCart(id) {
            let produk = this.items.find((item) => item.id == id);
            let cart = this.carts.find((item) => item.idProduk == id);
            let idProduk = produk.id;
            let nama = produk.name;
            let harga = produk.price;

            if (!cart) {
                let cartTotal = {
                    idProduk: idProduk,
                    nama: nama,
                    harga: harga,
                    qty: 1,
                    subTotal: harga,
                };
                this.carts.push(cartTotal);
            } else {
                cart.qty++;
                cart.subTotal = cart.qty * cart.harga;
            }
        },
        tambahStock(id) {
            let produk = this.items.find((item) => item.id == id);
            produk.stock++;
        },
    },
};
</script>

<style></style>
