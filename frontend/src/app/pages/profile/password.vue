<template>
    <div class="change-password">
        <v-form v-model="valid">
            <v-text-field
              v-model="password"
              :append-icon="show1 ? 'visibility_off' : 'visibility'"
              :type="show1 ? 'text' : 'password'"
              @click:append="show1 = !show1"
              label="Old password"
              id="password"
              required
            ></v-text-field>
            <v-text-field
              v-model="newPassword"
              :append-icon="show2 ? 'visibility_off' : 'visibility'"
              :type="show2 ? 'text' : 'password'"
              @click:append="show2 = !show2"
              label="New password"
              required
              id="newPassword"
            ></v-text-field>
            <v-text-field
              v-model="newPasswordAgain"
              :append-icon="show3 ? 'visibility_off' : 'visibility'"
              :type="show3 ? 'text' : 'password'"
              @click:append="show3 = !show3"
              label="New password"
              required
              id="newPasswordAgain"
            ></v-text-field>
            <v-btn @click.native="save()" color="primary">Change Password</v-btn>
          </v-form>
    </div>
</template>

<script>
    import User from 'model/user';

    export default {
        name: 'change-password',
        data() {
            return {
                'model': this.$session.getUser(),
                'password': '',
                'newPassword': '',
                'newPasswordAgain': '',
                show1: false,
                show2: false,
                show3: false,
            };
        },
        methods: {
            save() {
                this.model.changePassword(this.password, this.newPassword).then(response => {
                    this.password = '';
                    this.newPassword = '';
                    this.newPasswordAgain = '';
                    this.$alert.success('Password successfully changed');
                });
            },
        }
    };
</script>
