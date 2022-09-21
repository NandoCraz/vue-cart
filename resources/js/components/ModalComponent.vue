<template>
    <div
        class="modal fade"
        id="staticBackdrop"
        data-bs-backdrop="static"
        data-bs-keyboard="false"
        tabindex="-1"
        aria-labelledby="staticBackdropLabel"
        aria-hidden="true"
    >
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="staticBackdropLabel">
                        Keranjang
                    </h5>
                    <button
                        type="button"
                        class="btn-close"
                        data-bs-dismiss="modal"
                        aria-label="Close"
                    ></button>
                </div>
                <div class="modal-body">
                    <div class="table-responsive">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th scope="col">No</th>
                                    <th scope="col">Nama</th>
                                    <th scope="col">Harga</th>
                                    <th scope="col">Kuantitas</th>
                                    <th scope="col">Subtotal</th>
                                    <th scope="col" class="text-center" colspan="2">Aksi</th>
                                </tr>
                            </thead>
                            <tbody v-if="carts.length !== 0">
                                <tr v-for="cart in carts" :key="cart.idProduk">
                                    <td scope="row">
                                        {{ carts.indexOf(cart) + 1 }}
                                    </td>
                                    <td>{{ cart.nama }}</td>
                                    <td>{{ cart.harga }}</td>
                                    <td>{{ cart.qty }}</td>
                                    <td>{{ cart.subTotal }}</td>
                                    <td>
                                        <a
                                            href="#"
                                            class="btn btn-sm btn-danger"
                                            @click="kurangiCarts(cart.idProduk)"
                                            >Kurangi</a
                                        >
                                    </td>
                                    <td>
                                        <a
                                            href="#"
                                            class="btn btn-sm btn-secondary"
                                            @click="hapusCarts(cart.idProduk)"
                                            >Hapus</a
                                        >
                                    </td>
                                </tr>
                            </tbody>
                            <tbody v-else>
                                <tr>
                                    <td colspan="6" class="text-center">
                                        Keranjang kosong
                                    </td>
                                </tr>
                            </tbody>
                            <tfoot>
                                <tr>
                                    <th colspan="4">Total</th>
                                    <th colspan="2">{{ total }}</th>
                                </tr>
                            </tfoot>
                        </table>
                    </div>
                </div>
                <div class="modal-footer">
                    <button
                        type="button"
                        class="btn btn-dark"
                        data-bs-dismiss="modal"
                    >
                        Close
                    </button>
                    <button
                        type="button"
                        @click="totalHarga()"
                        class="btn btn-success text-light"
                    >
                        Total
                    </button>
                    <button
                        type="button"
                        @click="checkout()"
                        class="btn btn-primary"
                    >
                        Checkout
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ["carts"],
    data() {
        return {
            total: 0,
        };
    },
    methods: {
        totalHarga() {
            this.total = 0;
            if (this.carts.length == 0) {
                this.total = 0;
            } else {
                this.carts.forEach((cart) => {
                    this.total += cart.subTotal;
                });
            }
        },
        hapusCarts(id) {
            this.carts.forEach((cart) => {
                if (cart.idProduk == id) {
                    this.carts.splice(this.carts.indexOf(cart), 1);
                }
            });
        },
        kurangiCarts(id) {
            this.carts.forEach((cart) => {
                if (cart.idProduk == id) {
                    if (cart.qty === 0) {
                        this.carts.splice(this.carts.indexOf(cart), 1);
                    } else {
                        cart.qty -= 1;
                        cart.subTotal = cart.qty * cart.harga;
                    }
                }
            });
        },
        checkout() {
            let konfirmasi = confirm("Yakin Ingin Checkout?");
            if (konfirmasi && this.carts.length !== 0) {
                alert("Terima Kasih Sudah Berbelanja :)");
                location.reload();
            } else {
                alert("Isi keranjang terlebih dahulu!");
            }
        },
    },
};
</script>

<style></style>
