<template>
    <ion-grid>
        <form @submit="onSubmit">
            <ion-col>
                <ion-item>
                    <ion-label>Ziocode:</ion-label>
                    <ion-input :value="zip" @input="zip = $event.target.value" placeholder="Enter US zipcode" name="zip"></ion-input>
                </ion-item>
            </ion-col>
            <ion-col>
                <ion-button type="submit" color="primary" expand="block">Find</ion-button>
            </ion-col>
        </form>
    </ion-grid>
</template>

<script>
export default {
    name: "ZipSearch",
    data() {
        return {
            zip: ""
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();
            const isValid = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip);
            if(!isValid) {
                this.showAlert();
                this.zip=""
            } else {
                this.$emit("get-zip", this.zip);
                this.zip=""
            }
        },
        showAlert() {
            return this.$ionic.alertController.create({header: "Enter Zipcode", message: "Please enter a valid US zipcode", buttons: ["Ok"]}).then(a => a.present())
        }
    } 
}
</script>