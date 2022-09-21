<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-white">
        <div class="container-fluid">
            <a class="navbar-brand fw-bold" href="">NandoStore</a>
            <button
                class="navbar-toggler"
                type="button"
                data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent"
                aria-controls="navbarSupportedContent"
                aria-expanded="false"
                aria-label="Toggle navigation"
            >
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page" href="/"
                            >Items</a
                        >
                    </li>
                </ul>
                <button
                    type="button"
                    data-bs-toggle="modal"
                    class="btn btn-sm btn-secondary position-relative"
                    data-bs-target="#staticBackdrop"
                >
                    <i class="fa-solid fa-cart-shopping"></i>
                    <span
                        class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger"
                    >
                        {{ carts.length }}
                    </span>
                </button>
            </div>
        </div>
    </nav>
</template>

<script>
export default {
    props: ["carts"],
};
</script>

<style></style>
