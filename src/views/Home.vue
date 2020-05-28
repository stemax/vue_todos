<template>
<div>
    <b-jumbotron bg-variant="info" text-variant="white" border-variant="dark">
        <template v-slot:header>TODO Application Homepage</template>
        <template v-slot:lead>
            This is a simple VUE JS + Vue Router + BootstrapVue components application.
        </template>
        <hr class="my-4">
        <p>
            It uses utility classes for typography and spacing to space content out within the larger
            container.
        </p>
        <b-button variant="success" to="/todos">Check Todo functional now</b-button>
    </b-jumbotron>
   <!-- <router-link to="/todos">Todos</router-link>-->
</div>
</template>
