<template>
    <div>
        <vue-excel-xlsx
            :data="rows"
            :columns="columns"
            :file-name="`katilimcilar_${(new Date().toJSON().slice(0,10))}`"
            :file-type="'xlsx'"
            :sheet-name="'sheetname'">
            Excel İndir
        </vue-excel-xlsx>
        <datatable :columns="columns" :data="rows"></datatable>
    </div>
</template>

<script>
export default {
    data() {
        return {
            columns: [
                { label: "id", field: "id" },
                { label: "Instagram", field: "instagram" },
                { label: "Name", field: "name" },
                { label: "Eposta", field: "email" },
                { label: "Mobil", field: "mobile" },
                { label: "Doğum Tarihi", field: "birthday" },
                { label: "Adres", field: "address" },
                { label: "IP", field: "ipAddress" },
                { label: "Oluşturulma", field: "created_at" },
            ],
            rows: []
        };
    },
    created(){
        this.$axios.$get("draws").then((response) => {
            this.rows = response.data
        }).catch({})
    }
};
</script>

<style>
    table {
        width: 100% !important;
    }
    th {
        text-align: left !important;
    }
</style>