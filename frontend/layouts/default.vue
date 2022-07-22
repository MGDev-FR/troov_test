<template>
    <div>
        <b-navbar toggleable="lg" type="dark" variant="info" class="mb-5">
            <b-navbar-brand to="/">Troov'APP</b-navbar-brand>

            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav v-if="$auth.loggedIn">
                <b-nav-item to="/user/my-account"><b-icon-user></b-icon-user> Mon compte</b-nav-item>
                <b-nav-item @click="$auth.logout()"><b-icon-box-arrow-left></b-icon-box-arrow-left> Déconnexion</b-nav-item>
            </b-navbar-nav>
            <b-navbar-nav v-else>
                <b-nav-item to="/login">Connexion</b-nav-item>
                <b-nav-item to="/register">Inscription</b-nav-item>
            </b-navbar-nav>
            </b-collapse>
        </b-navbar>

        <div class="router-view">
            <Nuxt />
        </div>
    </div>
</template>
