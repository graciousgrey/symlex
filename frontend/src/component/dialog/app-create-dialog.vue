<template>
    <v-dialog v-model="show" max-width="600">
         <v-card>
            <v-card-title class="title">Create {{ modelName }}</v-card-title>
            <v-card-text>
                <form>
                    <app-form-fields :form="form"></app-form-fields>
                </form>
            </v-card-text>

            <v-card-actions>
                <v-btn color="secondary" id="cancelCreate" @click.native="close()">Cancel</v-btn>
                <v-btn color="primary" @click.native="save()">Create</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
    import Form from 'common/form';

    export default {
        name: 'app-create-dialog',
        data() {
            return {
                'model': false,
                'modelName': 'Item',
                'form': new Form(),
                'onSave': false,
                'show': false,
            };
        },
        methods: {
            open(model, form, onSave) {
                this.model = model;
                this.modelName = model.getModelName();
                this.form = form;
                this.onSave = onSave;

                this.show = true;
            },
            save() {
                if (this.onSave) {
                    this.onSave(this.form)
                }
            },
            close() {
                this.show = false;
            }
        }
    };
</script>


<style scoped>
    form {
        min-width: 400px;
    }
</style>