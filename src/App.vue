<template>

    <div>

        <div uk-sticky class="uk-navbar-container tm-navbar-container uk-active">
            <div class="uk-container uk-container-expand">
                <nav uk-navbar>
                    <div class="uk-navbar-left">
                        <a id="sidebar_toggle" class="uk-navbar-toggle" uk-navbar-toggle-icon></a>
                        <a href="/" class="uk-navbar-item uk-logo">
                            {{title}}
                        </a>
                    </div>
                    <div class="uk-navbar-right uk-light">
                        <Lang></Lang>
                    </div>
                </nav>
            </div>
        </div>
        <div id="sidebar" class="tm-sidebar-left uk-background-default">
            <center>
                <div class="user"><a href="#">{{$store.state.user.data.email}}</a>
                </div>
                <br/>
            </center>
            <LeftBar></LeftBar>
        </div>
        <router-view></router-view>
    </div>
</template>

<script>
    /* eslint-disable no-new */
    import * as types from './store/types'
    import LeftBar from './components/Leftbar.vue'
    import Lang from './components/Lang.vue'
    import rest from './http/rest'
    import http from './http/base'
    import {getLang} from './tools/util'

    export default {
        name: 'App',
        data () {
            return {
                title: 'ss-panel',
                user: {
                },
            }
        },
        methods: {
            handleCfg: function () {
                http.get("config")
                    .then(response => {
                        // JSON responses are automatically parsed.
                        this.title = response.data.data.app;
                        document.title = response.data.data.app;
                    })
                    .catch(e => {
                        this.errors.push(e)
                    })
            },
            checkToken: function () {
                let token = sessionStorage.getItem('token');
                let id = sessionStorage.getItem('id');
                if (!token) {
                    window.location.href = '/';
                }
                this.$store.commit(types.Login, {
                    token: token,
                    id: id,
                });
            },
            checkLang(){
                let lang = sessionStorage.getItem('lang');
                console.log("get lang from session: " + lang);
                if (!lang) {
                    console.log("load default lang: ", getLang());
                    return this.$store.commit(types.ChangeLocale, getLang());
                }
                this.$store.commit(types.ChangeLocale, lang);
            },
            initUser(){
                rest.get("")
                    .then(response => {
                        // JSON responses are automatically parsed.
                        this.user = response.data;
                        this.$store.commit(types.StoreUser, response.data);
                        console.log(this.user);
                    })
                    .catch(e => {
                        sessionStorage.removeItem('token');
                        window.location.href = '/';
                    })
            }
        },
        mounted: function () {
            this.handleCfg();
            this.checkToken();
            this.initUser();
            this.checkLang();
        },
        components: {
            LeftBar,
            Lang,
        }
    }
</script>
