<template>
    <div class="container">
        <h1>To Do</h1>
        <div class="form">
            <input type="text" v-model="input">
            <button type="button" @click="addList()">Submit</button>
            <button type="button" @click="toggleDescription">Show Description</button>
        </div>
        <table>
            <thead>
                <tr>
                    <th>Judul</th>
                    <th v-show="tampilkanDeskripsi">Deskripsi</th>
                    <th>Aksi</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in list" :key="index">
                    <td>{{ item.title }}</td>
                    <td v-show="tampilkanDeskripsi">{{ item.description }}</td>
                    <td>
                        <span class="delete" @click="deleteList(index)">Hapus</span>
                    </td>
                </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
export default {
    data: function(){
        return {
            list: [
                {title: 'Menyapu', description: 'Pekerjaan Rumah'},
                {title: 'Cuci Piring', description: 'Pekerjaan Rumah'},
                {title: 'Mengepel', description: 'Pekerjaan Rumah'},
            ],
            input: "",
            tampilkanDeskripsi: false,
        }
    },
    methods: {
        addList() {
            let newList = {
                title : this.input
            }
            if (this.input !== '') {
                this.list.push(newList)
                this.input = ""
            } else {
                alert("Tidak boleh kosong")
            }
            
        },
        deleteList(index) {
            this.list.splice(index, 1);
        },
        toggleDescription() {
            this.tampilkanDeskripsi = !this.tampilkanDeskripsi
        }
    },
    mounted() {
        console.log('Component mounted.')
    },
}
</script>