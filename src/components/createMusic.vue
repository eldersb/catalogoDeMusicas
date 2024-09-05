<template>
    <v-card class="mx-auto" max-width="960">
        <v-layout>
            <v-app-bar color="pink-lighten-2" density="compact">
                <v-app-bar-title>Cadastre sua música favorita</v-app-bar-title>
            </v-app-bar>

            <v-main>
                <v-container fluid>
                    <v-form v-model="valid" @submit.prevent>
                        <v-container>
                            <v-row>
                                <v-col cols="12" md="8">
                                    <v-text-field v-model="music.songName" :counter="10" :rules="songRules"
                                        label="Nome da música" hide-details required></v-text-field>
                                </v-col>

                                <v-col cols="12" md="8">
                                    <v-text-field v-model="music.artistName" :counter="10" :rules="artistRules"
                                        label="Nome do artista" hide-details required></v-text-field>
                                </v-col>

                                <v-col cols="12" md="8">
                                    <v-text-field v-model="music.genre" :rules="genreRules" label="Estilo musical"
                                        hide-details required class="mb-5"></v-text-field>

                                    <v-text-field v-model="music.range" :rules="rangeRules" label="Pontuação" hide-details
                                        required></v-text-field>



                                </v-col>

                                <v-col cols="6">
                                    <v-btn color="white" @click="saveMusic" type="submit">Cadastrar</v-btn>
                                </v-col>
                            </v-row>
                        </v-container>
                    </v-form>


                </v-container>
            </v-main>
        </v-layout>
    </v-card>

    <v-card class="mx-auto mt-5" max-width="960">
        <v-layout>
            <v-app-bar color="pink-lighten-2" density="compact">
                <v-app-bar-title>Músicas cadastradas</v-app-bar-title>
            </v-app-bar>

            <v-main>
                <v-container fluid>
                    <v-table>
                        <thead>
                            <tr>
                                <th class="text-left">
                                   Música
                                </th>
                                <th class="text-left">
                                   Artista
                                </th>
                                <th class="text-left">
                                   Estilo
                                </th>
                                <th class="text-left">
                                   Pontuação
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="item in desserts" :key="item.name">
                                <td>{{ item.name }}</td>
                                <td>{{ item.calories }}</td>
                            </tr>
                        </tbody>
                    </v-table>

                </v-container>
            </v-main>
        </v-layout>
    </v-card>

    <v-dialog v-model="dialog" width="auto">
        <v-card max-width="400" prepend-icon="mdi-check-bold" :text="dialogMessage" :title="dialogTitle">
            <template v-slot:actions>
                <v-btn class="ms-auto" text="Ok" @click="dialog = false"></v-btn>
            </template>
        </v-card>
    </v-dialog>
</template>

<script>
export default {
    data: () => ({
        valid: false,
        firstname: '',
        lastname: '',
        music: {
            songName: '',
            artistName: '',
            genre: '',
            range: ''
        },
        musics: [],
        nameRules: [
            value => {
                if (value) return true

                return 'Name is required.'
            },
            value => {
                if (value?.length <= 10) return true

                return 'Name must be less than 10 characters.'
            },
        ],
        email: '',
        emailRules: [
            value => {
                if (value) return true

                return 'E-mail is requred.'
            },
            value => {
                if (/.+@.+\..+/.test(value)) return true

                return 'E-mail must be valid.'
            },
        ],
    }),

    methods: {
        saveMusic(){
            this.musics.push(this.music)
        }
    }

}
</script>