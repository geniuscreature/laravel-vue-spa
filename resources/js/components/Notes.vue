<template>
    <div class="content">
        <button class="add-btn" color="pink" dark fab @click="dialog = !dialog">
            +
        </button>
        <v-dialog v-model="dialog" width="700px" color="#001a2b">
            <v-card class="card">
                <v-container>
                    <form action="" method="post" class="notes-form">
                        <div class="add-note-title-input">
                            <input type="text" class="title-input add-note-input" placeholder="Note title" v-model="title">
                        </div>
                        <div class="add-note-subtitle-input">
                            <div contenteditable="true" data-text="Note" class="subtitle-input"></div>
                            <textarea v-model="content" class="textarea" hidden></textarea>
                        </div>
                    </form>
                </v-container>
                <v-card-actions>
                    <v-menu>
                        <template v-slot:activator="{ on }">
                            <v-btn icon v-on="on">
                                <img src="images/icons/fontfamily.svg" alt="" class="img-action">
                            </v-btn>
                        </template>

                        <v-list color="#001a2b">
                            <v-list-item class="list-item"><v-list-item-title @click="ff()" class="list-item-title text1">Nunito</v-list-item-title></v-list-item>
                            <v-list-item class="list-item"><v-list-item-title class="list-item-title text2">Bebas</v-list-item-title></v-list-item>
                            <v-list-item class="list-item"><v-list-item-title class="list-item-title text3">Montserrat</v-list-item-title></v-list-item>
                            <v-list-item class="list-item"><v-list-item-title class="list-item-title text4">Rubik</v-list-item-title></v-list-item>
                        </v-list>
                    </v-menu>
                    <v-menu>
                        <template v-slot:activator="{ on }">
                            <v-btn icon v-on="on">
                                <img src="images/icons/colorblack.svg" alt="" class="img-action">
                            </v-btn>
                        </template>

                        <v-list color="#001a2b">
                            <v-list-item class="list-item"><v-list-item-title class="list-item-title">Profile</v-list-item-title></v-list-item>
                            <v-list-item class="list-item"><v-list-item-title class="list-item-title">RU language</v-list-item-title></v-list-item>
                            <v-list-item class="list-item"><v-list-item-title class="list-item-title">Dark theme</v-list-item-title></v-list-item>
                            <v-list-item class="list-item"><v-list-item-title class="list-item-title logout-item">Logout</v-list-item-title></v-list-item>
                        </v-list>
                    </v-menu>
                    <v-menu>
                        <template v-slot:activator="{ on }">
                            <v-btn icon v-on="on">
                                <img src="images/icons/voiceblack.svg" alt="" class="img-action">
                            </v-btn>
                        </template>

                        <v-list color="#001a2b">
                        </v-list>
                    </v-menu>
                    <v-spacer />
                    <v-btn text color="primary" @click="dialog = false">Cancel</v-btn>
                    <v-btn text @click="save()">Save</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
    export default {
        data: () => ({
            dialog: false,
            drawer: null,
            title: '',
            content:''
        }),
        methods:{
            save(){
                this.dialog = false;
                axios.post('/create', {
                    title: this.title,
                    content: this.content,
                })
                    .then((response) => {
                        console.log(response);
                    })
                    .catch((error) => {
                        console.log(error);
                    });
            },
            ff(){
                let title = document.getElementsByClassName('title-input');
                let content = document.getElementsByClassName('subtitle-input');
                let fontfamily = document.getElementsByClassName('list-item-title');

                for (let i = 0; i < fontfamily.length; i++) {
                    fontfamily[i].addEventListener('click', function () {
                        if (i == 0) {
                                console.log('eew');
                            title.style.fontFamily = 'NunitoR';
                            content.style.fontFamily = 'NunitoR';
                            console.log('eew');
                        } else if (i == 1) {
                            title.style.fontFamily = 'BebasR';
                            content.style.fontFamily = 'BebasR';
                        } else if (i == 2) {
                            title.style.fontFamily = 'MontserratR';
                            content.style.fontFamily = 'MontserratR';
                        } else {
                            title.style.fontFamily = 'RubikR';
                            content.style.fontFamily = 'RubikR';
                        }
                    });
                }
            },
        }
    }
</script>

<style scoped>
    .add-btn {
        color: #fff;
        border: 1px solid #fff;
        font-size: 1.5rem;
        box-shadow: 0px 3px 5px -1px rgba(0, 0, 0, 0.2), 0px 6px 10px 0px rgba(0, 0, 0, 0.14), 0px 1px 18px 0px rgba(0, 0, 0, 0.12);
        width: 100px;
        height: 100px;
    }

    .card {
        border: 1px solid #fff;
        background: #001a2b;
    }

    .img-action {
        width: 20px;
        height: 20px;
    }

    .text1 {
        font-family: 'NunitoR', sans-serif;
    }

    .text2 {
        font-family: 'BebasR', sans-serif;
    }

    .text3 {
        font-family: 'MontserratR', sans-serif;
    }

    .text4 {
        font-family: 'RubikR', sans-serif;
    }
</style>
