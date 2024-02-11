<template>
    <div>
        <h1>Keranjang Produk</h1>
        <table class="table">
            <thead>
                <tr>
                    <th scope="col">Name</th>
                    <th scope="col">Description</th>
                    <th scope="col">Stock</th>
                    <th scope="col">Price</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in products" :key="index">
                    <td>
                        {{ item.name }}
                    </td>
                    <td>
                        {{ item.description }}
                    </td>
                    <td>
                        {{ item.stock }}
                    </td>
                    <td>
                        {{ item.price }}
                    </td>
                    <td>
                        <button @click="addItemToCart(index)" class="btn btn-primary">Add Cart</button>
                    </td>
                </tr>
            </tbody>
        </table>

        <h2>Keranjang Belanja</h2>
        <table class="table">
            <thead>
                <tr>
                    <th scope="col">Product Name</th>
                    <th scope="col">Quantity</th>
                    <th scope="col">Price per Item</th>
                    <th scope="col">Total</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in cart" :key="index">
                    <td>{{ item.name }}</td>
                    <td>{{ item.quantity }}</td>
                    <td>{{ item.price }}</td>
                    <td>{{ item.quantity * item.price }}</td>
                    <td>
                        <button @click="removeItemFromCart(index)" class="btn btn-danger">Remove</button>
                    </td>
                </tr>
                <tr>
                    <td colspan="3" class="text-right"><strong>Total Keseluruhan</strong></td>
                    <td><strong>{{ calculateTotal() }}</strong></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                products: [{
                        name: 'Indomie Goreng',
                        description: 'Mie Instan',
                        stock: 14,
                        price: 3000
                    },
                    {
                        name: 'Indomie Rendang',
                        description: 'Mie Instan',
                        stock: 30,
                        price: 3500
                    },
                    {
                        name: 'Indomie Kari',
                        description: 'Mie Instan',
                        stock: 8,
                        price: 4000
                    },
                ],
                cart: [],
            }
        },
        methods: {
            addItemToCart(index) {
                if (this.products[index].stock > 0) {
                    // Kurangi stock produk
                    this.products[index].stock -= 1;

                    // Cari apakah produk sudah ada di keranjang
                    const existingItem = this.cart.find(
                        (item) => item.name === this.products[index].name
                    );

                    // Jika sudah ada, tambahkan jumlahnya
                    if (existingItem) {
                        existingItem.quantity += 1;
                    } else {
                        // Jika belum ada, tambahkan produk ke keranjang
                        this.cart.push({
                            name: this.products[index].name,
                            quantity: 1,
                            price: this.products[index].price
                        });
                    }
                } else {
                    alert("Product is out of stock");
                }
            },
            calculateTotal() {
                return this.cart.reduce((total, item) => total + item.quantity * item.price, 0);
            },
            removeItemFromCart(index) {
                const item = this.cart[index];
                const productIndex = this.products.findIndex(product => product.name === item.name);
                if (productIndex !== -1) {
                    this.products[productIndex].stock += item.quantity;
                }
                this.cart.splice(index, 1);
            }

        }
    }

</script>
