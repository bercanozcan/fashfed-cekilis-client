<template>
    <div>
        <el-row>
            <el-col :span="24">
                <div class="header">
                    <div class="logo">
                        <img src="/logo.svg" class="logoImage" />
                    </div>
                </div>
            </el-col>
        </el-row>
        <el-row v-loading="loading">
            <el-col :span="18" :offset="3">
                <div class="grid-content bg-purple">
                    <div class="head">
                        <h1>FashFed Çekiliş Formu</h1>
                    </div>
                </div>
            </el-col>
            <el-col
                :xs="{ span: 22, offset: 1 }"
                :sm="{ span: 22, offset: 1 }"
                :md="{ span: 18, offset: 4 }"
                :lg="{ span: 12, offset: 6 }"
                :xl="{ span: 8, offset: 8 }"
            >
                <div class="grid-content bg-purple">
                    <div class="description" v-if="!formResponse">
                        <p>
                            Lorem ipsum dolor sit amet ipsum dolor sit amet
                            ipsum dolor sit amet ipsum dolor sit amet ipsum
                            dolor sit amet ipsum dolor sit amet ipsum dolor sit
                            amet ipsum dolor sit amet Lorem ipsum dolor sit amet
                            ipsum dolor sit amet ipsum dolor sit amet ipsum
                            dolor sit amet ipsum dolor sit amet ipsum dolor
                        </p>
                    </div>

                    <div class="success" v-if="formResponse">
                        <span>{{ alertMessage }}</span>
                    </div>
                    <el-form v-if="!formResponse">
                        <el-form-item class="formItem">
                            <el-input
                                v-model="feshFedForm.name"
                                class="formInput"
                                prop="name"
                                :class="{
                                    borderActive: errorField.name.status,
                                }"
                            ></el-input>
                            <span class="formLabel">Ad Soyad</span>
                            <small
                                class="errorMessage"
                                v-if="errorField.name.status"
                                >{{ errorField.name.message }}</small
                            >
                        </el-form-item>
                        <el-form-item class="formItem">
                            <el-input
                                v-model="feshFedForm.instagram"
                                class="formInput"
                                prop="instagram"
                                :class="{
                                    borderActive: errorField.name.status,
                                }"
                            ></el-input>
                            <span class="formLabel"
                                >Instagram Kullanıcı Adı</span
                            >
                            <small
                                class="errorMessage"
                                v-if="errorField.instagram.status"
                                >{{ errorField.instagram.message }}</small
                            >
                        </el-form-item>
                        <span class="birthdaySpan">Doğum Tarihiniz</span>
                        <el-row :gutter="10">
                            <el-col :span="8">
                                <el-select
                                    v-model="feshFedForm.day"
                                    filterable
                                    placeholder="Gün"
                                    prop="day"
                                    :class="{
                                        borderActive: errorField.name.status,
                                    }"
                                >
                                    <el-option
                                        v-for="item in dayOptions"
                                        :key="item.value"
                                        :label="item.label"
                                        :value="item.value"
                                    >
                                    </el-option>
                                </el-select>
                                <small
                                    class="errorMessage"
                                    v-if="errorField.day.status"
                                    >{{ errorField.day.message }}</small
                                >
                            </el-col>
                            <el-col :span="8">
                                <el-select
                                    v-model="feshFedForm.mounth"
                                    filterable
                                    placeholder="Ay"
                                    prop="mounth"
                                    :class="{
                                        borderActive: errorField.name.status,
                                    }"
                                >
                                    <el-option
                                        v-for="item in mounthOptions"
                                        :key="item.value"
                                        :label="item.label"
                                        :value="item.value"
                                    >
                                    </el-option>
                                </el-select>
                                <small
                                    class="errorMessage"
                                    v-if="errorField.mounth.status"
                                    >{{ errorField.mounth.message }}</small
                                >
                            </el-col>
                            <el-col :span="8">
                                <el-select
                                    v-model="feshFedForm.year"
                                    filterable
                                    placeholder="Yıl"
                                    prop="year"
                                    :class="{
                                        borderActive: errorField.name.status,
                                    }"
                                >
                                    <el-option
                                        v-for="item in yearOptions"
                                        :key="item.value"
                                        :label="item.label"
                                        :value="item.value"
                                    >
                                    </el-option>
                                </el-select>
                                <small
                                    class="errorMessage"
                                    v-if="errorField.year.status"
                                    >{{ errorField.year.message }}</small
                                >
                            </el-col>
                        </el-row>
                        <el-form-item class="formItemAddress">
                            <el-input
                                v-model="feshFedForm.address"
                                type="textarea"
                                :rows="2"
                                class="formInput"
                                resize="none"
                                prop="address"
                                :class="{
                                    borderActive: errorField.name.status,
                                }"
                            ></el-input>
                            <span class="formLabel">Adres</span>
                            <small
                                class="errorMessage"
                                v-if="errorField.address.status"
                                >{{ errorField.address.message }}</small
                            >
                        </el-form-item>
                        <el-form-item class="formItem">
                            <el-input
                                v-model="feshFedForm.email"
                                class="formInput"
                                :autofocus="true"
                                prop="email"
                                :class="{
                                    borderActive: errorField.name.status,
                                }"
                            ></el-input>
                            <span class="formLabel">Eposta Adresi</span>
                            <small
                                class="errorMessage"
                                v-if="errorField.email.status"
                                >{{ errorField.email.message }}</small
                            >
                        </el-form-item>
                        <el-form-item class="formItem">
                            <el-input
                                v-model="feshFedForm.mobile"
                                v-mask="'0 (5##) ### ## ##'"
                                class="formInput"
                                :autofocus="true"
                                prop="mobile"
                                :class="{
                                    borderActive: errorField.name.status,
                                }"
                            ></el-input>
                            <span class="formLabel"
                                >Cep Telefonu Numaranız</span
                            >
                            <small
                                class="errorMessage"
                                v-if="errorField.mobile.status"
                                >{{ errorField.mobile.message }}</small
                            >
                        </el-form-item>
                        <el-row>
                            <el-col :span="24">
                                <ul class="aggreeList">
                                    <li>
                                        <el-tooltip
                                            class="item"
                                            effect="dark"
                                            content="Lütfen sözleşmeyi okuyun."
                                            placement="left"
                                        >
                                            <el-checkbox
                                                :disabled="true"
                                                v-model="feshFedForm.aggree1"
                                                size="medium"
                                                prop="aggree1"
                                            ></el-checkbox>
                                        </el-tooltip>
                                        <span @click="aggreDialog1 = true"
                                            ><b
                                                >Çekiliş Yasal Süreçlerine
                                                Yönelik Aydınlatma Metni</b
                                            >'ni okudum, kabul ediyorum.</span
                                        >
                                    </li>
                                    <li>
                                        <el-tooltip
                                            class="item"
                                            effect="dark"
                                            content="Lütfen sözleşmeyi okuyun."
                                            placement="left"
                                        >
                                            <el-checkbox
                                                :disabled="true"
                                                v-model="feshFedForm.aggree2"
                                                size="medium"
                                                prop="aggree2"
                                            ></el-checkbox>
                                        </el-tooltip>
                                        <span @click="aggreDialog2 = true"
                                            ><b
                                                >Kişisel Verilerin İşlenmesine
                                                Yönelik Aydınlatma Metni</b
                                            >'ni okudum, kabul ediyorum.</span
                                        >
                                    </li>
                                </ul>
                            </el-col>
                        </el-row>
                        <el-button class="submitForm" @click="submitForm"
                            >GÖNDER</el-button
                        >
                    </el-form>
                </div>
            </el-col>
            <el-dialog
                title="Çekiliş Yasal Süreçlerine Yönelik Aydınlatma Metni"
                :visible.sync="aggreDialog1"
                width="90%"
            >
                <span>This is a message</span>
                <span slot="footer" class="dialog-footer">
                    <el-button
                        @click="
                            (aggreDialog1 = false),
                                (feshFedForm.aggree1 = false)
                        "
                        >İptal</el-button
                    >
                    <el-button
                        @click="
                            (aggreDialog1 = false), (feshFedForm.aggree1 = true)
                        "
                        >Kabul Ediyorum</el-button
                    >
                </span>
            </el-dialog>
            <el-dialog
                title="Kişisel Verilerin İşlenmesine Yönelik Aydınlatma Metni"
                :visible.sync="aggreDialog2"
                width="90%"
            >
                <span>This is a message</span>
                <span slot="footer" class="dialog-footer">
                    <el-button
                        @click="
                            (aggreDialog2 = false),
                                (feshFedForm.aggree2 = false)
                        "
                        >İptal</el-button
                    >
                    <el-button
                        @click="
                            (aggreDialog2 = false), (feshFedForm.aggree2 = true)
                        "
                        >Kabul Ediyorum</el-button
                    >
                </span>
            </el-dialog>
        </el-row>
    </div>
