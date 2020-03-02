<template>
    <v-app id="inspire">
        <v-navigation-drawer v-model="drawer" clipped app color="#003252">
            <v-list dense>
                <v-list-item link>
                    <v-list-item-action>
                        <v-icon>mdi-home</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title><router-link to="/">Home</router-link></v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
                <v-list-item link>
                    <v-list-item-action>
                        <v-icon>mdi-contact-mail</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title><router-link to="/about">About</router-link></v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
                <v-list-item link>
                    <v-list-item-action>
                        <v-icon>mdi-contact-mail</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title><router-link to="/create/post">Create post</router-link></v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>

        <v-app-bar app color="#001e32" clipped-left dark hide-on-scroll height="46px">
            <template v-slot:img="{ props }">
                <v-img v-bind="props" gradient="to top right, rgba(100,115,201,.7), rgba(25,32,72,.7)"></v-img>
            </template>

            <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

            <v-toolbar-title>
                <v-avatar size="32px" class="logo-img">
                    <img src="images/logo/n1.svg" alt="notes logo" class="header-logo-img">
                </v-avatar>
                <p class="header-logo-name">ote.it</p>
            </v-toolbar-title>

            <v-spacer></v-spacer>


            <v-menu bottom left>
                <template v-slot:activator="{ on }">
                    <v-btn icon color="white" v-on="on">
                        <v-icon>mdi-dots-vertical</v-icon>
                    </v-btn>
                </template>

                <v-list color="#001e32">
                    <v-list-item class="list-item"><v-list-item-title class="list-item-title">Profile</v-list-item-title></v-list-item>
                    <v-list-item class="list-item"><v-list-item-title class="list-item-title">RU language</v-list-item-title></v-list-item>
                    <v-list-item class="list-item"><v-list-item-title class="list-item-title">Dark theme</v-list-item-title></v-list-item>
                    <v-list-item class="list-item"><v-list-item-title class="list-item-title logout-item"><a href="#" @click.prevent="$auth.logout()">Logout</a></v-list-item-title></v-list-item>
                </v-list>
            </v-menu>

            <template v-slot:extension class="switches-link">
                <v-tabs centered fixed-tabs>
<!--                    <v-tab class="tab"><router-link to="/notes" class="router-link link">Notes</router-link></v-tab>-->
<!--                    <v-tab class="tab"><router-link to="/reminders" class="router-link link">Reminders</router-link></v-tab>-->
<!--                    <v-tab class="tab"><router-link to="/todo" class="router-link link">ToDo</router-link></v-tab>-->
                </v-tabs>
            </template>
        </v-app-bar>

        <!--    ================================= content =================================== -->
        <v-content>
            <router-view></router-view>
        </v-content>

        <!--     ======================================== footer ============================================= -->
        <v-footer color="#001e32" app>
            <span class="white--text">weather</span>
        </v-footer>
    </v-app>
</template>

<script>
    export default {
        props: {
            source: String,
        },
        data: () => ({
            drawer: null,
            primaryDrawer: {
                clipped: false
            },
        }),
    }
</script>

<style scoped>
    .header-logo-name {
        margin: 0;
        padding-top: 10px;
    }

    .v-avatar {
        border-radius: 0;
    }

    .v-toolbar__title {
        display: flex;
        align-items: center;
    }

    .tab {
        max-width: 240px;
    }

    .router-link {
        padding: 15px 0;
        width: 100%;
        text-decoration: none;
        color: #fff;
        font-family: 'NunitoR', sans-serif;
    }

    .logout-item {
        border-top: 1px solid #fff;
        padding-top: 10px;
        color: #fff;
    }
</style>
