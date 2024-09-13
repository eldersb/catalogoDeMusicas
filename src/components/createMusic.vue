<template>
    <v-card class="mx-auto" max-width="960">
        <v-layout>
            <v-app-bar color="indigo-darken-4" density="compact">
                <v-app-bar-title>Cadastre sua música favorita</v-app-bar-title>
            </v-app-bar>

            <v-main>
                <v-container fluid>
                    <v-form v-model="formIsValid" ref="form" @submit.prevent="saveMusic">
                        <v-container>
                            <v-row>
                                <v-col cols="12" md="8">
                                    <v-text-field
                                    v-model="music.songName"
                                    :counter="10" :rules="songRules"
                                    label="Nome da música"
                                    required
                                    >
                                  </v-text-field>
                                </v-col>

                                <v-col cols="12" md="8">
                                    <v-text-field
                                    v-model="music.artistName"
                                    :counter="10"
                                    :rules="artistRules"
                                    label="Nome do artista"
                                    required></v-text-field>
                                </v-col>

                                <v-col cols="12" md="8">
                                    <v-text-field
                                     v-model="music.genre"
                                     :rules="genreRules"
                                     label="Estilo musical"
                                     required
                                     class="mb-5"
                                    >
                                    </v-text-field>

                                    <v-text-field
                                     v-model="music.range"
                                      :rules="rangeRules"
                                      label="Digite uma pontuação entre 1 e 5"
                                      required
                                        >
                                      </v-text-field>
                                </v-col>

                                <v-col cols="6">
                                    <v-btn color="grey-darken-3" type="submit">Cadastrar</v-btn>
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
            <v-app-bar color="indigo-darken-4" density="compact">
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
                            <tr v-for="music in musics" :key="music.songName">
                                <td>{{ music.songName }}</td>
                                <td>{{ music.artistName }}</td>
                                <td>{{ music.genre }}</td>
                                <td>{{ music.range }}</td>
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
        formIsValid: false,
        dialog: false,
        dialogTitle: '',
        dialogMessage: '',
        valid: false,
        music: {
            songName: '',
            artistName: '',
            genre: '',
            range: ''
        },
        musics: [],
        songRules: [
          value => (value && value.trim()) ? true : 'Nome da música é obrigatório.',
        ],
        artistRules: [
          value => (value && value.trim()) ? true : 'Nome do artista é obrigatório.',
        ],
        genreRules: [
          value => (value && value.trim()) ? true : 'Estilo musical é obrigatório.',
        ],
        rangeRules: [
          value => (value && value.trim()) ? true : 'Pontuação é obrigatória.',
          value => {
            if (value && value >= 1 && value <= 5) return true

            return 'Pontuação deve ser entre 1 e 5'
          }
        ],
    }),

    methods: {
        saveMusic(){

          this.$refs.form.validate();

          if(this.checkMusic()){
            this.dialogTitle = "Ops!!";
            this.dialogMessage = "Essa música já foi cadastrada!";
            this.dialog = true;
            return
          }

          if(this.formIsValid) {

              this.musics.push({...this.music});

              this.music = {songName: '', artistName: '', genre: '', range: ''};

              this.dialogTitle = "Ok!!"
              this.dialogMessage = "Música cadastrada com sucesso!"
              this.dialog = true

            }

        },
        checkMusic() {
            return this.musics.some(existingMusic =>
              existingMusic.songName === this.music.songName
            );
            }
        }

    }


</script>

<style scoped>
    /* .custom-text-field {
      color: #FF5722;
    } */
</style>
