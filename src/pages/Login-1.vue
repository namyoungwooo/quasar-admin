<template>
    <q-layout>
        <q-page-container>
            <q-page class="flex bg-image flex-center">
                <q-card v-bind:style="$q.screen.lt.sm?{'width': '80%'}:{'width':'30%'}">
                    <q-card-section>
                        <q-avatar size="103px" class="absolute-center shadow-10">
                            <img src="profile.svg"></q-avatar>
                        </q-card-section>
                        <q-card-section>
                            <div class="text-center q-pt-lg">
                                <div class="col text-h6 ellipsis">
                                    Log in
                                </div>
                            </div>
                        </q-card-section>
                        <q-card-section>
                            <q-form class="q-gutter-md">
                                <q-input
                                    filled="filled"
                                    v-model="username"
                                    label="Username"
                                    lazy-rules="lazy-rules"/>

                                <q-input
                                    type="password"
                                    filled="filled"
                                    v-model="password"
                                    label="Password"
                                    lazy-rules="lazy-rules"/>

                                <div>
                                    <q-btn label="Login" @click="login()" type="button" color="primary"/>
                                    <!-- to="/" -->
                                </div>
                            </q-form>
                        </q-card-section>
                    </q-card>
                </q-page>
            </q-page-container>
        </q-layout>
    </template>

    <script>
        import {defineComponent} from 'vue'
        import {ref} from 'vue'
        import {useStore, mapActions, mapGetters} from "vuex";

        export default defineComponent({
            setup() {

                const store = useStore();
                //.. 람다함수, method : 안에서는 정의 못함 - 왜
                let loginTest = () => {
                    console.log('loginTest 되는군');
                }

                return {username: ref('Pratik'), password: ref('12345')}
            },

            methods: {

                login() {

                    console.log('login');
                    //loginTest(); -- not define  ... 이곳에서는 안보임
                    this.$store.commit("setFireUser", "testuser");
                    console.log('>>>>> login');
                    this.$router.push({path: "/"});
                }
            }
        })
    </script>

    <style>

        .bg-image {
            background-image: linear-gradient(135deg, #7028e4 0%, #e5b2ca 100%);
        }
    </style>
