<template>
    <div>
        <b-navbar toggleable="lg" type="dark" variant="info" class="mb-5">
            <b-navbar-brand to="/">Troov'APP</b-navbar-brand>

            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav v-if="$auth.loggedIn">
                Username
                <b-nav-item @click="$auth.logout()">Logout</b-nav-item>
            </b-navbar-nav>
            <b-navbar-nav v-else>
                <b-nav-item to="/login">Login</b-nav-item>
                <b-nav-item to="/register">Register</b-nav-item>
            </b-navbar-nav>
            </b-collapse>
        </b-navbar>

        <div class="router-view">
            <Nuxt />
        </div>
    </div>
</template>