</template>

<script>
export default {
    data() {
        return {
            alertMessage: "",
            formResponse: false,
            loading: false,
            errorField: {
                name: {
                    status: false,
                    message: "Ad ve soyadınızı kontrol ediniz.",
                },
                instagram: {
                    status: false,
                    message: "Instagram kullanıcı adınızı kontrol ediniz.",
                },
                day: {
                    status: false,
                    message: "Doğum gününü kontrol ediniz.",
                },
                mounth: {
                    status: false,
                    message: "Doğum ayını kontrol ediniz.",
                },
                year: {
                    status: false,
                    message: "Doğum yılını kontrol ediniz.",
                },
                aggree1: {
                    status: false,
                    message: "Bu alanı kontrol ediniz.",
                },
                aggree2: {
                    status: false,
                    message: "Bu alanı kontrol ediniz.",
                },
                mobile: {
                    status: false,
                    message: "Cep telefonu numaranızı kontrol ediniz.",
                },
                email: {
                    status: false,
                    message: "Eposta adresinizi kontrol ediniz.",
                },
                address: {
                    status: false,
                    message: "Adresinizi kontrol ediniz.",
                },
            },
            feshFedForm: {
                name: "",
                instagram: "",
                day: "",
                mounth: "",
                year: "",
                aggree1: false,
                aggree2: false,
                mobile: "",
                email: "",
                address: "",
            },
            aggreDialog1: false,
            aggreDialog2: false,
        };
    },
    computed: {
        dayOptions() {
            let option = [];
            for (var i = 1; i <= 31; i++) {
                option.push({
                    id: i,
                    value: i,
                    label: i,
                });
            }
            return option;
        },
        yearOptions() {
            let option = [];
            for (var i = 2004; i >= 1901; i--) {
                option.push({
                    id: i,
                    value: i,
                    label: i,
                });
            }
            return option;
        },
        mounthOptions() {
            let month = [];
            month.push({
                id: 1,
                value: "01",
                label: "Ocak",
            });
            month.push({
                id: 2,
                value: "02",
                label: "Şubat",
            });
            month.push({
                id: 3,
                value: "03",
                label: "Mart",
            });
            month.push({
                id: 4,
                value: "04",
                label: "Nisan",
            });
            month.push({
                id: 5,
                value: "05",
                label: "Mayıs",
            });
            month.push({
                id: 6,
                value: "06",
                label: "Haziran",
            });
            month.push({
                id: 7,
                value: "07",
                label: "Temmuz",
            });
            month.push({
                id: 8,
                value: "08",
                label: "Ağustos",
            });
            month.push({
                id: 9,
                value: "09",
                label: "Eylül",
            });

            month.push({
                id: 10,
                value: "10",
                label: "Ekim",
            });

            month.push({
                id: 11,
                value: "11",
                label: "Kasım",
            });

            month.push({
                id: 12,
                value: "12",
                label: "Aralık",
            });

            return month;
        },
    },
    watch: {
        "feshFedForm.name"(val) {
            if (val.length > 0) {
                this.errorField.name.status = false;
            } else {
                this.errorField.name.status = true;
            }
        },
        "feshFedForm.instagram"(val) {
            if (val.length > 0) {
                this.errorField.instagram.status = false;
            } else {
                this.errorField.instagram.status = true;
            }
        },
        "feshFedForm.day"(val) {
            if (this.feshFedForm.day > 0) {
                this.errorField.day.status = false;
            } else {
                this.errorField.day.status = true;
            }
        },
        "feshFedForm.month"(val) {
            if (this.feshFedForm.month) {
                this.errorField.month.status = false;
            } else {
                this.errorField.name.status = true;
            }
        },
        "feshFedForm.year"(val) {
            if (this.feshFedForm.year) {
                this.errorField.year.status = false;
            } else {
                this.errorField.year.status = true;
            }
        },
        "feshFedForm.address"(val) {
            if (this.feshFedForm.address.length > 0) {
                this.errorField.address.status = false;
            } else {
                this.errorField.address.status = true;
            }
        },
        "feshFedForm.email"(val) {
            if (val.length > 0) {
                this.errorField.email.status = false;
            } else {
                this.errorField.email.status = true;
            }
        },
        "feshFedForm.mobile"(val) {
            if (val.length > 0) {
                this.errorField.mobile.status = false;
            } else {
                this.errorField.mobile.status = true;
            }
        },
    },
    methods: {
        async submitForm() {
            const data = this.feshFedForm;

            if (data.name.length === 0)
                return (this.errorField.name.status = true);
            if (data.instagram.length === 0)
                return (this.errorField.instagram.status = true);
            if (data.day.length === 0)
                return (this.errorField.day.status = true);
            if (data.mounth.length === 0)
                return (this.errorField.mounth.status = true);
            if (data.year.length === 0)
                return (this.errorField.year.status = true);
            if (data.mobile.length === 0)
                return (this.errorField.mobile.status = true);
            if (data.address.length === 0)
                return (this.errorField.address.status = true);
            if (data.email.length === 0)
                return (this.errorField.email.status = true);

            this.loading = true;

            await this.$axios.post(
                "draws",
                data
            ).then((response) => {
                if(response.data.status){
                    this.formResponse = true
                    this.alertMessage = response.data.message
                }else{
                    this.$notify({
                        title: 'Uyarı!',
                        message: response.data.message,
                        type: 'warning'
                    });
                }
                this.loading = false;
            }).catch({});
        },
    },
};
</script>

