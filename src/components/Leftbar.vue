<template>
<div>
    <ul class="uk-nav uk-nav-default">
        <li class="uk-nav-header">
            {{ $t("user-nav.user-home") }}
        </li>
        <li class="uk-nav">
            <router-link tag="li" :to="{ name: 'dashboard' }" exact>
            <a href="#">
                <span class="uk-margin-small-right" uk-icon="icon: user"></span>
            {{ $t("user-nav.dashboard") }}</a>
            </router-link>
        </li>
        <li class="uk-nav">
            <router-link tag="li" :to="{ name: 'nodes' }" exact>
            <a href="#">
                <span class="uk-margin-small-right" uk-icon="icon: server"></span>
                {{ $t("user-nav.node-list") }}
            </a>
            </router-link>
        </li>
        <li class="uk-nav">
            <router-link tag="li" :to="{ name: 'trafficLogs' }" exact>
            <a href="#">
                <span
                    class="uk-margin-small-right" uk-icon="icon: cloud-download"></span>
            {{ $t("user-nav.traffic-log") }}</a>
            </router-link>
        </li>
        <li class="uk-nav">
            <router-link tag="li" :to="{ name: 'profile' }" exact>
            <a href="#">
                <span class="uk-margin-small-right" uk-icon="icon: thumbnails"></span>
            {{ $t("user-nav.my-profile") }} </a>
            </router-link>
        </li>
        <li class="uk-nav">
            <router-link tag="li" :to="{ name: 'invite' }" exact>
            <a href="#">
                <span class="uk-margin-small-right" uk-icon="icon: users"></span>
            {{ $t("user-nav.invite-friend") }} </a>
            </router-link>
        </li>
        <li class="uk-nav">
            <router-link tag="li" :to="{ name: 'setting' }" exact>
            <a href="#">
                <span class="uk-margin-small-right" uk-icon="icon: settings"></span>
            {{ $t("base.setting") }} </a>
            </router-link>
        </li>
        <li class="uk-nav" v-if="$store.state.user.data.is_admin">
            <a href="/admin">
                <span class="uk-margin-small-right" uk-icon="icon:  more-vertical"></span>
            {{ $t("user-nav.admin-panel") }} </a>
        </li>
        <li class="uk-nav-divider">
        </li>
        <li class="uk-nav">
            <router-link tag="li" :to="{ name: 'logout' }" exact>
            <a href="#">
                <span class="uk-margin-small-right" uk-icon="icon: sign-out"></span>
            {{ $t("auth.logout") }} </a>
            </router-link>
        </li>
    </ul>
</div>


</template>

<script>
    /* eslint-disable no-new */
    import axios from 'axios'
    import * as types from '../store/types'
    import Lang from './Lang.vue'

    export default {
        name: 'LeftBar',
        data () {
            return {
                navigation: {}
            }
        },
        methods: {},
        mounted: function () {
        },
        components: {
            Lang,
        }
    };
</script>
