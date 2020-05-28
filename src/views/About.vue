<template>
<div>
    <b-jumbotron bg-variant="info" text-variant="white" border-variant="dark">
        <template v-slot:header>TODO Application About</template>
        <template v-slot:lead>
                <div style="font-size: 2rem">
                    <b-avatar badge-variant="info" src="https://avatars3.githubusercontent.com/u/2697561?s=460&v=4">
                        <template v-slot:badge><b-icon icon="star-fill"></b-icon></template>
                    </b-avatar>
                </div>
            </template>
        <hr class="my-4">
        <p>
            Author: Max Stemplevski
        </p>
        <b-button variant="warning"  href="https://github.com/stemax">https://github.com/stemax</b-button>
    </b-jumbotron>
</div>
</template>