<style>
* {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-family: "Roboto", sans-serif;
}

body {
    margin: 0;
    padding: 0;
}

.header {
    height: 100px;
    background-color: #000;
}

.logo {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.logoImage {
    height: 48px;
}

.head {
    margin-top: 30px;
    display: flex;
    justify-content: center;
    border-bottom: 1px solid #e5e5e5;
    margin-bottom: 25px;
}

.head h1 {
    font-weight: 500;
    font-size: 22px;
}

.formItem {
    position: relative;
}

.formInput .el-input__inner {
    height: 62px !important;
    width: 100%;
    transition: all 0.3s;
    padding-top: 15px;
    font-size: 16px;
    border-radius: 0px;
}

.formItemAddress .formInput .el-textarea__inner {
    width: 100%;
    transition: all 0.3s;
    padding-top: 25px;
    font-size: 16px;
    border-radius: 0px;
}

.el-select {
    width: 100%;
}

.el-select .el-input .el-input__inner {
    height: 62px !important;
    width: 100%;
    transition: all 0.3s;
    font-size: 14px;
    border-radius: 0px;
    color: #000;
    margin-bottom: 10px;
}

.formLabel {
    position: absolute;
    top: -2px;
    left: 16px;
    font-size: 12px;
    margin: 0;
    display: block;
    color: #9d9d9d;
}

.birthdaySpan {
    margin-bottom: 15px;
    display: block;
    color: #9d9d9d;
}

.formItemAddress {
    margin-top: 15px;
}

.submitForm {
    background-color: black;
    color: #fff;
    width: 100%;
    height: 62px;
    margin-top: 20px;
    margin-bottom: 100px;
}

.aggreHead {
    text-align: center;
}

.aggreeList {
    list-style-type: none;
    padding: 0;
}

.aggreeList li {
    margin-bottom: 20px;
    cursor: pointer;
}

.aggreeList li span b {
    font-weight: 500;
    cursor: pointer;
    margin-left: 10px;
}

.el-checkbox__inner {
    border: 1px solid #9d9d9d;
    border-radius: 0px;
    width: 24px;
    height: 24px;
}

.el-checkbox__inner::after {
    height: 14px;
    width: 6px;
    left: 7px;
    border-color: #000000;
}

.el-button:focus,
.el-button:hover {
    color: #000;
    border-color: #000;
    background-color: #fff;
}

.el-input.is-active .el-input__inner,
.el-input__inner:focus {
    border-color: #e5e5e5;
    outline: 0;
}

.error-border {
    border-color: red !important;
}

.el-loading-spinner .path {
    stroke: #000000;
    stroke-width: 4px;
}

.errorMessage {
    display: block;
    font-size: 10px;
    color: red;
}
.borderActive input,
.borderActive select,
.borderActive textarea {
    border-color: red !important;
}

.success span {
    font-size: 36px;
    display: block;
    margin-top: 40px;
    background-color: #70c576;
    padding: 20px;
    color: #000;
    border-radius: -1px;
    text-align: center;
}

.el-input__inner,
.el-textarea__inner {
    border-color: #c9c9c9;
}

@media (max-width: 767px) {
    .aggreeList li {
        font-size: 14px;
    }
    .logoImage {
        height: 34px;
    }
    .header {
        height: 70px;
    }
    .description {
        font-size: 13px;
    }
    .birthdaySpan {
        font-size: 15px;
    }
}


</style>
