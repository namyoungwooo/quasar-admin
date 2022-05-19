<template>
    <q-layout view="lHh Lpr lFf">
        <q-header elevated="elevated">
            <q-toolbar >
                <q-btn
                    flat="flat"
                    dense="dense"
                    round="round"
                    @click="toggleLeftDrawer"
                    icon="menu"
                    aria-label="Menu"/>
                <q-toolbar-title>
                    <div v-if="logined()">
                        Wise Haccp App
                    </div>
                    <div v-if="!isUserAuth">
                        Not Logined
                    </div>
                </q-toolbar-title>
                <q-space/>
                <div class="q-gutter-sm row items-center no-wrap">
                    <q-btn
                        round="round"
                        dense="dense"
                        flat="flat"
                        color="white"
                        :icon="$q.fullscreen.isActive ? 'fullscreen_exit' : 'fullscreen'"
                        @click="$q.fullscreen.toggle()"
                        v-if="$q.screen.gt.sm"></q-btn>
                    <q-btn
                        round="round"
                        dense="dense"
                        flat="flat"
                        color="white"
                        icon="fab fa-github"
                        type="a"
                        href="https://github.com/pratik227/quasar-admin"
                        target="_blank"></q-btn>
                    <q-btn
                        round="round"
                        dense="dense"
                        flat="flat"
                        icon="fas fa-heart"
                        style="color:#9d4182 !important;"
                        type="a"
                        href="https://github.com/sponsors/pratik227"
                        target="_blank"></q-btn>
                    <q-btn
                        round="round"
                        dense="dense"
                        flat="flat"
                        color="white"
                        icon="notifications">
                        <q-badge color="red" text-color="white" floating="floating">
                            5
                        </q-badge>
                        <q-menu >
                            <q-list style="min-width: 100px">
                                <messages></messages>
                                <q-card class="text-center no-shadow no-border">
                                    <q-btn
                                        label="View All"
                                        style="max-width: 120px !important;"
                                        flat="flat"
                                        dense="dense"
                                        class="text-indigo-8"></q-btn>
                                </q-card>
                            </q-list>
                        </q-menu>
                    </q-btn>
                    <q-btn round="round" flat="flat">
                        <q-avatar size="26px">
                            <img src="https://cdn.quasar.dev/img/boy-avatar.png"></q-avatar>
                        </q-btn>
                    </div>
                </q-toolbar>
            </q-header>

            <q-drawer
                v-model="leftDrawerOpen"
                show-if-above="show-if-above"
                bordered="bordered"
                class="bg-primary text-white">
                <q-list>
                    <q-item to="/Login-1" active-class="q-item-no-link-highlighting">
                        <q-item-section avatar="avatar">
                            <q-icon name="email"/>
                        </q-item-section>
                        <q-item-section>
                            <q-item-label>Login-1</q-item-label>
                        </q-item-section>
                    </q-item>

                    <q-expansion-item icon="pages" label="Pages">
                        <q-list class="q-pl-lg">
                            <q-item to="/Login-1" active-class="q-item-no-link-highlighting">
                                <q-item-section avatar="avatar">
                                    <q-icon name="email"/>
                                </q-item-section>
                                <q-item-section>
                                    <q-item-label>Login-1</q-item-label>
                                </q-item-section>
                            </q-item>
                        </q-list>
                    </q-expansion-item>

                    <!-- not completed-->
                    <q-item to="/Calendar" active-class="q-item-no-link-highlighting">
                        <q-item-section avatar="avatar">
                            <q-icon name="date_range"/>
                        </q-item-section>
                        <q-item-section>
                            <q-item-label>Calendar</q-item-label>
                        </q-item-section>
                    </q-item>

                    <q-item to="/Pagination" active-class="q-item-no-link-highlighting">
                        <q-item-section avatar="avatar">
                            <q-icon name="date_range"/>
                        </q-item-section>
                        <q-item-section>
                            <q-item-label>Pagination</q-item-label>
                        </q-item-section>
                    </q-item>
                    <q-item class="q-ml-xl" active-class="q-item-no-link-highlighting">
                        <q-item-section>
                            <q-item-label>Level 1</q-item-label>
                        </q-item-section>
                    </q-item>

                </q-list>
            </q-drawer>

            <q-page-container class="bg-grey-2">
                <router-view/>
            </q-page-container>
        </q-layout>
    </template>

    <script>
        import EssentialLink from 'components/EssentialLink.vue'
        import Messages from "./Messages";

        import {defineComponent, ref} from 'vue'
        import {useRouter, useRoute} from "vue-router";
        import {useStore, mapActions, mapGetters} from "vuex";
        //import { emptyStatement } from '@babel/types';

        export default defineComponent({
            name: 'MainLayout',

            components: {
                EssentialLink,
                Messages
            },

            setup() {
                const leftDrawerOpen = ref(false);
                // const store = useStore(); const store1 = useStore();   의미 없음... store로 생성시
                // 고정해 둔 듯

                return {
                    leftDrawerOpen,
                    toggleLeftDrawer() {
                        leftDrawerOpen.value = !leftDrawerOpen.value
                    }
                }
            },

            methods: {
                ...mapGetters(["getFireUser", "isUserAuth"]),

                logined() {
                    if (this.getFireUser() == null || this.getFireUser() == undefined || this.getFireUser() == '')
                        return false;
                    else
                        return true;

                    }
                },
            beforeMount() {
                //this.$store.commit("setFireUser", "testuser");

                console.log('beforeMount----');
                console.log('1=> ' + this.$store1); //통과.. 모든 객체는 setup()에서 할것
                // console.log('1-1=> '  + $store1);  죽어.. -- stro
                // this.$store.commit("setFireUser", "test%%");  ok console.log('3=> ' +
                // this.$store.getters.fireUser );   ok

                console.log('4=> getFireUser() =>' + this.getFireUser()); //ok --- mapGetters의 힘

                if (this.getFireUser() == null || this.getFireUser() == undefined || this.getFireUser() == '')
                    this
                        .$router
                        .push({path: "/Login-1"});
                console.log('beforeMount end');
            },

            mounted() {

                if (localStorage.checkbox && localStorage.checkbox !== "") {
                    this.remember = true;
                    this.email = localStorage.username;
                } else {
                    this.remember = false;
                }
            }
        })
    </script>
