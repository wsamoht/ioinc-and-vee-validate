<template>
    <ion-page>
        <ion-header>
            <ion-toolbar mode="md">
                <ion-title>VeeValidate Test</ion-title>
            </ion-toolbar>
        </ion-header>
        <ion-content>
            <v-form :initial-values="formValues" v-slot="{ errors, values }">
                <ion-item>
                    <ion-label position="stacked">Name</ion-label>
                    <v-field
                        name="name"
                        v-slot="{ field }"
                        rules="required|min:3"
                    >
                        <ion-input
                            type="text"
                            name="name"
                            placeholder="Your name"
                            v-bind="field"
                        />
                    </v-field>
                </ion-item>
                <ion-item>
                    <ion-label position="stacked">Email</ion-label>
                    <v-field
                        name="email"
                        v-slot="{ field }"
                        rules="required|email"
                    >
                        <ion-input
                            type="text"
                            name="email"
                            placeholder="Your email"
                            v-bind="field"
                        />
                    </v-field>
                </ion-item>
                <div style="margin-top: 50px; padding: 10px">
                    <div>
                        <b>VeeValidate values:</b>
                        <pre>{{ values }}</pre>
                    </div>
                    <div>
                        <b>VeeValidate errors:</b>
                        <pre>{{ errors }}</pre>
                    </div>
                </div>
                <div style="margin-top: 50px; padding: 10px">
                    Works correctly in Ionic versions:
                    <ul>
                        <li>5.5.2</li>
                        <li>5.5.1</li>
                        <li>5.5.0</li>
                    </ul>

                    Does not work in Ionic versions:
                    <ul>
                        <li>5.5.4</li>
                        <li>5.5.3</li>
                    </ul>
                </div>
            </v-form>
        </ion-content>
    </ion-page>
</template>

<script lang="ts">
import {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonLabel,
    IonItem,
    IonInput,
} from "@ionic/vue";
import { defineComponent } from "vue";
import {
    configure as VeeConfigure,
    Form,
    Field,
    defineRule,
} from "vee-validate";
import { required, min } from "@vee-validate/rules";

export default defineComponent({
    name: "Home",
    components: {
        IonContent,
        IonHeader,
        IonPage,
        IonTitle,
        IonToolbar,
        IonLabel,
        IonItem,
        IonInput,
        VForm: Form,
        VField: Field,
    },
    data() {
        return {
            formValues: {
                name: "",
                email: "test@test.com",
            },
        };
    },
    mounted() {
        VeeConfigure({
            validateOnInput: true,
        });

        defineRule("required", required);
        defineRule("min", min);
    },
});
</script>